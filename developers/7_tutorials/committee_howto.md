### Contents:
- [How to Create a new Committee Member](/developers/7_tutorials/committee_howto.md#how-to-creating-a-new-committee-member)
- [How to Propose Committee Actions](/developers/7_tutorials/committee_howto.md#how-to-propose-committee-actions)
- [How to Approve/Disapprove a Committee Proposal](/developers/7_tutorials/committee_howto.md#how-to-approvedisapprove-a-committee-proposal)
- [How Committee Proposes a Change in Fee](/developers/7_tutorials/committee_howto.md#how-committee-proposes-a-change-in-fee)

***

## Committee - How to

## How to Creating a New Committee Member

    >>> create_committee_member account "url" true


## How to Propose Committee Actions

#### Setting Smartcoin Parameters

This paragraph shows how the committee account can act using the proposed transaction system. Specifically, as an example I’m using the creation of BitShares proposal 1.10.21, a proposal to update a committee-controlled BitAsset to reduce `maximum_force_settlement_volume` for asset `CNY` from 2000 (20%) to 200 (2%).

First check the asset to see what its current configuration is:

    >>> get_asset CNY
    {
      ...
      "bitasset_data_id": "2.4.13"
    }

Then check its bitasset object to get the currently active options:

    >>> get_object 2.4.13
    {
      ...
        "options": {
          "feed_lifetime_sec": 86400,
          "minimum_feeds": 7,
          "force_settlement_delay_sec": 86400,
          "force_settlement_offset_percent": 0,
          "maximum_force_settlement_volume": 2000,
          "short_backing_asset": "1.3.0",
          "extensions": []
        },
      ...
    }

Then do `update_bitasset` to update the options. Note we copy-paste other fields from above; there is no way to selectively update only one field.

    >>> update_bitasset "CNY" {"feed_lifetime_sec" : 86400, "minimum_feeds" : 7, "force_settlement_delay_sec" : 86400, "force_settlement_offset_percent" : 0, "maximum_force_settlement_volume" : 200, "short_backing_asset" : "1.3.0", "extensions" : []} false

If this was a privatized BitAsset (i.e. a user-issued asset with feed), you could simply set the `broadcast` parameter of the above command to `true` and be done.

However this is a committee-issued asset, so we have to use a proposed transaction to update it. To create the proposed transaction, we use the transaction builder API. Create a transaction builder transaction with `begin_builder_transaction` command:

    >>> begin_builder_transaction

This returns a numeric handle used to refer to the transaction being built. In the following commands you need to replace $HANDLE with the number returned by `begin_builder_transaction` above.

    >>> add_operation_to_builder_transaction $HANDLE [12,{"fee": {"amount":
    100000000, "asset_id": "1.3.0"}, "issuer": "1.2.0", "asset_to_update":
    "1.3.113", "new_options": { "feed_lifetime_sec": 86400, "minimum_feeds": 7,
    "force_settlement_delay_sec": 86400, "force_settlement_offset_percent": 0,
    "maximum_force_settlement_volume": 200, "short_backing_asset": "1.3.0",
    "extensions": []}, "extensions": []}]
    >>> propose_builder_transaction2 $HANDLE init0 "2015-12-04T14:55:00" 3600 false

The `propose_builder_transaction` command is broken and deprecated. You need to recompile with this patch in order to use the new `propose_builder_transaction2` command which allows you to set the proposing account.

Then set fees, sign and broadcast the transaction:

    >>> set_fees_on_builder_transaction $HANDLE BTS
    >>> sign_builder_transaction $HANDLE true

**Notes:**
- `propose_builder_transaction2` modifies builder transaction in place. It is not idempotent, running it once will get you a proposal to execute the transaction, running it twice will cause you to get a proposal to propose the transaction!
- Remember to transfer enough to cover the fee to committee account and set review period to at least `committee_proposal_review_period`
- Much of this could be automated by a better wallet command.

## How to Approve/Disapprove a Committee Proposal

#### Approve Proposal

Now we need to convince the other committee members to approve. We can do so on the blockchain by asking them for approval with

    >>> approve_proposal <fee-paying-account> <proposal-id> {"active_approvals_to_add" : ["<MY-COMMITTEE-MEMBER>"]} true

where `<proposal-id>` takes the form `1.10.xxx` and identifies the actual proposal to approve.

#### Removeing Approval

A previous approval can also be removed if the proposal is not yet expired, executed or within the preview period. This is done by::

    >>> approve_proposal <fee-paying-account> <proposal-id> {"active_approvals_to_remove" : ["<MY-COMMITTEE-MEMBER>"]} true

Note that we now use `active_approvals_to_remove` instead of `active_approvals_to_add`.

## How Committee Proposes a Change in Fee

#### Create an Proposal

Let’s assume we want to propose a new fee for the account creation operation. We want 5 BTS as basic fee and want premium names to cost 2000 BTS. Additionally, a price per kbyte for the account creation transaction can be defined. We get

    {
     "account_create_operation" : {
               "basic_fee"      : 500000,
               "premium_fee"    : 200000000,
               "price_per_kbyte": 100000}
    }

We propose the fee change for account `<committee_member>` with::

    >>> propose_fee_change <committee_member> "2015-10-14T15:29:00" {"account_create_operation" : {"basic_fee": 500000, "premium_fee": 200000000, "price_per_kbyte": 100000}} false

#### Approve Proposal

Now we need to convince the other committee members to approve. We can do so on the blockchain by asking them for approval with

    >>> approve_proposal <committee_member> "1.10.1" {"active_approvals_to_add" : ["<MY-COMMITTEE-MEMBER>"]} true

where `1.10.1` is the id of the proposal in question.




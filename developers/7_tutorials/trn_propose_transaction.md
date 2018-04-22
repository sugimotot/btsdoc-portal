## Proposing a Transaction

### Contents:
- [Proposing a Transaction](/developers/7_tutorials/trn_propose_transaction.md#proposing-a-transaction-1)
- [Approving a Proposal](/developers/7_tutorials/trn_propose_transaction.md#approving-a-proposal)
- [Example: Setting Smartcoin parameter](/developers/7_tutorials/trn_propose_transaction.md#example-setting-smartcoin-parameter)

***

Proposed transactions can be used everywhere multiple parties have to agree for a transaction to become valid.

### Crafting a Transaction

If is recommended that the reader first reads through the following tutorial:

- [Manually Construct Any Transaction](/developers/7_tutorials/07_construct_transaction.md#construct-any-transaction---manually)

***

### Proposing a Transaction

A proposed transaction is encapsulated within another operation type. We can achieve this by slightly modifying our procedure:

    >>> begin_builder_transaction
    >>> add_operation_to_builder_transaction $HANDLE [opId, {operation}]

    # New:
    >>> propose_builder_transaction2 $HANDLE <proposing-account-name> <expiration> <review-period-secs> false

    >>> set_fees_on_builder_transaction $HANDLE BTS
    >>> sign_builder_transaction $HANDLE true

#### Definition

signed_transaction `graphene::wallet::wallet_api::propose_builder_transaction`(transaction_handle_type handle, time_point_sec expiration = time_point::now()+fc::minutes(1), uint32_t review_period_seconds = 0, bool broadcast = true)

signed_transaction `graphene::wallet::wallet_api::propose_builder_transaction2`(transaction_handle_type handle, string account_name_or_id, time_point_sec expiration = time_point::now()+fc::minutes(1), uint32_t review_period_seconds = 0, bool broadcast = true)

***

### Approving a Proposal

A proposal can be approved simply by:

    approve_proposal <proposing-account> <proposal_id> {"active_approvals_to_add" : ["<account-name-required-for-approval>"]} false

When replacing the final `false` with true, the transaction will be broadcasted!

Available approval options are:

- active_approvals_to_add
- active_approvals_to_remove
- owner_approvals_to_add
- owner_approvals_to_remove
- key_approvals_to_add
- key_approvals_to_remove

#### Definition

signed_transaction `graphene::wallet::wallet_api::approve_proposal`(const string &fee_paying_account, const string &proposal_id, const approval_delta &delta, bool broadcast)

Approve or disapprove a proposal.

**Return**

the signed version of the transaction 

**Parameters**

- fee_paying_account: The account paying the fee for the op.
- proposal_id: The proposal to modify.
- delta: Members contain approvals to create or remove. In JSON you can leave empty members undefined.
- broadcast: true if you wish to broadcast the transaction

***

### Example: Setting Smartcoin parameter

A simple `asset_update` takes the following form:

    get_prototype_operation asset_update_bitasset_operation
    [
      12,{
        "fee": {
          "amount": 0,
          "asset_id": "1.3.0"
        },
        "issuer": "1.2.0",
        "asset_to_update": "1.3.0",
        "new_options": {
          "feed_lifetime_sec": 86400,
          "minimum_feeds": 1,
          "force_settlement_delay_sec": 86400,
          "force_settlement_offset_percent": 0,
          "maximum_force_settlement_volume": 2000,
          "short_backing_asset": "1.3.0",
          "extensions": []
        },
        "extensions": []
      }
    ]

The operation id for the `asset_update_bitasset_operation` is thus 12 (third line) and the core elements (removing fee) of this operation take the form:

    {
       "issuer": "1.2.0",
       "asset_to_update": "1.3.0",
       "new_options": {
         "feed_lifetime_sec": 86400,
         "minimum_feeds": 1,
         "force_settlement_delay_sec": 86400,
         "force_settlement_offset_percent": 0,
         "maximum_force_settlement_volume": 2000,
         "short_backing_asset": "1.3.0",
         "extensions": []
       },
       "extensions": []
    }

We add an operation to a transaction as follows (line breaks inserted for readability):

    >>> begin_builder_transaction
    0
    >>> add_operation_to_builder_transaction
            0
            [12, {
                  "asset_to_update": "1.3.113",
                  "issuer": "1.2.0",
                  "extensions": [],
                  "new_options": {
                    "feed_lifetime_sec": 86400,
                    "force_settlement_delay_sec": 86400,
                    "short_backing_asset": "1.3.0",
                    "maximum_force_settlement_volume": 200,
                    "force_settlement_offset_percent": 0,
                    "minimum_feeds": 7,
                    "extensions": []
                  },
                }]

The corresponding asset id can be obtained with `get_asset`.

Now let’s make it a proposal for the committee members to sign:

    >>> propose_builder_transaction2 0 init0 "2015-12-10T14:55:00" 3600 false

We add a fee payed in BTS, sign and broadcast the transaction (if valid):

    >>> set_fees_on_builder_transaction 0 BTS
    >>> sign_builder_transaction 0 true
    
***



## Construct Any Transaction - Manually

### Contents:
- 
- 

***

### General Procedure

The general principle for generating, singing and broadcasting an arbitrary transactions works as follows:

1. Create an instance of the transaction builder
1. Add arbitrary operation types
1. Add the required amount of fees
1. Sign and broadcast your transaction

The corresponding API calls in the CLI Wallet are:

    >>> begin_builder_transaction
    >>> add_operation_to_builder_transaction $HANDLE [opId, {operation}]
    >>> set_fees_on_builder_transaction $HANDLE BTS
    >>> sign_builder_transaction $HANDLE true

The begin_builder_transaction call returns a number we call $HANDLE` It allows to construct several transactions in parallel and identify them individually!

The opId and the JSON structure of the operation can be obtained with:

    get_prototype_operation <operation-type>

The operation types available are:

typedef fc::static_variant<transfer_operation, limit_order_create_operation, limit_order_cancel_operation, call_order_update_operation, fill_order_operation, account_create_operation, account_update_operation, account_whitelist_operation, account_upgrade_operation, account_transfer_operation, asset_create_operation, asset_update_operation, asset_update_bitasset_operation, asset_update_feed_producers_operation, asset_issue_operation, asset_reserve_operation, asset_fund_fee_pool_operation, asset_settle_operation, asset_global_settle_operation, asset_publish_feed_operation, witness_create_operation, witness_update_operation, proposal_create_operation, proposal_update_operation, proposal_delete_operation, withdraw_permission_create_operation, withdraw_permission_update_operation, withdraw_permission_claim_operation, withdraw_permission_delete_operation, committee_member_create_operation, committee_member_update_operation, committee_member_update_global_parameters_operation, vesting_balance_create_operation, vesting_balance_withdraw_operation, worker_create_operation, custom_operation, assert_operation, balance_claim_operation, override_transfer_operation, transfer_to_blind_operation, blind_transfer_operation, transfer_from_blind_operation, asset_settle_cancel_operation, asset_claim_fees_operation, fba_distribute_operation> graphene::chain::operation

In practise, each operation has to pay a fee, and hence, each operation has to carry a `fee` member. When crafting a transaction, you now have the choice between either defining each fee for your operations individually, or you use `set_fees_on_builder_transaction` that sets the fee for each operation automatically to the chosen asset.

***

### Example: Transfer

A simple _transfer_ takes the following form:

    get_prototype_operation transfer_operation
    [
      0,{
        "fee": {
          "amount": 0,
          "asset_id": "1.3.0"
        },
        "from": "1.2.0",
        "to": "1.2.0",
        "amount": {
          "amount": 0,
          "asset_id": "1.3.0"
        },
        "extensions": []
      }
    ]

The operation id for the `transfer_operation` is thus `0` (third line) and the core elements (removing fee) of this operation take the form:

    {
      "from": "1.2.0",
      "to": "1.2.0",
      "amount": {
        "amount": 0,
        "asset_id": "1.3.0"
      }
    }

We add an operation to a transaction as follows (line breaks inserted for readability):

    >>> begin_builder_transaction
    0
    >>> add_operation_to_builder_transaction
         0
        [0,{
               "from": "1.2.0",
               "to": "1.2.0",
               "amount": {
                 "amount": 0,
                 "asset_id": "1.3.0"
               }
           }]

The corresponding `id` can be obtained with `get_account`, and `get_asset`.

We add a fee payed in BTS, sign and broadcast the transaction (if valid):

    >>> set_fees_on_builder_transaction 0 BTS
    >>> sign_builder_transaction 0 true



***

## Questions

### Contents:


**[General](/developers/7_tutorials/QA.md#general)**
- [What is the standard Bitshares address structure and format?](/developers/7_tutorials/QA.md#q-what-is-the-standard-bitshares-address-structure-and-format
)
- [What is the format of the block header?](/developers/7_tutorials/QA.md#q-what-is-the-format-of-the-block-header)
- [What is the maximum bitshares block size?](/developers/7_tutorials/QA.md#q-what-is-the-maximum-bitshares-block-size)
- [Are there any sharding mechanics currently deployed?](/developers/7_tutorials/QA.md#q-are-there-any-sharding-mechanics-currently-deployed)
- [How are SPV clients handled?](/developers/7_tutorials/QA.md#q-how-are-spv-clients-handled)
- [How is time addressed in the blockchain? Is NTP used or some other protocol?](/developers/7_tutorials/QA.md#q-how-is-time-addressed-in-the-blockchain-is-ntp-used-or-some-other-protocol)
- [How do new clients bootstrap into the network?](/developers/7_tutorials/QA.md#q-how-do-new-clients-bootstrap-into-the-network)
- [What is the average block time?](/developers/7_tutorials/QA.md#q-what-is-the-average-block-time)
- [How is accounting addressed in Bitshares? Is it a Nxt style accounting model or like Bitcoin’s UTXO](/developers/7_tutorials/QA.md#q-how-is-accounting-addressed-in-bitshares-is-it-a-nxt-style-accounting-model-or-like-bitcoins-utxo)

[**Protocol**](/developers/7_tutorials/QA.md#protocol)
- [Are there any special affordances made for privacy?](/developers/7_tutorials/QA.md#q-are-there-any-special-affordances-made-for-privacy)
- [Does the protocol provide mechanisms for overlay protocols to interact such as OR_RETURN?](/developers/7_tutorials/QA.md#q-does-the-protocol-provide-mechanisms-for-overlay-protocols-to-interact-such-as-or_return)
- [Is this done via a gossip protocol or through a federate relay?](/developers/7_tutorials/QA.md#q-is-this-done-via-a-gossip-protocol-or-through-a-federate-relay)

**[Data Structures](/developers/7_tutorials/QA.md#data-structures)**
- [What data structures are used in the blockchain?](/developers/7_tutorials/QA.md#q-what-data-structures-are-used-in-the-blockchain)

**[Public Key System](/developers/7_tutorials/QA.md#public-key-system)**
- [What public key system is used? If elliptic curve, then what is the curv?](/developers/7_tutorials/QA.md#q-what-public-key-system-is-used-if-elliptic-curve-then-what-is-the-curve)

**[Scripting Language](/developers/7_tutorials/QA.md#scripting-language)**
- [Is there a specification for Bitshares scripting language? (assuming there is one)](/developers/7_tutorials/QA.md#q-is-there-a-specification-for-bitshares-scripting-language-assuming-there-is-one)
- [Is the scripting language turing complete?](/developers/7_tutorials/QA.md#q-is-the-scripting-language-turing-complete)

***
### [Accounts](/developers/7_tutorials/QA.md#accounts)
- [How can I create, register and upgrade an account to Lifetime Membership?](/developers/7_tutorials/QA.md#q-how-can-i-create-register-and-upgrade-an-account-to-lifetime-membership)

***

### [Assets](/developers/7_tutorials/QA.md#assets-1)
- [What happens to the asset creation fee?](/developers/7_tutorials/QA.md#q-what-happens-to-the-asset-creation-fee)
- [Can I change x after creation of the asset?](/developers/7_tutorials/QA.md#qcan-i-change-x-after-creation-of-the-asset)
- [What about Parent and Child assets?](/developers/7_tutorials/QA.md#q-what-about-parent-and-child-assets)
- [Can I change the issuer?](/developers/7_tutorials/QA.md#q-can-i-changing-the-issuer)

**Fee Pool**
- [What is the fee pool all about?](/developers/7_tutorials/QA.md#q-what-is-the-fee-pool-all-about)
- [What to do if the fee pool is empty?](/developers/7_tutorials/QA.md#q-what-to-do-if-the-fee-pool-is-empty)
- [What is Fee Pool Draining?](/developers/7_tutorials/QA.md#q-what-is-fee-pool-draining)

**Market Fee**
- [What happens if I enable Market fees?](/developers/7_tutorials/QA.md#q-what-happens-if-i-enable-market-fees)
- [How to claim accumulated fees?](/developers/7_tutorials/QA.md#q-how-to-claim-accumulated-fees)
- [What if two different market fees are involved in a trade?](/developers/7_tutorials/QA.md#q-what-if-two-different-market-fees-are-involved-in-a-trade)
- [What are Asset Flags and Permissions?](/developers/7_tutorials/QA.md#q-what-are-asset-flags-and-permissions)
- [What are the Permissions?](/developers/7_tutorials/QA.md#q-what-are-the-permissions)
- [What are the Flags?](/developers/7_tutorials/QA.md#q-what-are-the-flags)

**Market Pegged Assets**
- [Can I use the same flags/permissions as for UIAs?](/developers/7_tutorials/QA.md#q-can-i-use-the-same-flagspermissions-as-for-uias)
- [What are market-pegged-asset-specific parameters?](/developers/7_tutorials/QA.md#q-what-are-market-pegged-asset-specific-parameters)


***
### [Testnet](/developers/7_tutorials/QA.md#testnet-1)

- [Public & private testnet differences What is the difference between public and private testnet?](/developers/7_tutorials/QA.md#q-public--private-testnet-differences-what-is-the-difference-between-public-and-private-testnet)

***
### [Wallet / CLI Wallet](/developers/7_tutorials/QA.md#wallet--cli-wallet-1)
- [How can I close the CLI client in a clean way?](/developers/7_tutorials/QA.md#q-how-can-i-close-the-cli-client-in-a-clean-way)
- [How can I import to my CLI client a wallet originally created in the web GUI?](/developers/7_tutorials/QA.md#q-how-can-i-import-to-my-cli-client-a-wallet-originally-created-in-the-web-gui)
- [How can I transfer a single account to a cli wallet?](/developers/7_tutorials/QA.md#q-how-can-i-transfer-a-single-account-to-a-cli-wallet)
- [Why does the CLI client crash immediately when I try to run it for the first time?](/developers/7_tutorials/QA.md#q-why-does-the-cli-client-crash-immediately-when-i-try-to-run-it-for-the-first-time)

***
### [Witness](/developers/7_tutorials/QA.md#witness)
- [Change the Signing Key of your Witness?](/developers/7_tutorials/QA.md#q-change-the-signing-key-of-your-witness)
- [How can I close the witness node in a clean way?](/developers/7_tutorials/QA.md#q-how-can-i-close-the-witness-node-in-a-clean-way)
- [How do I check whether the witness node is already synced?](/developers/7_tutorials/QA.md#q-how-do-i-check-whether-the-witness-node-is-already-synced)
- [If it seems to be unable to sync beyond a certain date?](/developers/7_tutorials/QA.md#q-if-it-seems-to-be-unable-to-sync-beyond-a-certain-date)
- [Is it safe to delete logs stored in witness_node_data_dirlogsp2p?](/developers/7_tutorials/QA.md#q-is-it-safe-to-delete-logs-stored-in-witness_node_data_dirlogsp2p)
- [What is the best way to interact with the witness node?](/developers/7_tutorials/QA.md#q-what-is-the-best-way-to-interact-with-the-witness-node)
- [What is the meaning of all those different text colors in the witness node console?](/developers/7_tutorials/QA.md#q-what-is-the-meaning-of-all-those-different-text-colors-in-the-witness-node-console)
- [Whose private key is [“BTS6MRyAjQ..”,”5KQwrPbwdL..”]? Why is it predefined ion the config.ini?](/developers/7_tutorials/QA.md#q-whose-private-key-is-bts6mryajq5kqwrpbwdl-why-is-it-predefined-ion-the-configini)


***
### Worker

***
***

## Questions and Answers

## General

#### Q. What is the standard Bitshares address structure and format?

address = ‘BTS’+base58(ripemd(sha512(compressed_pub))) (checksum obviated) But addresses are not used directly, instead you have an account (that can be controlled by one or more address, pubkey or another account). https://bitshares.org/technology/dynamic-account-permissions/


#### Q. What is the format of the block header?

    struct block_header
       {
          digest_type                   digest()const;
          block_id_type                 previous;
          uint32_t                      block_num()const { return num_from_id(previous) + 1; }
          fc::time_point_sec            timestamp;
          witness_id_type               witness;
          checksum_type                 transaction_merkle_root;
          extensions_type               extensions;

          static uint32_t num_from_id(const block_id_type& id);
       };

#### Q. What is the maximum bitshares block size?

Configurable by chain parameters.

    struct chain_parameters
    {
       /** using a smart ref breaks the circular dependency created between operations and the fee schedule */
       smart_ref<fee_schedule> current_fees;                       ///< current schedule of fees
       uint8_t                 block_interval                      = GRAPHENE_DEFAULT_BLOCK_INTERVAL; ///< interval in seconds between blocks
       uint32_t                maintenance_interval                = GRAPHENE_DEFAULT_MAINTENANCE_INTERVAL; ///< interval in sections between blockchain maintenance events
       uint8_t                 maintenance_skip_slots              = GRAPHENE_DEFAULT_MAINTENANCE_SKIP_SLOTS; ///< number of block_intervals to skip at maintenance time
       uint32_t                committee_proposal_review_period    = GRAPHENE_DEFAULT_COMMITTEE_PROPOSAL_REVIEW_PERIOD_SEC; ///< minimum time in seconds that a proposed transaction requiring committee authority may not be signed, prior to expiration
       uint32_t                maximum_transaction_size            = GRAPHENE_DEFAULT_MAX_TRANSACTION_SIZE; ///< maximum allowable size in bytes for a transaction
       uint32_t                maximum_block_size                  = GRAPHENE_DEFAULT_MAX_BLOCK_SIZE; ///< maximum allowable size in bytes for a block
       uint32_t                maximum_time_until_expiration       = GRAPHENE_DEFAULT_MAX_TIME_UNTIL_EXPIRATION; ///< maximum lifetime in seconds for transactions to be valid, before expiring
       uint32_t                maximum_proposal_lifetime           = GRAPHENE_DEFAULT_MAX_PROPOSAL_LIFETIME_SEC; ///< maximum lifetime in seconds for proposed transactions to be kept, before expiring
       uint8_t                 maximum_asset_whitelist_authorities = GRAPHENE_DEFAULT_MAX_ASSET_WHITELIST_AUTHORITIES; ///< maximum number of accounts which an asset may list as authorities for its whitelist OR blacklist
       uint8_t                 maximum_asset_feed_publishers       = GRAPHENE_DEFAULT_MAX_ASSET_FEED_PUBLISHERS; ///< the maximum number of feed publishers for a given asset
       uint16_t                maximum_witness_count               = GRAPHENE_DEFAULT_MAX_WITNESSES; ///< maximum number of active witnesses
       uint16_t                maximum_committee_count             = GRAPHENE_DEFAULT_MAX_COMMITTEE; ///< maximum number of active committee_members
       uint16_t                maximum_authority_membership        = GRAPHENE_DEFAULT_MAX_AUTHORITY_MEMBERSHIP; ///< largest number of keys/accounts an authority can have
       uint16_t                reserve_percent_of_fee              = GRAPHENE_DEFAULT_BURN_PERCENT_OF_FEE; ///< the percentage of the network's allocation of a fee that is taken out of circulation
       uint16_t                network_percent_of_fee              = GRAPHENE_DEFAULT_NETWORK_PERCENT_OF_FEE; ///< percent of transaction fees paid to network
       uint16_t                lifetime_referrer_percent_of_fee    = GRAPHENE_DEFAULT_LIFETIME_REFERRER_PERCENT_OF_FEE; ///< percent of transaction fees paid to network
       uint32_t                cashback_vesting_period_seconds     = GRAPHENE_DEFAULT_CASHBACK_VESTING_PERIOD_SEC; ///< time after cashback rewards are accrued before they become liquid
       share_type              cashback_vesting_threshold          = GRAPHENE_DEFAULT_CASHBACK_VESTING_THRESHOLD; ///< the maximum cashback that can be received without vesting
       bool                    count_non_member_votes              = true; ///< set to false to restrict voting privlegages to member accounts
       bool                    allow_non_member_whitelists         = false; ///< true if non-member accounts may set whitelists and blacklists; false otherwise
       share_type              witness_pay_per_block               = GRAPHENE_DEFAULT_WITNESS_PAY_PER_BLOCK; ///< CORE to be allocated to witnesses (per block)
       uint32_t                witness_pay_vesting_seconds         = GRAPHENE_DEFAULT_WITNESS_PAY_VESTING_SECONDS; ///< vesting_seconds parameter for witness VBO's
       share_type              worker_budget_per_day               = GRAPHENE_DEFAULT_WORKER_BUDGET_PER_DAY; ///< CORE to be allocated to workers (per day)
       uint16_t                max_predicate_opcode                = GRAPHENE_DEFAULT_MAX_ASSERT_OPCODE; ///< predicate_opcode must be less than this number
       share_type              fee_liquidation_threshold           = GRAPHENE_DEFAULT_FEE_LIQUIDATION_THRESHOLD; ///< value in CORE at which accumulated fees in blockchain-issued market assets should be liquidated
       uint16_t                accounts_per_fee_scale              = GRAPHENE_DEFAULT_ACCOUNTS_PER_FEE_SCALE; ///< number of accounts between fee scalings
       uint8_t                 account_fee_scale_bitshifts         = GRAPHENE_DEFAULT_ACCOUNT_FEE_SCALE_BITSHIFTS; ///< number of times to left bitshift account registration fee at each scaling
       uint8_t                 max_authority_depth                 = GRAPHENE_MAX_SIG_CHECK_DEPTH;
       extensions_type         extensions;
    
       /** defined in fee_schedule.cpp */
       void validate()const;
    };


#### Q. Are there any sharding mechanics currently deployed?

No

#### Q. How are SPV clients handled?

No SPV clients at the moment, each full node can expose a public websocket/http api.

#### Q. How is time addressed in the blockchain? Is NTP used or some other protocol?

NTP

#### Q. How do new clients bootstrap into the network?

Trusted seed nodes. Knowledge of initial witness keys.

#### Q. What is the average block time?

Current 3 seconds, configurable by chain parameters.

#### Q. How is accounting addressed in Bitshares? Is it a Nxt style accounting model or like Bitcoin’s UTXO

Each account has a finite set of balances, one for each asset type.

### Protocol

#### Q. Are there any special affordances made for privacy?

…such as using CoinJoin or a ZK-SNARK based privacy scheme like Zerocash? If mixing is integrated at the protocl level are you using the standards set forth by the BNMCKF Mixcoin proposal

Confidential values (same as blockstream elements using the same secp256k1-zkp lib) + stealth addresses. https://github.com/Ele

#### Q. Does the protocol provide mechanisms for overlay protocols to interact such as OR_RETURN?

Yes, using a custom_operation.

    struct custom_operation : public base_operation
       {
          struct fee_parameters_type {
             uint64_t fee = GRAPHENE_BLOCKCHAIN_PRECISION;
             uint32_t price_per_kbyte = 10;
          };

          asset                     fee;
          account_id_type           payer;
          flat_set<account_id_type> required_auths;
          uint16_t                  id = 0;
          vector<char>              data;

          account_id_type   fee_payer()const { return payer; }
          void              validate()const;
          share_type        calculate_fee(const fee_parameters_type& k)const;
       };

#### Q. Is this done via a gossip protocol or through a federate relay?

Each node immediately broadcast the data it receives to its peers after validating it https://github.com/cryptonomex/graphene/blob/master/libraries/p2p/design.md


### Data Structures

#### Q. What data structures are used in the blockchain?

::
    Blocks => transactions => operations => objects.

The blockchain state is contained in an object database that is affected by the operations. Example objects::

    account_object
    asset_object
    account_balance_object
    ...


    class account_balance_object : public abstract_object<account_balance_object>
       {
          public:
             static const uint8_t space_id = implementation_ids;
             static const uint8_t type_id  = impl_account_balance_object_type;

             account_id_type   owner;
             asset_id_type     asset_type;
             share_type        balance;

             asset get_balance()const { return asset(balance, asset_type); }
             void  adjust_balance(const asset& delta);
       };

### Public key system

#### Q. What public key system is used? If elliptic curve, then what is the curve?

Same as Bitcoin, secp256k1.

### Scripting Language 

#### Q. Is there a specification for Bitshares scripting language? (assuming there is one)

No scripting

#### Q. Is the scripting language turing complete?

No scripting

***
### Accounts

#### Q. How can I create, register and upgrade an account to Lifetime Membership?

Without already having an account, or knowing someone that has an account, it is not possible. You can’t create accounts out of nowhere.

But you can work around it by importing an active key of a **Lifetime Member** account that has funds:

1. In the gui, go to the permissions tab of an account that is funded and has a LTM status.
1. Click on the BTS public key on the ACTIVE tab and copy the private key.
1. In the cli-wallet run: import_key <account_name> <private_key>
1. Then run: suggest_brain_key and copy the brain key. (You might want to make a backup of your brain key somewhere.)
1. Create a new account with this command: create_account_with_brain_key <brainkey> <new_account_name> <imported_name> <imported_name> true

This will create a new account called <new_account_name> and set the registrar and referrer to <imported_name>. The brainkey can be used to regenerate the account (even in the GUI wallet). You can manually delete the other active key from the wallet.json file.

***
### Assets

#### Q. What happens to the asset creation fee?

50% of the asset creation fee are used to pre-fill the assets fee pool. From the other 50%, 20% go to the network and 80% go to the referral program. This means, that if you are a life-time member, you get back 40% of the asset creation fee after the vesting period (currently 90 days).

#### Q.Can I change x after creation of the asset?

The following parameters can be changed after creation:

- Issuer
- UIA-Options:
   - Max Supply
   - Market Fee
   - Permissions (disable only/nor re-enable)
   - Flags (if permissions allow it)
   - Core exchange rate
   - White/Black Listing
   - Description
- MPG-Options:
   - Feed Life Time
   - Minimum Feeds
   - Force Settlement Offset/Delay/Volume

Things that cannot be changes:
- Symbol
- Precision

#### Q. What about Parent and Child assets?

A **parent/child** relation ship for assets can be represented by the name of the symbol, e.g.:

    PARENT.child

can only be created by the issuer of `PARENT` and no one else.

#### Q. Can I changing the issuer?

The current issue of an asset may transfer ownership of the asset to someone else by changing the issuer in the asset’s settings.

#### Q. What is the fee pool all about?

The fee pool allows participants in the network to deal with assets and pay for the transaction fees without the need to hold BTS. Any transaction fee can be paid by paying any asset that has a core exchange rate (i.e. a price) at which the asset can be exchange implicitly into BTS to cover the network fee. If the asset’s fee pool is funded, the fees can be payed in the native UIA instead of BTS.

**Note :** The core exchange rate at which a fee can be exchanged into BTS may differ from the actual market valuation of the asset. A user, thus, may pay a premium or spare funds by paying in BTS.

**Warning :** Make sure your core exchange rate is higher than the lowest ask, otherwise, people will buy your token from the market and drain your fee pool via implicit abitrage.

It is the task of the issuer to keep the fee pool funded and the core exchange rate updated unless he wants the owner of his asset to be required to hold BTS for the fee.

#### Q. What to do if the fee pool is empty?

Open up the issuer’s account, click the assets tab and open up the dialog to change the asset. There will be a fee pool tab that allows you to fund the fee pool and claim the accumulated fees!

#### Q. What is Fee Pool Draining?

If an order is created and paid in a non-BTS asset, the fee is implicitly exchange into BTS to pay the network fee. However, if the order is canceled, 90% of the fee will be returned as BTS. The result is, that if the core exchange rate is lower than the highest bid, people can simply buy your token from the market, and exchange them implicitly with the fee pool by creating and canceling an order. This will deplete the fee pool and leave the issuer with his tokens at a slight loss (depending on the offset of the core exchange rate). For this reason, we recommend to use a core exchange that is slightly higher than the market price of your asset. As a consequence, paying fees in BTS should always be cheaper.

#### Q. What happens if I enable Market fees?

If Market Fees of a UIA are turned on, fees have to be payed for each **market transaction**. This means, that market fees only apply to **filled orders**!

The percentage of market fees that are applied can be defined and changed by the issuer and any fee generated that way will be accumulated for each asset only to be claimed by the issuer.

If the Market Fee is set to 1%, the issuer will earn 1% of market volume as profit. These profits are accumulated for each UIA and can be withdrawn by the issuer.

#### Q. How to claim accumulated fees?

Open up the issuer’s account, click the assets tab and open up the dialog to change the asset. There will be a fee pool tab that allows you to fund the fee pool and claim the accumulated fees!

#### Q. What if two different market fees are involved in a trade?

Suppose, I set the market fee for MyUIA market at 0.1%. and the market fee for YourUIA market at 0.3%.

In BitShares, You pay the fee upon receiving an asset. Hence, one side will pay 0.3% the other will pay 0.1%.

#### Q. What are Asset Flags and Permissions?

When an asset is creatd, the issuer can set any combination of flags/permissions. Flags are set in stone unless there is permission to edit. Once a permission to edit is revoked, flags are permanent, and can never be modified again.

#### Q. What are the Permissions?

- Enable market fee
- Require holders to be white-listed
- Issuer may transfer asset back to himself
- Issuer must approve all transfers
- Disable confidential transactions

#### Q. What are the Flags?

| flag | |
|---|---|
| charge_market_fee | an issuer-specified percentage of all market trades in this asset is paid to the issuer|
| white_list | accounts must be white-listed in order to hold this asset |
| override_authority | issuer may transfer asset back to himself |
| transfer_restricted | require the issuer to be one party to every transfer |
| disable_force_settle | disable force settling |
| global_settle | (only for bitassets) allows bitasset issuer to force a global settling - this may be set in permissions, but should not be set as flag unless, for instance, a prediction market has to be resolved. If this flag has been enabled, no further shares can be borrowed! |
| disable_confidential | allow the asset to be used with confidential transactions |
| witness_fed_asset | allow the asset to be fed by witnesses |
| committee_fed_asset | allow the asset to be fed by the committee |

#### Q. Can I use the same flags/permissions as for UIAs?

Yes!

#### Q. What are market-pegged-asset-specific parameters?

| parameter| |
|---|---|
| feed_lifetime_sec | The lifetime of a feed. After this time (in seconds) a feed is no longer considered valid. |
| minimum_feeds | The number of feeds required for a market to become (and stay) active. |
| force_settlement_delay_sec | The delay between requesting a settlement and actual execution of settlement (in seconds) |
| force_settlement_offset_percent | A percentage offset from the price feed for settlement (100% = 10000) |
| maximum_force_settlement_volume | Maximum percentage of the supply that can be settled per day (100% = 10000) |
| short_backing_asset | The asset that has to be used to back this asset (when borrowing) |

***
### Testnet

#### Q. Public & private testnet differences What is the difference between public and private testnet?**

Not much. The biggest difference is that public testnet are intended for wider audience and has fixed (not easy to change parameters), while private testnets can be setup with arbitrary settings

***
### Wallet / CLI Wallet
#### Q. How can I close the CLI client in a clean way?

In Windows closing the whole window produces a nasty exception. In Windows you can try ctrl-d which stops the process but stil produces a nasty exception.

#### Q. How can I import to my CLI client a wallet originally created in the web GUI?

CLI and WEB wallet are two separated applications. They use separated ways to represent backups. You can currently only manually import keys from the GUI into the CLI.

#### Q. How can I transfer a single account to a cli wallet?

If you have a need to run just the cli wallet, you will likely want to transfer an existing account from the Web wallet or your light wallet into the cli. This guide assumes that you already have your web wallet working and properly connected to a full node. Something like this:

    ./cli-wallet -s wss://bitshares.openledger.info/ws

You should get a prompt

    new >>>

Now set a password for the wallet

    new >>> set_password my_password
    locked >>> unlock my_password
    unlocked >>>

Now you need to go to your bitshares 2.0 webwallet or lite client and select the account you wish to bring across. Click on permissions followed by the key icon within Active Permissions. This will reveal your private key. Copy it to the clipboard.
development\tutorials\account-active-permissions.png

Now let’s import the account into this wallet

    new >>> import_key <accountname> THISISTHEKEYTHATYOUCOPIED

#### Q. Why does the CLI client crash immediately when I try to run it for the first time?

The CLI client is unable to run on its own, i.e. without being connected to the witness node (via a web socket connection). So to successfully run the CLI client you need to do this:

- make sure you have this entry uncommented in the witness_node_data_dir/config.ini file rpc-endpoint = 127.0.0.1:8090
- before you start the CLI client, you need to start the witness node (and wait a while till it’s up and running)

***
### Witness
#### Q. Change the Signing Key of your Witness?

As a witness you may want to change your key occasionally or on a regular basis. You can do so by calling update_witness:

    >>> update_witness <witness-name> <url> <new-publickey> false

By replacing `false` with `true`, the signed transaction will be broadcast and executed otherwise it will only print the signed transaction for review.

You can get a new public key by calling:

    >>> suggest_brain_key

#### Q. How can I close the witness node in a clean way?
In windows use ctrl-c.

#### Q. How do I check whether the witness node is already synced?

Run the info command in the CLI client and check the head_block_age value.

#### Q. If it seems to be unable to sync beyond a certain date?

You should always make sure you use the newest build available here_ as earlier releases will get stuck due to hard-forks.

#### Q. Is it safe to delete logs stored in witness_node_data_dirlogsp2p?
Yes, but

- they’re rotated automatically after 24 hours anyway
- if you don’t use them you should probably modify config.ini so they aren’t written to disk in the first place.

#### Q. What is the best way to interact with the witness node?
The only way you can interact with the witness node is through the CLI client by using its API. You can also use the GUI (i.e. the light client). In the GUI, change Settings -> API connection, add ws://127.0.0.1:8090/ws (according to settings of your witness node) and select it.

#### Q. What is the meaning of all those different text colors in the witness node console?

| color | |
|---|---|
| green | debug |
| white| info/default |
| yellow/brown| warning |
| red | error |
| blue | some kind of info, I don’t know |

Related source files are in libraries/fc/include/fc/log/ and libraries/fc/src/log/.

#### Q. Whose private key is [“BTS6MRyAjQ..”,”5KQwrPbwdL..”]? Why is it predefined ion the config.ini?

It’s a shared key for some special purpose. But I don’t remember what it is. If I remember BM or someone else has ever explained it in the forum, but I can’t find the post right now. Just let it be there. I think if you comment it out, it will appear again automatically, it’s generated by the code of witness_node.

***
### Worker

***

    












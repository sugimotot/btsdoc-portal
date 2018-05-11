## Private Testnet

### How to setup Private Testnet

#### Contents

1. [Prerequisites](#1-prerequisites)
2. [Creating a Testnet folder](/developers/testnets/private_testnet.md#2-creating-a-testnet-folder)
3. [Creating a Genesis File for a Private Testnet](/developers/testnets/private_testnet.md#3-creating-a-genesis-file-for-a-private-testnet)
4. [Customization of the Genesis File](/developers/testnets/private_testnet.md#4-customization-of-the-genesis-file)
5. [Embedding Genesis (optional)](/developers/testnets/private_testnet.md#5-embedding-genesis-optional)
6. [Creating a Data Directory](/developers/testnets/private_testnet.md#6-creating-a-data-directory)
7. [Setting up Witness Configuration](/developers/testnets/private_testnet.md#7-setting-up-witness-configuration)
8. [Starting Block Production](/developers/testnets/private_testnet.md#8-starting-block-production)
9. [Obtaining the Chain ID](/developers/testnets/private_testnet.md#9-obtaining-the-chain-id)
10. [Creating a new Wallet](/developers/testnets/private_testnet.md#10-creating-a-new-wallet)
11. [Gaining Access to the Genesis Stake](/developers/testnets/private_testnet.md#11-gaining-access-to-the-genesis-stake)
12. [Creating Another Account](/developers/testnets/private_testnet.md#12-creating-another-account)
13. [Creating Committee Members](/developers/testnets/private_testnet.md#13-creating-committee-members)

****

## 1. Prerequisites 

We assume that you have both `witness_node` and `cli_wallet` already compliled (or downloaded from [the offical respository](https://github.com/bitshares/bitshares-2/releases/latest).

## 2. Creating a Testnet Folder

Create a new folder (e.g., `[Testnet-Home]`) in any location you like and copy `witness_node` and `cli_wallet` there. The `[Testnet-Home]` folder will contain all files and folders related to the Testnet.

Open a _Command Prompt_ window and switch the current directory to `[Testnet-Home]`.

## 3. Creating a Genesis File for a Private Testnet

The genesis.json is the initial state of the network. We create a new genesis json file named `my-genesis.json` for a Private Testnet.

    witness_node --create-genesis-json=my-genesis.json

The `my-genesis.json` file will be created in the `[Testnet-Home]` folder. Once this task is done, the witness node will terminate on its own. 

## 4. Customization of the Genesis File

If you want to customize the network's initial state, edit `my-genesis.json`. This allows you to control things such as:

- The accounts that exist at genesis, their names and public keys
- Assets and their initial distribution (including core asset)
- The initial values of chain parameters
- The account / signing keys of the `init` witnesses (or in fact any account at all).

#### Default Genesis
The graphene code base has a default genesis block integrated that has all witnesses, committee members and funds and a single account called `nathan` available from a single private key:

    5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

## 5. Embedding Genesis (optional)

Once you have `genesis.json`, you may set a cmake variable like so:

    cmake -DGRAPHENE_EGENESIS_JSON="$(pwd)/genesis/my-genesis.json"

and then rebuild. Note, sometimes I've had to clean the build and CMake cache variables in order for `GRAPHENE_EGENESIS_JSON` to take effect:

    make clean
    find . -name "CMakeCache.txt" | xargs rm -f
    find . -name "CMakeFiles" | xargs rm -Rf
    cmake -DGRAPHENE_EGENESIS_JSON="$(pwd)/genesis/my-genesis.json" .

Deleting caches will reset all `cmake` variables, so if you have used instructions like build-ubuntu which tells you to set other `cmake` variables, you will have to add those variables to the `cmake` line above.

Embedding the genesis copies the entire content of genesis.json into the witness_node binary, and additionally copies the chain ID into the cli_wallet binary. Embedded genesis allows the following simplifications to the subsequent instructions:

- You do not need to specify the `genesis.json` file on the witness node command line, or in the witness node configuration file.
- You do not need to specify the chain ID on the `cli_wallet` command line when starting a new wallet.

Embedded genesis is a feature designed to make life easier for consumers of pre-compiled binaries, in exchange for slight, optional complication of the process for producing binaries.



## 6. Creating a Data Directory

We create a new data directory for our witness.

    witness_node --data-dir data/my-blockprod --genesis-json genesis/my-genesis.json --seed-nodes "[]"   # or

    witness_node --data-dir=data/my-blockprod --genesis-json=genesis/my-genesis.json --seed-nodes "[]"

The `data/my-blockprod` directory does not exist, it will be created by the witness node.

> Note: `seed-nodes = []` creates a list of empty seed nodes to avoid connecting to default hardcoded seeds.  
    
The below message means the initialization is complete. It will complete nearly instantaneously with the tiny example genesis, unless you added a ton of balances. Use `ctrl-c` to close the witness node. 

    3501235ms th_a main.cpp:165 main] Started witness node on a chain with 0 blocks.
    3501235ms th_a main.cpp:166 main] Chain ID is cf307110d029cb882d126bf0488dc4864772f68d9888d86b458d16e6c36aa74b

As a result, you should get two items:

- A directory named `data/my-blockprod` has been created (initialized) with a file named `config.ini` located in it.
- The chain ID is now known - it’s displayed in the message above (i.g., Chain ID).


## 7. Setting up Witness Configuration

Open the `[Testnet-Home]/data/my-blockprod/config.ini` file and set the following settings, uncommenting them if necessary.

    rpc-endpoint = 127.0.0.1:8090
    
    p2p-endpoint = 127.0.0.1:11010
    rpc-endpoint = 127.0.0.1:11011
    
    genesis-json = my-genesis.json
    enable-stale-production = true

    private-key = ["GPH6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV","5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"]

    witness-id = "1.6.1"
    witness-id = "1.6.2"
    witness-id = "1.6.3"
    witness-id = "1.6.4"
    witness-id = "1.6.5"
    witness-id = "1.6.6"
    witness-id = "1.6.7"
    witness-id = "1.6.8"
    witness-id = "1.6.9"
    witness-id = "1.6.10"
    witness-id = "1.6.11"

The above list authorizes the `witness_node` to produce blocks on behalf of the listed `witness-id`s and specifies the private key needed to sign those blocks. Normally each witness would be on a different node, but for the purpose of this **private testnet**, we will start out with all witnesses signing blocks on a single node. 

## 8. Starting Block Production

Now run witness_node again:

    witness_node --data-dir data/my-blockprod --enable-stale-production --seed-nodes "[]"

Note:
- We do not need to specify `genesis.json` on the command line, since we now specify it in the config file. 
- The `--enable-stale-production` flag tells the `witness_node` to produce on a chain with zero blocks or very old blocks. We specify the `--enable-stale-production` parameter on the command line as we will not normally need it (although it can also be specified in the config file). 
- The empty `--seed-nodes` is added to avoid connecting to the default seed nodes hardcoded for production.

Subsequent runs which connect to an existing witness node over the p2p network, or which get blockchain state from an existing data directory, need not have the `--enable-stale-production` flag.

## 9. Obtaining the Chain ID

(*see #6.when we created a data directory, we also obtained a chain ID.*)

The chain ID (e.g. blockchain id) is a hash of the genesis state. All transaction signatures are only valid for a single chain ID. So editing the genesis file will change your chain ID, and make you unable to sync with all existing chains (unless one of them has exactly the same genesis file you do).

For testing purposes, the `--dbg-init-key` option will allow you to quickly create a new chain against any genesis file, by replacing the witnesses' block production keys.

Each wallet is specifically associated with a single chain, specified by its chain ID. This is to protect the user from e.g. unintentionally using a testnet wallet on the real chain.

The chain ID is printed at witness node startup. It can also be obtained by using the API to query a running witness node with the `get_chain_properties` API call:

    curl --data '{"jsonrpc": "2.0", "method": "get_chain_properties", "params": [], "id": 1}' http://127.0.0.1:11011/rpc && echo

This curl command will return a short JSON object including the `chain_id`.

## 10. Creating a new Wallet

We are now ready to connect a new wallet to your Private testnet witness node. You must specify a chain ID and server. Keep your witness node running and in another _Command Prompt_ window run this command (a blank username and password will suffice):

    cli_wallet --wallet-file my-wallet.json --chain-id cf307110d029cb882d126bf0488dc4864772f68d9888d86b458d16e6c36aa74b --server-rpc-endpoint ws://127.0.0.1:11011 -u '' -p ''

> Note: Make sure to replace the above blockchain id `cf307110d0...36aa74b` with **your own chain ID** reported by your witness_node. The chain-id passed to the CLI-wallet needs to match the id generated and used by the witness node.

If you get the `set_password` prompt, it means your wallet has successfully connected to the testnet witness node.

Fist you need to create a new password for your wallet. This password is used to encrypt all the private keys in the wallet. For this example, we will use the password `supersecret` .

    >>> set_password supersecret

## 11. Gaining Access to the Genesis Stake

In Graphene, balances are contained in accounts. To import an account that exists in the Graphene genesis into your wallet, all you need to know its name and its private key. We will now import into the wallet an account called `nathan` (a general purpose test account) by using the `import_key` command: 

    unlock supersecret
    import_key nathan "5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"

> Note: `nathan` happens to be the account name defined in the genesis file. If you had edited your `my-genesies.json` file just after it was created, you could have put a different name there. Also, note that `5KQwrPbwdL...P79zkvFD3` is the private key defined in the `config.ini` file.

Now we have the private key imported into the wallet but still no funds assocciated with it. Funds are stored in genesis balance objects. These funds can be claimed, with no fee, using the `import_balance` command.

    import_balance nathan ["5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"] true

As a result, we have one account (named `nathan`) imported into the wallet and this account is well funded with BTS as we have claimed the funds stored in the genesis file. You can view this account information and the balance by using the below commands:

    get_account nathan
    list_account_balances nathan

## 12. Creating Another Account

We will now create another account (named `alpha`) so that we can transfer funds back and forth between `nathan` and `alpha`.

Creating a new account is always done by using an existing account - we need it because someone (i.e. the registrar) has to fund the registration fee. Also, there is the requirement for the registrar account to have a lifetime member (LTM) status. Therefore we need to upgrade the account `nathan` to LTM, before we can proceed with creating other accounts. 

    upgrade_account nathan true
    get_account nathan

In the response, next to `membership_expiration_date` you should see `1969-12-31T23:59:59`. If you get `1970-01-01T00:00:00` something is wrong and `nathan` has not been successfully upgraded.

We can now register an account by using `nathan` as registrar. But first we need to get hold of the public key for the new account. We do it by using the `suggest_brain_key` command.

And the resposne should be something similar to this:

    suggest_brain_key
    {
    "brain_priv_key": "MYAL SOEVER UNSHARP PHYSIC JOURNEY SHEUGH BEDLAM WLOKA FOOLERY GUAYABA DENTILE RADIATE TIEPIN ARMS FOGYISH COQUET",
    "wif_priv_key": "5JDh3XmHK8CDaQSxQZHh5PUV3zwzG68uVcrTfmg9yQ9idNisYnE",
    "pub_key": "BTS78CuY47Vds2nfw2t88ckjTaggPkw16tLhcmg4ReVx1WPr1zRL5"
    }

We can now register an account. The `register_account` command allows you to register an account using only a public key:

    register_account alpha BTS78CuY47Vds2nfw2t88ckjTaggPkw16tLhcmg4ReVx1WPr1zRL5 BTS78CuY47Vds2nfw2t88ckjTaggPkw16tLhcmg4ReVx1WPr1zRL5 nathan nathan 0 true
   
### Transfer funds between accounts

    transfer nathan alpha 100000 CORE "here is the cash" true
    list_account_balances alpha

The text `here is some cash` is an arbitrary memo you can attatch to a transfer. If you don’t need it, just use `"" `instead.
    
We can now open a new wallet for alpha user:

    import_key alpha 5JDh3XmHK8CDaQSxQZHh5PUV3zwzG68uVcrTfmg9yQ9idNisYnE
    upgrade_account alpha true
    create_witness alpha "http://www.alpha" true

The `get_private_key` command allows us to obtain the public key corresponding to the block signing key:

    get_private_key BTS78CuY47Vds2nfw2t88ckjTaggPkw16tLhcmg4ReVx1WPr1zRL5


## 13. Creating Committee Members

    create_account_with_brain_key com0 com0 nathan nathan true
    create_account_with_brain_key com1 com1 nathan nathan true
    create_account_with_brain_key com2 com2 nathan nathan true
    create_account_with_brain_key com3 com3 nathan nathan true
    create_account_with_brain_key com4 com4 nathan nathan true
    create_account_with_brain_key com5 com5 nathan nathan true
    create_account_with_brain_key com6 com6 nathan nathan true
    transfer nathan com0 100000 CORE "some cash" true
    transfer nathan com1 100000 CORE "some cash" true
    transfer nathan com2 100000 CORE "some cash" true
    transfer nathan com3 100000 CORE "some cash" true
    transfer nathan com4 100000 CORE "some cash" true
    transfer nathan com5 100000 CORE "some cash" true
    transfer nathan com6 100000 CORE "some cash" true
    upgrade_account com0 true
    upgrade_account com1 true
    upgrade_account com2 true
    upgrade_account com3 true
    upgrade_account com4 true
    upgrade_account com5 true
    upgrade_account com6 true
    create_committee_member com0 "http://www.com0" true
    create_committee_member com1 "http://www.com1" true
    create_committee_member com2 "http://www.com2" true
    create_committee_member com3 "http://www.com3" true
    create_committee_member com4 "http://www.com4" true
    create_committee_member com5 "http://www.com5" true
    create_committee_member com6 "http://www.com6" true
    vote_for_committee_member nathan com0 true true
    vote_for_committee_member nathan com1 true true
    vote_for_committee_member nathan com2 true true
    vote_for_committee_member nathan com3 true true
    vote_for_committee_member nathan com4 true true
    vote_for_committee_member nathan com5 true true
    vote_for_committee_member nathan com6 true true

    propose_parameter_change com0 {"block_interval" : 6} true




*****

(ref)
- https://github.com/bitshares/bitshares-core/wiki/private-testnet
- http://docs.bitshares.org/testnet/private-testnet.html




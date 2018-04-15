## Private Testnet

### How to setup Private Testnet

### Contents

1. [Prerequisites](#1-prerequisites)
2. [Folder Structure](#2-folder-structure)
3. [The Genesis Files](#3-the-genesis-file)
4. [Get the Blockchain ID](#4-get-the-blockchain-id)
5. [Witness Configuration](#5-witness-configuration)
6. [Start Block Production](#6-start-block-production)
7. [Connecting a CLI wallet](#7-connecting-a-cli-wallet)

****

## 1. Prerequisites 

We assume that you have both `witness_node` and `cli_wallet` already compliled.

## 2. Folder structure 

Create a new folder (e.g., `[Testnet-Home]`) in any location you like and copy `witness_node` and `cli_wallet` there. The `[Testnet-Home]` folder will contain all files and folders related to the Testnet.

Open a _Command Prompt_ window and switch the current directory to `[Testnet-Home]`.

## 3. The Genesis file

The genesis file defines the initial state of the network.

### Default Genesis

The graphene code base has a default genesis block integrated that has all witnesses, committee members and funds and a single account called `nathan` available from a single private key:

    5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

See below how to use this key, or go ahead to learn about how to define your own genesis file

### Creation of the Genesis file

Create a new genesis json file named `my-genesis.json`:

    programs/witness_node/witness_node --create-genesis-json=my-genesis.json

The `my-genesis.json` file will be created in the `[Testnet-Home]` folder. Once this task is done, the witness node will terminate on its own.

### Customization of the Genesis file

If you want to customize the network’s initial state, edit the newly created my-genesis.json file. This allows you to control things such as:

- The accounts that exist at genesis, their names and public keys
- Assets and their initial distribution (including core asset)
- The initial values of chain parameters (including fees)
- The account signing keys of the init witnesses (or in fact any account at all).


## 4. Get the Blockchain ID

The blockchain id (e.g. chain id) is a hash of the genesis state. All transaction signatures are only valid for a single blockchain id. So editing the genesis file will change your blockchain id, and make you unable to sync with all existing chains (unless one of them has exactly the same genesis file you do).

### Creating data directory

**Run commend**

    programs/witness_node/witness_node --data-dir=data   # to use the default genesis, OR
    
    programs/witness_node/witness_node --data-dir=data --genesis-json=my-genesis.json   # your own genesis block

### Obtain Cain ID (blockchain id)

The below message means the initialization is complete. Use `ctrl-c` to close the witness node.

    3501235ms th_a main.cpp:165 main] Started witness node on a chain with 0 blocks.
    3501235ms th_a main.cpp:166 main] Chain ID is 8b7bd36a146a03d0e5d0a971e286098f41230b209d96f92465cd62bd64294824

As a result, you should get two items:

- A directory named `data` has been created with a file named `config.ini` located in it.
- Your blockchain id is now known - it’s displayed in the message above (i.g., Chain ID).

> Note: Your blockchain id will be different than the one used in the above example. Copy this id somewhere as you will be needing it later on.

## 5. Witness Configuration

### config.ini file settings

Open the `[Testnet-Home]/data/config.ini` file and set the following settings, uncommenting them if necessary.

    rpc-endpoint = 127.0.0.1:8090
    genesis-json = my-genesis.json
    enable-stale-production = true

### Add witness-ids

Find the below line in the `config.ini` file:

    # ID of witness controlled by this node (e.g. "1.6.5", quotes are required, may specify multiple times)

… and add the following entries:

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

The above list authorizes the `witness_node` to produce blocks on behalf of the listed `witness-id`s. Normally each witness would be on a different node, but for the purpose of this **private testnet**, we will start out with all witnesses signing blocks on a single node. The private keys for all those witness ids (needed to sign blocks) are already supplied in the `config.ini` file:

    # Tuple of [PublicKey, WIF private key] (may specify multiple times)
    private-key = ["BTS6MRyA...T5GDW5CV","5KQwrPb...tP79zkvFD3"]

### Create empty seed nodes

Create a list of empty seed nodes to avoid connecting to default hardcoded seeds:

    seed-nodes = []

## 6. Start Block Production

This is the crucial moment - you are about to produce the very first blocks of your private blockchain. 

### Run the witness node

    programs/witness_node/witness_node --data-dir=data

and your block production should start at this stage. You should see this big message:

    ********************************
    *                              *
    *   ------- NEW CHAIN ------   *
    *   - Welcome to Graphene! -   *
    *   ------------------------   *
    *                              *
    ********************************

and subsequently further messages indicating the successful creation of blocks:

    2322793ms th_a  main.cpp:176     main    ] Started witness node on a chain with 0 blocks.
    2322794ms th_a  main.cpp:177     main    ] Chain ID is       8b7bd36a146a03d0e5d0a971e286098f41230b209d96f92465cd62bd64294824
    2324613ms th_a  witness.cpp:185  block_production_loo ] Generated block #1 with timestamp 2016-01-21T22:38:40 at time 2016-01-21T22:38:40
    2325604ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2342604ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2343609ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2344604ms th_a  witness.cpp:185  block_production_loo ] Generated block #2 with timestamp 2016-01-21T22:39:00 at time 2016-01-21T22:39:00
    2345605ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2349616ms th_a  witness.cpp:185  block_production_loo ] Generated block #3 with timestamp 2016-01-21T22:39:05 at time 2016-01-21T22:39:05
    2350602ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2353612ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2354605ms th_a  witness.cpp:185  block_production_loo ] Generated block #4 with timestamp 2016-01-21T22:39:10 at time 2016-01-21T22:39:10
    2355609ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived
    2356609ms th_a  witness.cpp:194  block_production_loo ] Not producing block because slot has not yet arrived

## 7. Connecting a CLI wallet

### Obtaining the chain ID

Each wallet is specifically associated with a single chain, specified by its chain ID. This is to protect the user from e.g. unintentionally using a testnet wallet on the real chain.

The chain ID is printed at witness node startup. It can also be obtained by using the API to query a running witness node with the `get_chain_properties` API call.

### Create a new wallet - Private Testnet

We are now ready to connect the CLI-wallet to your Private testnet witness node. You must specify a chain ID and server. Keep your witness node running and in another _Command Prompt_ window run this command:

    programs/cli_wallet/cli_wallet --wallet-file=my-wallet.json --chain-id=8b7bd36a146a03d0e5d0a971e286098f41230b209d96f92465cd62bd64294824 --server-rpc-endpoint=ws://127.0.0.1:8090

> Note: Make sure to replace the above blockchain id `8b7bd36a...4294824` with **your own blockchain id (Chain ID)**. The blockchain id passed to the CLI-wallet needs to match the id generated and used by the witness node.

If you get the `set_password` prompt, it means your CLI-wallet has successfully connected to the testnet witness node.

**Set a new password**

Fist you need to create a new password for your wallet. This password is used to encrypt all the private keys in the wallet. For this example, we will use the password `supersecret` but obviously you are free to come up with your own combination of letters and numbers. Use this command to create the password:

    >>> set_password supersecret

**unlock the wallet**

    >>> unlock supersecret

### Gain access to the genesis stake

In Graphene, balances are contained in accounts. To import an account into your wallet, all you need to know its name and its private key. We will now import into the wallet an account called `nathan` (a general purpose test account) by using the `import_key` command:

    >>> import_key nathan 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

> Note: `nathan` happens to be the account name defined in the genesis file. If you had edited your `my-genesies.json` file just after it was created, you could have put a different name there. Also, note that `5KQwrPbwdL...P79zkvFD3` is the private key defined in the `config.ini` file.

Now we have the private key imported into the wallet but still no funds assocciated with it. Funds are stored in genesis balance objects. These funds can be claimed, with no fee, by using the `import_balance` command:

    >>> import_balance nathan ["5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"] true

As a result, we have one account (named nathan) imported into the wallet and this account is well funded with BTS as we have claimed the funds stored in the genesis file. You can view this account by using this command:

    >>> get_account nathan

and its balance by using this command:

    >>> list_account_balances nathan

### Create another account

We will now create another account (named `alpha`) so that we can transfer funds back and forth between `nathan` and `alpha`.

Creating a new account is always done by using an existing account - we need it because someone (i.e. the registrar) has to fund the registration fee. Also, there is the requirement for the registrar account to have a lifetime member (LTM) status. Therefore we need to upgrade the account `nathan` to LTM, before we can proceed with creating other accounts. To upgrade to LTM, use the `upgrade_account` command:

    >>> upgrade_account nathan true

> Note: Due to a known [caching issue](https://github.com/cryptonomex/graphene/issues/530), you need to _restart_ the CLI-wallet at this stage as otherwise it will not be aware of `nathan` having been upgraded. Stop the CLI-wallet by pressing `ctrl-c` and start it again by using exactly the same command as before, i.e.

    programs/cli_wallet/cli_wallet --wallet-file=my-wallet.json --chain-id=8b7bd36a146a03d0e5d0a971e286098f41230b209d96f92465cd62bd64294824 --server-rpc-endpoint=ws://127.0.0.1:8090

**Verify that `nathan` has now a LTM status**

    >>> get_account nathan

In the response, next to `membership_expiration_date` you should see `1969-12-31T23:59:59`. If you get `1970-01-01T00:00:00` something is wrong and `nathan` has not been successfully upgraded.

We can now register an account by using nathan as registrar.ut first we need to get hold of the public key for the new account. We do it by using the `suggest_brain_key` command.

**example 1** 

Create an account by `create_account_with_brain_key`

    >>> suggest_brain_key
    {
    "brain_priv_key": "MYAL SOEVER UNSHARP PHYSIC JOURNEY SHEUGH BEDLAM WLOKA FOOLERY GUAYABA DENTILE RADIATE TIEPIN ARMS FOGYISH COQUET",
    "wif_priv_key": "5JDh3XmHK8CDaQSxQZHh5PUV3zwzG68uVcrTfmg9yQ9idNisYnE",
    "pub_key": "BTS78CuY47Vds2nfw2t88ckjTaggPkw16tLhcmg4ReVx1WPr1zRL5"
    }

The `create_account_with_brain_key` command allows you to register an account using brain key and will automatically import the corresponding private key.

    >>> create_account_with_brain_key "Brain ... key" <accountname> nathan nathan true


### Transfer funds between accounts

As a final step, we will transfer some money from nathan to alpha. For that we use the transfer command:

    >>> transfer nathan alpha 2000000000 BTS "here is some cash" true

The text `here is some cash` is an arbitrary memo you can attatch to a transfer. If you don’t need it, just use `"" `instead.

And now you can verify that `alpha` has indeed received the money:

    >>> list_account_balances alpha

*****

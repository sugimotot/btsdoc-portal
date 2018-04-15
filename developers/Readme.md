## BitShares Documentation for Developpers

***
***
### Documentation Integration and update Processes
1. Bring _doc.bitshares.org_ information and merge with _BitShares Core Wiki_ information
2. Remove redundant information 
3. Gather spreding a piece of good information 
4. Remove old information
5. Restructure contents & re-grouping
6. Update by current information
7. Update by BitShares Core closed issues tagged  'Documentation'
8. Add new contents
9. Get review
10. Improve & update

_**above processes will go parallel_

***
***

## Contents:

### 1. Environment & Installation 
- Ubuntu Linux
- OS X
- Windows
- [Windows - CLI Tools](/developers/1_installation/1-4_windows_cli_tool.md#contents)
- Q&A
   
### 2.[Tools & References ](/developers/2_references_tools#references--tools)
- [References](/developers/2_tools_rerefemces/references.md#releases)
   - Releases
   - Python Library
   - Github other repositories
   - BirShares GitHub Code | Issues
- [Monitoring Account Deposits: Python](/developers/2_tools_rerefemces/python-monitor.md#monitoring-account-deposits-with-python)
- [Monitoring Balance History: NodeJS](/developers/2_tools_rerefemces/nodejs-monitor.md#monitoring-the-balance-history---nodejs)
- Propose & ideas
     
### 3. Accounts
- [Account](/developers/3_Accounts/accounts.md#contents)
   - Permissions
   - Memberships
   - Authorities
- [Account Registration](/developers/3_Accounts/account_registration.md#contents)
   - Create a brain Key and derive a private/public key pair
   - Create an Account
   - Register an Account

### 4. CLI Wallet
- [OverView](/developers/4_cli_wallet/cli_wallet.md#contents)
- Cli-Tools for Windows (option)
- [Create a Cli Wallet and Open RPC port](/developers/4_cli_wallet/cli_wallet.md#create-a-cli-wallet-and-open-rpc-port)
   - Case 1: Connecting a Cli-Wallet - use the public API node
   - Case 2: Connecting a Cli-Wallet
   - Case 3: Connecting a Cli-Wallet - Public Testnet
- Examples 
   - available commands to the cli-wallet (Wallet APIs) 
   - construct a transaction manually
- Gaining Access to Blockchain
   - Manage Account & import
   - Examples 
      - Send funds from faucet to alpha 
- Network and Wallet Configuration
   - [General](/developers/4_cli_wallet/network_wallet.md#network-setups)
      - Trusted Full Node:
      - Wallet
   - [Secure](/developers/4_cli_wallet/network_wallet.md#secure-network-and-wallet-configuration)
      - Trusted Full Node:
      - Delayed Full Node:
      - Wallet

### 5.1. [Full Nodes (Witness Nodes)](/developers/5_full-witness_nodes/full_nodes.md#type-of-witness-nodes)
- Type of Witness nodes
   - Non-Block producing
   - Block producing
- How to launch the full node
- Enabling Remote Procedure Calls (RPC)

### 5.2. [Become an Active Witness](/developers/5_full-witness_nodes/active_witness.md#contents)
- A Block Producing Witness
   - Requirements
   - Hardware Advice
   - Active Witness Duties
- How to become a Block-Producing Witness
   - Run a local (non block producing) full node
   - Launch a CLI wallet
   - Gain Access to Stake
   - Register a new Witness Object
   - Configuration of the Witness Node
   - Verifying Block Production
   - Backup Server
   - Price Feeds

### 6. APIs
- [APIs two categories](/developers/6_apis/apis-about.md#apis-categories)
   - Blockchain API
   - Wallet API
- API Access Restrictions
- Blockchain Specifications
   - Object and IDs
- Calls
   - Remote Procedure Calls
   - [Websocket Calls & Notifications](https://github.com/cedar-book/btsdoc-portal/blob/master/developers/6_apis/websocket_calls_notifications.md#contents)
- Wallet APIs
- Blockchain APIs   
- Namespaces (**idea needed)
   - Graphene::App
   - Graphene::Chain
   - Graphene::Wallet
### 7. Tutorials

### 8. Testnets
   - [Public Testnet Details](/developers/8_testnets/public_testnet_details.md#the-open-public-testnet-information)
   - [Public Testnet Witness(Full) Nodes (block producing witness nodes) ](/developers/8_testnets/public_testnet.md#how-to-deploy-your-own-public-network)
       - 1.Installation/Configuration of Witness
       - 2.Genesis Configuration
       - 3.Initializing Blockchain
       - 4.Connecting a CLI Wallet
       - 5.Establishing a Committee
       - 6.Web wallet 
       - 7.Setup the Faucet      
       - 8.Setup NGing WebServer 
       - 9.Instillation of Python Library
        - 10.Create MPAs/UIAs
    - [Private Testnet](/developers/8_testnets/public_testnet_details.md#the-open-public-testnet-information)
      - 1.Prerequisites
      - 2.Folder Structure
      - 3.The Genesis Files
      - 4.Get the Blockchain ID
      - 5.Witness Configuration
      - 6.Start Block Production
      - 7.Connecting a CLI wallet

### 9. Use Cases / Examples
   - Exchanges
   - Merchants
   - Traders
   - Create MPAs/UIAs
   - 
   



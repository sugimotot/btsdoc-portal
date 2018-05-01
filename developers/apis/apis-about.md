## API Guide 

### Contents:
- 
- 
- 

***


### APIs Categories

* **Blockchain API** -- It is used to query blockchain data (account, assets, trading history, etc.) Besides data stores in the blockchain itself (blocks, transactions, etc. ..), higher level objects (such as accounts, balances, etc. …) can be retrieved through the full node’s database.
* **Wallet API** -- It interract with thr blockchain to operate 
The wallet (cli-wallet) has your private keys and is required a running full node to connect to the blockchain.  when interacting with the blockchain with new transactions. The wallet does not offer P2P or blockchain capabilities directly.


API Calls
----------

* All API calls are formatted in JSON and return JSON only. 
* The set of available calls depends on whether you connected to a full node (witness_node) or the wallet (CLI-wallet). Both support RPC-JSON.   
* The full node also supports the websocket (statefull) protocol with notifications.
* The full node offers a set of API(s), of which only the database calls are available via RPC. Calls that are restricted by default (i.e. `network_node_api`) or have been restricted by configuration are not accessible via RPC because a statefull protocol (websocket) is required for login.
* The CLI- wallet can open a RPC port so that you can interface your application with it. You have the choices of 
     - websocket RPC via the `-r `parameter, and 
     - HTTP RPC via the `-H` parameter.

Call methods
---------------

* Remote Procedure Calls -- In Graphene, RPC calls are **state-less** and accessible via regular JSON formated RPC-HTTP-calls.
* Websocket Calls -- In Graphene, Websocket calls are **stateful** and accessible via regular JSON formated websocket connection. 


API Access Restrictions
------------------------

Access to some APIs may be **restricted** and requires login with username and passphrase. 
### Network and Wallet Configuration
* General Network and Wallet Configuration
* Secure Network and Wallet Configuration




 

## Blockchain APIs

* Database API
* Account History API
* Crypto API
* Network Broadcast API
* Network Nodes API




Wallet API Calls
--------------------

In order to interact the wallet, you need to run the CLI Wallet. The CLI Wallet has the private keys and signing capabilities.  It *requires* a running full node (*witness node*)  (not necessarily locally) and connects to it. 



Blockchain Objects and their Identifiers
----------------------------------------

In the protocol space, there are raw objects such as, accounts, assets, committee members as well as orders, proposals and balances. The implementation space is used to gain access to higher abstraction layers for instance content of the current database state (these include, current global blockchain properties, dynamic asset data, transaction histories as well as account statistics and budget records).


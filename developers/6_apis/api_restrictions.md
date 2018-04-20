## API Access Restrictions

### Contents:
- Authorization Scheme
   - Example 
- Login In
   - *class* graphene::app::login_api
   
***

We provide several different API's. Each API has its own ID. When running witness_node, initially two API's are available.

- API 0: provides read-only access to the database. (e.g. state-less RPC-calls querying)
- API 1: is used to login and gain access to additional, restricted API's. (e.g. authencitated interaction)

> Note: To access the restricted API-1 we are required to use the websocket connection with callbacks to access API-1

***

## Authorization Scheme

You can restrict API’s to particular users by specifying an `api-access` file in `config.ini` or by using the `--api-access /full/path/to/api-access.json` startup node command. 

#### Example: 
`apiaccess` file which allows user `bytemaster` with password `supersecret` to access *four different API’s*, while allowing any other user to access the *three public API’s* necessary to use the wallet::

    {
       "permission_map" :
       [
          [
             "bytemaster",
             {
                "password_hash_b64" : "9e9GF7ooXVb9k4BoSfNIPTelXeGOZ5DrgOYMj94elaY=",
                "password_salt_b64" : "INDdM6iCi/8=",
                "allowed_apis" : ["database_api", "network_broadcast_api", "history_api", "network_node_api"]
             }
          ],
          [
             "*",
             {
                "password_hash_b64" : "*",
                "password_salt_b64" : "*",
                "allowed_apis" : ["database_api", "network_broadcast_api", "history_api"]
             }
          ]
       ]
    }

- Passwords are stored in `base64` as as salted `sha256` hashes. 
- A simple Python script, `saltpass.py` is avaliable to obtain hash and salt values from a password. 
- A single asterisk `*` may be specified as username or password hash to accept any value.

#### Example: 
With the above configuration, how to call `add_node` from the `network_node` API

    {"id":1, "method":"call", "params":[1,"login",["bytemaster", "supersecret"]]}
    {"id":2, "method":"call", "params":[1,"network_node",[]]}
    {"id":3, "method":"call", "params":[2,"add_node",["127.0.0.1:9090"]]}

> Note: the call to `network_node` is necessary to obtain the correct API identifier for the network API. It is not guaranteed that the network API identifier will always be `2`.

Since the `network_node` API requires login, it is only accessible over the websocket RPC. Our [doxygen](https://bitshares.org/doxygen/) documentation contains the most up-to-date information about APIs.

***

## Login In

The `login_api` class implements the bottom layer of the RPC API. All other APIs must be requested from this API. 

#### *class* `graphene::app::login_api`

| -- | |
|------------------------|-----------------------------------------------------------------|
| Public Functions |  bool `login` (const string &user, const string &password) <br/>  Authenticate to the RPC server.  |
| Return |  True if logged in successfully; false otherwise |
| Note | This must be called prior to requesting other APIs. Other APIs may not be accessible until the client has sucessfully authenticated.  |
| Parameters | - `user`: Username to login with <br/> - `password`: Password to login with | 



| fc::api\<\>  | |
|------------------------|-----------------------------------------------------------------|
| fc::api<block_api> block() const | Retrieve the network block API.  |
| fc::api<network_broadcast_api> network_broadcast() const | Retrieve the network broadcast API.  |
| fc::api<database_api> database() const | Retrieve the database API. |
| fc::api<history_api> history() const | Retrieve the history API. |
| fc::api<network_node_api> network_node() const | Retrieve the network node API. |
| fc::api<crypto_api> crypto() const | Retrieve the cryptography API.  |
| fc::api<asset_api> asset() const | Retrieve the asset API. |
| fc::api<graphene::debug_witness::debug_api> debug() const | Retrieve the debug API (if available)  |
| void enable_api(const string &api_name) | Called to enable an API, not reflected. |


***

(ref)

- https://github.com/bitshares/bitshares-core/wiki/API
- http://docs.bitshares.org/api/access.html


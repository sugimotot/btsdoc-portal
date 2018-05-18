## Remote Procedure Calls

Contents:
- 
- 
- 

***

### Call Format

In Graphene, RPC calls are state-less and accessible via regular JSON formated RPC-HTTP-calls. The correct structure of the JSON call is

    {
     "jsonrpc": "2.0",
     "id": 1
     "method": "get_accounts",
     "params": [["1.2.0", "1.2.1"]],
    }

The `get_accounts` call is available in the Full Node’s `database` API and takes only one argument which is an array of account ids (e.g. ["1.2.0", "1.2.1"]).

#### Example Call with curl

Such as call can be submitted via `curl`:

    curl --data '{"jsonrpc": "2.0", "method": "get_accounts", "params": [["1.2.0", "1.2.1"]], "id": 1}' http://127.0.0.1:8090/rpc

#### Successful Calls

The API will return a properly JSON formated response carrying the same `id` as the request to distinguish subsequent calls.

    {
     "id":1,
     "result":  ..data..
    }

#### Errors

In case of an error, the resulting answer will carry an error attribute and a detailed description:

    {
      "id": 0
      "error": {
        "data": {
          "code": error-code,
          "name": " .. name of exception .."
          "message": " .. message of exception ..",
          "stack": [ .. stack trace .. ],
        },
        "code": 1,
      },
    }


### Remarks

Wallet specific commands, such as `transfer` and market orders, are only available if connecting to `cli_wallet` because only the wallet has the private keys and signing capabilities and some calls will only execute if the wallet is unlocked.

The full node offers a set of API(s), of which only the `database` calls are avaiable via RPC. Calls that are restricted by default (i.e. `network_node_api`) or have been restricted by configuration are not accessible via RPC because a statefull protocol (websocket) is required for login.



***

(ref)

- http://docs.bitshares.org/api/rpc.html





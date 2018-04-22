## Wallet API Calls

### Contents:
- 
- 


***

## General Calls

#### string graphene::wallet::wallet_api::`help()` const
| | |
|---|---|
|  |Returns a list of all commands supported by the wallet API. <br/>This lists each command, along with its arguments and return types. For more detailed help on a single command, use get_help() |
| Return |  a multi-line string suitable for displaying on a terminal |

#### string graphene::wallet::wallet_api::`gethelp(const string &method)` const
| | |
|---|---|
|  | Returns detailed help on a single API command. |
| Return | a multi-line string suitable for displaying on a terminal |
| Parameters | `method`: the name of the API command you want help with |

#### variant graphene::wallet::wallet_api::`info()`
#### variant_object graphene::wallet::wallet_api::`about()` const
| | |
|---|---|
|  | Returns info such as client version, git version of graphene/fc, version of boost, openssl. |
| Return | compile time info and client and dependencies versions |
| Parameters | |

#### void graphene::wallet::wallet_api::network_add_nodes(const vector<string> &nodes)
#### vector<variant> graphene::wallet::wallet_api::network_get_connected_peers()
| | |
|---|---|
|  | |
| Return |  |
| Parameters | |

## Wallet Calls

#### bool graphene::wallet::wallet_api::`is_new()` const
| | |
|---|---|
|  | Checks whether the wallet has just been created and has not yet had a password set. <br/>Calling set_password will transition the wallet to the locked state |
| Return | true if the wallet is new |
| Parameters |- |

#### bool graphene::wallet::wallet_api::`is_locked()` const
| | |
|---|---|
|  | Checks whether the wallet is locked (is unable to use its private keys). <br/> This state can be changed by calling lock() or unlock() |
| Return | true if the wallet is locked |
| Parameters | |


#### void graphene::wallet::wallet_api::`lock()`
| | |
|---|---|
|  | Locks the wallet immediately |
| Return |  |
| Parameters | `password`: the password previously set with set_password() |

#### void graphene::wallet::wallet_api::`unlock(string password)`
| | |
|---|---|
|  | Unlocks the wallet. <br/> The wallet remain unlocked until the lock is called or the program exits. |
| Return |  |
| Parameters | |

#### void graphene::wallet::wallet_api::`set_password(string password)`
| | |
|---|---|
|  | Sets a new password on the wallet. <br/> The wallet must be either ‘new’ or ‘unlocked’ to execute this command |
| Return |  |
| Parameters | |

#### map<public_key_type, string> graphene::wallet::wallet_api::`dump_private_keys()`
| | |
|---|---|
|  | Dumps all private keys owned by the wallet. <br/> The keys are printed in WIF format. You can import these keys into another wallet using import_key() |
| Return | a map containing the private keys, indexed by their public key |
| Parameters | |

#### bool graphene::wallet::wallet_api::`import_key(string account_name_or_id, string wif_key)`
| | |
|---|---|
|  | Imports the private key for an existing account. <br/> The private key must match either an owner key or an active key for the named account.|
| Return | true if the key was imported  |
| Parameters | account_name_or_id: the account owning the key <br/> wif_key: the private key in WIF format|


| | |
|---|---|
|  | |
| Return |  |
| Parameters | |




| | |
|---|---|
|  | |
| Return |  |
| Parameters | |




| | |
|---|---|
|  | |
| Return |  |
| Parameters | |

| | |
|---|---|
|  | |
| Return |  |
| Parameters | |




| | |
|---|---|
|  | |
| Return |  |
| Parameters | |




| | |
|---|---|
|  | |
| Return |  |
| Parameters | |

| | |
|---|---|
|  | |
| Return |  |
| Parameters | |




| | |
|---|---|
|  | |
| Return |  |
| Parameters | |




| | |
|---|---|
|  | |
| Return |  |
| Parameters | |

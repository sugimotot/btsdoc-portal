

API Access Restrictions
==================================

In order to access the unrestricted API-0, we call make use of usual
*stateless* RPC-calls. To access the restricted API-1 we are required to use
the websocket connection with callbacks to access API-1:

* API-0: *state-less* querying
* API-1: *authencitated* interaction

Authorization Scheme
-------------------------

You can restrict API's to particular users by specifying an ``api-access`` file in ``config.ini`` or by using the ``--api-access /full/path/to/api-access.json`` startup node command.  Here is an example ``apiaccess`` file which allows user
``bytemaster`` with password ``supersecret`` to access four different API's, while
allowing any other user to access the three public API's necessary to use the
wallet:::

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

Passwords are stored in ``base64`` as as salted ``sha256`` hashes.  A simple Python
script, ``saltpass.py`` is avaliable to obtain hash and salt values from a
password.  A single asterisk ``*`` may be specified as username or password
hash to accept any value.

With the above configuration, here is an example of how to call ``add_node`` from
the ``network_node`` API:::

    {"id":1, "method":"call", "params":[1,"login",["bytemaster", "supersecret"]]}
    {"id":2, "method":"call", "params":[1,"network_node",[]]}
    {"id":3, "method":"call", "params":[2,"add_node",["127.0.0.1:9090"]]}

Note, the call to ``network_node`` is necessary to obtain the correct API
identifier for the network API.  It is not guaranteed that the network API
identifier will always be ``2``.

Since the ``network_node`` API requires login, it is only accessible over the
websocket RPC. Our `doxygen`_ documentation contains the most up-to-date
information about APIs.

Login In
-------------

.. doxygenclass:: graphene::app::login_api
   :members:

.. _doxygen: http://bitshares.org/doxygen

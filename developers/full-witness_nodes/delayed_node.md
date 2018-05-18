## Delayed Full Node


The delayed full node node will provide us with a `delayed` and several times confirmed and verified blockchain. Even though DPOS is more resistant against forks than most other blockchain consensus schemes, we delay the blockchain here to reduces the risk of forks even more. In the end, the delayed full node is supposed to never enter an invalid fork.

The delayed full node will need the IP address and port of the p2p-endpoint from the trusted full node and the number of blocks that should be delayed. We also need to open the RPC/Websocket port (to the local network!) so that we can interface using RPC-JSON calls.

For our example and for 10 blocks delaye (i.e. 30 seconds for 3 second block intervals), we need:


    ./programs/delayed_node/delayed_node --trusted-node="192.168.0.100:8090" \
                                         --delay-block-count=10 \
                                         --rpc-endpoint="192.168.0.101:8090" \
                                         --seed-nodes "[]"

### Network Setup

For high security Network setup, we provide a `delayed` full node which accepts the parameter trusted-node for an RPC endpoint of a trusted validating node. The trusted-node is a regular full node directly connected to the P2P network that works as a proxy. The delayed node will delay blocks until they are irreversible. Depending on the block interval and the number of witnesses, this may lead to a few minutes of delay.


![Secure Setup](https://github.com/cedar-book/btsdoc-portal/blob/master/source/secure-setup.png)

**The delayed full node should be in the same _local_ network as the trusted full node is in the same network and has internet access.** Hence we will work with the following IPs and open the corresponding RPC ports:

- Trusted Full Node:
   - extern: internet access **required**
   - intern: `192.168.0.100`
   - port: `8090`
- Delayed Full Node:
   - extern: **no** internet access required
   - intern: `192.168.0.101`
   - port: `8090`
- Wallet:
   - extern: **no** internet access required
   - intern: `192.168.0.102`
   - port: `8092`

### Trusted Full Node
For the trusted full node, the default settings can be used. For later, we will need to open the RPC port and listen to an IP address to connect the delayed full node to.

    /programs/witness_node/witness_node --rpc-endpoint="192.168.0.100:8090"
 
> Note: A _witness_ node is identical to a full node if no authorized block-signing private key is provided.

### Delayed Full Node
The delayed full node will need the IP address and port of the p2p-endpoint from the trusted full node and the number of blocks that should be delayed. We also need to open the RPC/Websocket port (to the local network!) so that we can interface using RPC-JSON calls.

For our example and for 10 blocks delaye (i.e. 30 seconds for 3 second block intervals), we need:

    /programs/delayed_node/delayed_node --trusted-node="192.168.0.100:8090" \
                                     --rpc-endpoint="192.168.0.101:8090"
                                     -d delayed_node \
                                     -s "0.0.0.0:0" \
                                     --p2p-endpoint="0.0.0.0:0" \
                                     --seed-nodes "[]"

We could now connect via RPC:

- `192.168.0.100:8090` : The trusted full node exposed to the internet
- `192.168.0.101:8090` : The delayed full node not exposed to the internet

> Note: For security reasons, an exchange should only interface with the delayed full node.

For obvious reasons, the trusted full node is should be running before attempting to start the delayed full node.

**For customer deposits, we will interface to the delayed node’s API using 192.168.0.101:8090.**


## Delayed Full Node


The delayed full node node will provide us with a `delayed` and several times confirmed and verified blockchain. Even though DPOS is more resistant against forks than most other blockchain consensus schemes, we delay the blockchain here to reduces the risk of forks even more. In the end, the delayed full node is supposed to never enter an invalid fork.

The delayed full node will need the IP address and port of the p2p-endpoint from the trusted full node and the number of blocks that should be delayed. We also need to open the RPC/Websocket port (to the local network!) so that we can interface using RPC-JSON calls.

For our example and for 10 blocks delaye (i.e. 30 seconds for 3 second block intervals), we need:


    ./programs/delayed_node/delayed_node --trusted-node="192.168.0.100:8090" \
                                         --delay-block-count=10 \
                                         --rpc-endpoint="192.168.0.101:8090" \
                                         --seed-nodes "[]"

### Setup

For high security Network setup, we provide a `delayed` full node which accepts the parameter trusted-node for an RPC endpoint of a trusted validating node. The trusted-node is a regular full node directly connected to the P2P network that works as a proxy. The delayed node will delay blocks until they are irreversible. Depending on the block interval and the number of witnesses, this may lead to a few minutes of delay.

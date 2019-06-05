# Messaging In Node Network

To broadcast a seal message efficiently and quickly, ISAAC+ uses the different broadcasting stretegies by *Group*, *Active Suffrage Group* and *Suffrage Group*. In *Active Suffrage Group* to make the consensus process to be fast, each node in *Active Suffrage Group* transfers it's seals directly to the other nodes in *Active Suffrage Group*. Despite *Active Suffrage Group*, basically within *Suffrage Group* uses *gossip* protocol to spread seals. 

* The *seal* will be broadcasted between *Active Suffrage Group* directly to each others.
* The *seal* from *Active Suffrage Group* will be spreaded by *gossip* protocol.

The matter is,

* The node in *Suffrage Group*, but not *Active Suffrage Group*.
* This node can be *Active Suffrage Group* in the next block.
* This node should catch up the active consensus as fast as it can.

Without hesitation or delay for storing next block, the round for next block will have some interval, it will help the nodes in *Suffrage Group* to store the block.

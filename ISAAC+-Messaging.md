# Messaging In Node Network

To broadcast a seal message efficiently and quickly, ISAAC+ uses the different broadcasting stretegies by *Group*, *Validator Group* and *Consensus Group*. In *Validator Group* to make the consensus process to be fast, each node in *Validator Group* transfers it's seals directly to the other nodes in *Validator Group*. Despite *Validator Group*, basically within *Consensus Group* uses *gossip* protocol to spread seals. 

* The *seal* will be broadcasted between *Validator Group* directly to each others.
* The *seal* from *Validator Group* will be spreaded by *gossip* protocol.

The matter is,

* The node in *Consensus Group*, but not *Validator Group*.
* This node can be *Validator Group* in the next block.
* This node should catch up the active consensus as fast as it can.

Without hesitation or delay for storing next block, the round for next block will have some interval, it will help the nodes in *Consensus Group* to store the block.

# Messaging In Node Network

To broadcast a seal message efficiently and quickly, ISAAC+ uses the different broadcasting stretegies by *Group*, *Acting Suffrage Group* and *Suffrage Group*. In *Acting Suffrage Group* to make the consensus process to be fast, each node in *Acting Suffrage Group* transfers it's seals directly to the other nodes in *Acting Suffrage Group*. Despite *Acting Suffrage Group*, basically within *Suffrage Group* uses *gossip* protocol to spread seals. 

* The *seal* will be broadcasted between *Acting Suffrage Group* directly to each others.
* The *seal* from *Acting Suffrage Group* will be spreaded by *gossip* protocol.

The matter is,

* The node in *Suffrage Group*, but not *Acting Suffrage Group*.
* This node can be *Acting Suffrage Group* in the next block.
* This node should catch up the acting consensus as fast as it can.

Without hesitation or delay for storing next block, the round for next block will have some interval, it will help the nodes in *Suffrage Group* to store the block.

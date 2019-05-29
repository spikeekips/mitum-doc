# PBFT: Practical Byzantine Faulty Tolerance

## Practical Byzantine Fault Tolerance

[Practical Byzantine Fault Tolerance](http://pmg.csail.mit.edu/papers/osdi99.pdf)

## Safety, Liveness and Fault Tolerance

> Definition (safety). A set of nodes in an FBAS enjoy safety if no two of them ever externalize different values for the same slot.
>
> Definition (liveness). A node in an FBAS enjoys liveness if it can externalize new values without the participation of any failed (including ill-behaved) nodes.
> 
> \- [The Stellar Consensus Protocol](https://www.stellar.org/papers/stellar-consensus-protocol.pdf)


## Why 3f+1?

3f+1 is the basic principle of BFT. `f` is the number of faulty nodes.

We also imagin `2f+1`. Simplfy the understanding, `f=1`(one faulty node) and `N=3`(total number of nodes). For reaching consensus, at least 2 nodes agree. The faulty node does not vote and the other 2 nodes vote the different states for request; one node says yes and the other says no. Under `2f+1`, the nodes except faulty node can not reach the agreement on request. Any decision can not be majority. Under `3f+1`, without participating faulty nodes, the rest of ndoes can be reached to agreement.

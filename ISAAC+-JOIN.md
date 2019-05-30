# *JOIN*ing Node Network

Node starts, it has *BOOTING* state and then, it tries to join node network, *JOIN* state. During joining node network, node checks whether it's current state is identical with the others.

1. Node checks it's last *block* state.
1. Node requests *BlockProof*s to the nodes of Consensus Group.
1. Node chooses the highest and valid *BlockProof*.
1. If the selected *BlockProof* is different(higher or lower) from node's, node tries to sync.
1. If same, node broadcasts *INIT* ballot.

---
***BlockProof*** :

*BlockProof* is usually used for joining node network. It contains several informations,

* Current *block* state: *height* and *hash*
* *Proposal* and *ACCEPTBallot* seals of current *block*(, not their *hash*es)

---

# *SIGN* Stage

In *SIGN* stage, node proposes *Proposal* or wait *Proposal*, and validates it. In details,

1. If node is *Proposer*, it proposes *Proposal*

---
***Proposal*** :

ISAAC+ shares the basic rule of consensus. In evenry round, there are *Proposer* and *Proposer* will propose the list of transactions using *Proposal* seal. *Proposal* should have these informations,

* *Block*: last block state
* *Round*: voting round
* *Transactions*: list of *Transaction*s

---

After *Proposal* recevied, node should do like these jobs,

1. Validates the received *Proposal*
1. Validates the *Transaction*s in *Proposal*
1. Ready to store the next block with *Transactions*

If *Proposal* is not valid, node starts next round with same block. After validation of *Proposal*, node can make the next block and it's *hash*. After validation, node will broadcast *SIGN* ballot with the new *block* *hash*. Node votes and collects *SIGN* ballots. If *SIGN* ballots are reached to agreement, node should go to the next stage, *ACCEPT*. 

*SIGN* ballot has these kind of informations,

* *Proposal*
* *Block*: next *block* state, which is applied *Proposal*

*SIGN* ballot will be validated by,

* Same *Block* is over thesehold


## Manged Senario

### None-Proposer node Waits Proposal, But Does Not

In the given time, node does not receive the *Proposal* from the expected *Proposer*, node will start next round with another *Proposer*.

### Proposer Received, But Invalid

Like failed to receive *Proposal*, node will start next round with another *Proposer*. Basically in ISAAC+, node will start next round if something wrong in voting.

### Transactions In Proposal Is Empty 

No reason to stop consensus.

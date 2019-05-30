# ISAAC+ and Mechanism

## Consensus Protocol

ISAAC+ is based on tranditional PBFT. The basic rules of PBFT are,

* Consensus can be reached through the majority of voting
* Each round(or view) has leader and it propose the next block
* Each node can validate and vote the next block of leader

ISAAC+ is also based these rules and has some additional rules,

* Consensus can be reached through the majority of voting
* Each round has proposer(leader) and it propose propsal(the transactions of next block)
* Each node can validate the proposal and vote the state result of proposal

## Node Network

Node consists the consensus network and node can participate the consensus process, but every node participate. The one of the critical fitfall of PBFT is that PBFT network is that only the small group of nodes can join the consensus for performance reason. To overcome this limitation, ISAAC+ has *Candidate Group* and *Validator Group*.

### *Candidate Group* and *Validator Group*

![Network Groups](./images/network-groups.png "Network Groups in ISAAC+")

*Validator Group* is the group of nodes to vote for new block. There are so many nodes can exist, but only small group of node can be participate the consensus in ISAAC+. *Validator Group* is selected from *Consensus Group* and node in the *Validator Group* can vote for new block.

*Candidate Group* is the set of nodes for ready to be *Validator Group*.

Simply we can put together like this,

* In each round, only the nodes in *Validator Group* can participate the consensus
* `Proposer` is selected from *Validator Group*
* *Validator Group* is changed in each round
* For performance reason, the number of *Validator Group* should be limited

### Joining *Candidate Group*

Every node can join *Candidate Group*, but there are some requirements and steps.

* Node, which want to join the *Candidate Group* should prove itself
    - state of block
    - validation capability
    - it's network stability
    - etc
* Node should vote on `Proposal` in each round and broadcast `SIGN` ballot to the current *Candidate Group* within the given time(before ALL-CONFIRM stage)
* After the given time(at this time, almost 1 month?), node gathers the enough agreement signing from nodes of *Candidate Group* and proposes the entrance request to the network.
* The entrance request is validated by *Validator Group* and if passed, the node can be join *Candidate Group*


## Limitation

* Account can send only one transaction per block
    - Account can not send 2 or more transactions at the same block
* There are some number of transaction for one block


## TODO

* node
    * validator group
    * validators
    * proposer

* at least 67% threshold
* round failed, go to next round
* to start new round, all the validators should agree to INIT ballot
* failed to agree to INIT ballot, round will be initialized to 0

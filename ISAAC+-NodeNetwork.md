# Node Network

There are several role for node in ISAAC+.

* Submittig *Proposal* for next block
* Keeping the state of block
* Validation of *Proposal*, blocks
* Maintaining *Consensus Group* by node of *Consensus Group*

Node consists the node network and node can participate the consensus process, but every node participate. The one of the critical fitfall of PBFT is that PBFT node network is that only the small group of nodes can join the consensus for performance reason. To overcome this limitation, ISAAC+ has *Consensus Group* and *Validator Group*.

## *Consensus Group* and *Validator Group*

![Node Network Groups](./images/network-groups.png "Node Network Groups in ISAAC+")

*Validator Group* is the group of nodes to vote for new block. There are so many nodes can exist, but only small group of node can be participate the consensus in ISAAC+. *Validator Group* is selected from *Consensus Group* and node in the *Validator Group* can vote for new block.

*Consensus Group* is the set of nodes for ready to be *Validator Group*.

Simply we can put together like this,

* In each round, only the nodes in *Validator Group* can participate the consensus
* *Proposer* is selected from *Validator Group*
* *Validator Group* is changed in every round
* Node list of *Validator Group* can be listed by block hash, it's height and some additional factors
* For performance reason, the number of *Validator Group* should be limited
* The node list of *Consensus Group* is stored in the block

## Joining *Consensus Group*

Every node can join *Consensus Group*, but there are some requirements and steps.

* Node, which want to join the *Consensus Group* should prove itself
    - required account data; like enough amount of balance
    - state of block
    - validation capability
        - machine power
        - fast-enough network; network should be fast and under stable environment
    - etc: additional conditions could be made by *Consensus Group*

* Node should vote on the active *Proposal* in each round and can broadcast *SIGN* ballot to the current *Consensus Group* within the given time(before *ALL-CONFIRM* stage)
* After the given time(at this time, almost 1 month?), node gathers the enough agreement signing from nodes of *Consensus Group* and proposes the entrance request to the node network.
* The entrance request is validated by *Validator Group* and if passed, the node can be join *Consensus Group*

## Leaving *Consensus Group*

Node can submit the leaving request to *Consensus Group* and if it correctly signed by node, it will be applied to the block state.

## Exile

Node in *Consensus Group* can be exiled by similar way, voting. If node in *Consensus Group* is judged to be the fauly node, any node in *Consensus Group* can propose the exile request for the faulty node. If passed, the node will be out of *Consensus Group*. If the fauly node want to join again, it should wait for the given time(almost 1 month?).

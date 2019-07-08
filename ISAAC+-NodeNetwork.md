# Node Network

There are several role for node in ISAAC+.

* Submittig *Proposal* for next block
* Keeping the state of block
* Validation of *Proposal*, blocks
* Maintaining *Suffrage Group* by node of *Suffrage Group*

Node consists the node network and node can participate the consensus process, and every node can participate. The one of the critical fitfalls of PBFT is that PBFT node network is that only the small group of nodes can join the consensus for performance reason. To overcome this limitation, ISAAC+ has *Suffrage Group* and *Acting Suffrage Group*.

![Node Network Groups](./images/network-groups.png "Node Network Groups in ISAAC+")

*Acting Suffrage Group* is the group of nodes to vote for new block. There are so many nodes can exist, but only small group of nodes can be participate the consensus in ISAAC+. *Acting Suffrage Group* is selected from *Suffrage Group* and node in the *Acting Suffrage Group* can vote for new block.

*Suffrage Group* is the set of nodes for ready to be *Acting Suffrage Group*.

Simply we can put together like this,

* In each round, only the nodes in *Acting Suffrage Group* can participate the consensus.
* *Proposer* is selected from *Acting Suffrage Group*.
* *Acting Suffrage Group* is selected in every round from *Suffrage Group*.
* Node list of *Acting Suffrage Group* can be listed by block hash, it's height and some additional factors.
* For performance reason, the number of *Acting Suffrage Group* should be limited.
* The node list of *Suffrage Group* is stored in the block.

## Node

In ISAAC+, node can be classified by it's role of consensus.

* *Suffrage Node*
* *Acting Suffrage Node*
* *Proposer Node*
* *Watcher Node*

### Suffrage Node

*Suffrage Node* is the node to be approved to participate consensus voting thru *JOIN* process. The group of *suffrage node*s, we call *Suffrage Group*.

### Acting Suffrage Node

*Acting Suffrage Node* is the node to participate consensus voting in acting voting round. These nodes are selected from *Suffrage Group*. The group of *Acting suffrage node*s, we call *Acting Suffrage Group*.

### Proposer Node

*Proposer Node* proposes the *proposal* of *transaction*s for next block. This node is selected from *acting suffrage group*.

### Watcher Node

Most of nodes in node network are *watcher node*. Simply to say, node, which is not in *acting suffrage group* is *watcher node*. *Watcher node* just keeps watching the consensus process and follows the global block state.

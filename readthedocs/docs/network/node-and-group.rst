============================================================
Node and Group
============================================================

In mitum network, there are several types of nodes by it's role and situations.

Home Node
------------------------------------------------------------

Node owner calls his/her node as home node.

Suffrage Group
------------------------------------------------------------

* Basically this member will keep the network going correctly.
* This member have the right to participate the consensus process.

    * Node, not in suffrage group can not participate the consensus process.
* The new block is established by the agreement of suffrage group.
* This member also have the privilege to vote on the decision for network policies.
* The member of this group is not hard-coded or managed by another system. The member of this group can be decided by the agreement of network.

Acting Suffrage Group
------------------------------------------------------------

* ISAAC+ will open the new round for establishing the next new block. In new round, not all the suffrage group members participate, only the limited members can join.
* In new round, the limited members is selected randomly, this members will be "acting suffrage group members".
* The member of acting suffrage group will be tested and challenged, whether it works correctly without problem by the other suffrage group members.

.. note::
    If some node in acting suffrage group members works weirdly, it may be exiled by network policy.

Proposer
------------------------------------------------------------

* In new round, the new proposer also be selected within acting suffrage members.
* Basically proposer will propose new proposal for next block.

Non-Consensus Node
------------------------------------------------------------

* This node is all the nodes not to belong to the suffrage group.
* This node will keep track of the established blocks from suffrage group.
* If this node proves itself to have enough qualifications for consensus process, this node will be one of the suffrage group.

Faulty Node
------------------------------------------------------------

Faulty node(or failed node) is the failed or malfunctioning node. Node can be faulty node in these cases,

    * Maybe crashed, or
    * has the different states to other nodes, or
    * responses the different acts to other nodes, etc.

Any node can be faulty node, whether it is acting suffrage group, suffrage group or even not in both.

Commonly faulty node is:

    * When it does not respond the request from other nodes
    * When it seems to have the different block state to the nodes

Faulty node in suffrage group is:

    * When it does not serve BlockProof
    * When it serves the invalid BlockProof
    * When it does not serve VotingProof
    * When it serves the invalid VotingProof

Faulty node in acting suffrage group is:

    * When it is proposer and does not broadcast proposal
    * When it does not broadcast ballots
    * When it broadcast the invalid ballot


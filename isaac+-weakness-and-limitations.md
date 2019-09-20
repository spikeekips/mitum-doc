# ISAAC+: Weakness and Limitations

Too obviously ISAAC+ is not perfect as consensus protocol. At this time, ISAAC+ is the practical solution over PBFT. At this section the weaknesses and limitations of ISAAC+ will be introduced.

## One Node Performance ≒  Entire Network Performance

The performance at this point is the ability how much contents can be handled at a time. With ISAAC+, the performance of entire network is almost same with the performance of one node. That is to say, one node can decide the maximum amount of contents for one block. At the worst case, the performance of entire network set to the one of poorest node.

This problem is not native to ISAAC+, most of implementation of PBFT suffers same problem.

To solve this problem, ISAAC+ has the suffrage group. Network designer designs it's network at the first time, the designer will set the several policies for new member for suffrage group like:

* Low network latency
* Enough computing power
* etc.

The new node, who want to join the suffrage group, should satisfy these condition.

We can assume that node was decent, but after joining group, it became weird node, too long to propose new proposal and too long to vote. At this case, the designer also set the rule for exiling faulty node.

## Network Latency is Important

For ISAAC+ working correctly, it requires fast network speed for node. It needs to broadcast voting ballot message to the others fast, because to complete one voting round within the given time.

Network designer can decide how much time node will wait for the expected ballot from others. The more node has enough duration, the network coverage will be wider. With short duration, network will require very low network latency.

## Too many ballot messages between suffrage group

ISAAC+ works by voting and voting is done by ballot messages. All the members of suffrage group should broadcast it's own ballot to the others. The more node participate network, the number of messages will be increased exponentially. 

Usually the size of ballot message is very tiny, but huge messages always will be a big burden in most systems. To reduce the problem, mitum basically rely on the UDP network layer and binary messaging serialization.

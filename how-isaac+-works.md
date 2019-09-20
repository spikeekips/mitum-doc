# ISAAC+, Mechanism

As described at the previous section, the consensus voting is processed thru voting stages, *INIT*, *SIGN* and *ACCEPT*. The node, which can participate in consensus process, set it's state to *Consensus* state. If node is under other state, it means node is not ready for participating consensus process.

## Voting and Round

In ISAAC+, node votes to make agreement with the others. How node can vote? The voting process is simple, just broadcasts Ballot to the entire network and gathers ballots from others.

Every node knows which nodes are in suffrage group and which nodes are in acting suffrage group at this stage and round. The member information does not need to be shared or synced, because it is managed and established at block like other data of block.

Voting occurs by round. For example,

* latest block is `H33`

1. *INIT*: `H34`, `R0`
2. *SIGN*: `H34`, `R0`
    1. Failed to get agreement: *INIT*: `H34`, `R1`
3. *SIGN*: `H34`, `R1`
4. *ACCEPT*: `H34`, `R1`
5. new *INIT*: `H35`, `R0`

Like the example, round is unique within new block voting.


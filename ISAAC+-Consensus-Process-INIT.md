# *INIT* Stage

In *INIT* STAGE, NODE TRIES TO START NEXT BLOCK OR NEW ROUND. AFTER *INIT* AGREEMENT BETWEEN NODES, NODE WILL START CONSENSUS FOR NEXT BLOCK OR NEST ROUND.

---
***ROUND***

In isaac+, there is only one voting for same block and same round at the time in entire network. Ff current block is `h33` and node starts consensus for it,

1. Node starts round, `R0` for `H33`.
1. If consensus reached, node starts new round, `R0-H34`, `H34` is newly created block.
1. If consensus failed, node start next round for `R1-H33`.

Node retries consensus by increasing round.

---

Node can broadcast *INIT* ballot in *INIT* stage. Same *block* and *round* reaches agreement, and then goes to *SIGN* stage.

## INIT Ballot

In *INIT* Ballot should have these informations,

* *Block*: last block state, usually *block* *height* will be used
* *Round*: voting round, usually it starts from *0*
* *Proposer*: *Proposer* node of *Block* and *Round*; naturally *Proposer* is one of *Validator Group*

Lime *Proposer*, nodes in *Validator Group* also should be selected by the specific block height and the round.

## Manged Senario

### Ballots Not Received In Given Time

In the given time, node is failed to receive the enough ballots to reach agreement, node will start next round.

### Mangled with different blocks and rounds

`N0` collected these *INIT* ballots,

* `B(N0 INIT H33 R0)`
* `B(N1 INIT H34 R0)`
* `B(N2 INIT H34 R0)`
* `B(N3 INIT H34 R0)`

> `B(N0 INIT H33 R0)` means, *INIT* ballot, which is signed by `N0` for block, `H33` and round, `R0`

Except `N0`, the other nodes can reach agreement for `H33` and `R0`. In this situation, the other nodes except `N0` will continue to *SIGN* and `N0` will accept the agreement for `H34` and `R0`, so `N0` should go into *SYNC*. If `N0` does not move to *SYNC*, it will not participate consensus in the future.


### All nodes has different blocks and rounds

`N0` collected these *INIT* ballots,

* `B(N0 INIT H33 R0)`
* `B(N1 INIT H34 R1)`
* `B(N2 INIT H35 R2)`
* `B(N3 INIT H36 R3)`

In this case, agreement is impossible, we call it, voting result is *DRAW*ed. `N0` and the others also should move to *JOIN* node state and join again to node network.

### All nodes has same blocks, but different rounds

`N0` collected these *INIT* ballots,

* `B(N0 INIT H33 R0)`
* `B(N1 INIT H33 R1)`
* `B(N2 INIT H33 R2)`
* `B(N3 INIT H33 R3)`

In this case, every nodes has it's own round with same block. ISAAC+ will initialize round to `R0`, so every nodes should start new round, `H33` and `R0`.

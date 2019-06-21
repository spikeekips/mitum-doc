# INIT Stage

In *INIT* stage, node tries to start next block or new round. After *init* agreement between *suffrage group*, node will start consensus for next block or next round. Unlike the other stages are based on *active suffrage group*, *INIT* stage is based on *suffrage group*, it means, moving to next block or next round should be agreed between nodes in *suffrage group*.

---
***ROUND*** :

In isaac+, there is only one voting for same block and same round at the time in entire network. If current block is `H33` and node starts consensus for it,

1. Node starts round, `R0` for `H33`.
1. If consensus reached in *suffrage group*, node starts new round, `R0-H34`; `H34` will be the newly created block.
1. If consensus failed, node start next round for `R1-H33`.

Node retries consensus by increasing round.

---

Node can broadcast *INITBallot* in *INIT* stage. Same *block* and *round* reaches agreement within the collected *ballot*s, and then goes to *SIGN* stage.

## Mangled Senario

### Ballots Not Received In Given Time

In the given time, node is failed to receive the enough ballots to reach agreement, node will start next round.

* `N₀` collected these *INITBallot*s,
    * `B(N₀ INIT H33 R0)`
    * `B(N₃ INIT H33 R0)`
* After teh given time, there are no more incoming ballots,
* `N₀` starts the next round, `H33 R1`.

> `B(N₀ INIT H33 R0)` means, *INITBallot*, which is signed by `N₀` for block, `H33` and round, `R0`.

### Mangled with different blocks and rounds

`N₀` collected these *INITBallot*s,

* `B(N₀ INIT H33 R0)`
* `B(N₁ INIT H34 R0)`
* `B(N₂ INIT H34 R0)`
* `B(N₃ INIT H34 R0)`

Except `N₀`, the other nodes can reach agreement for `H34` and `R0`. In this situation, the other nodes except `N₀` will continue to *SIGN* and `N₀` will accept the agreement for `H34` and `R0`, so `N₀` should go into *SYNC*. If `N₀` does not move to *SYNC*, it will not participate consensus in the future.


### All nodes has different blocks and rounds

`N₀` collected these *INITBallot*s,

* `B(N₀ INIT H33 R0)`
* `B(N₁ INIT H34 R1)`
* `B(N₂ INIT H35 R2)`
* `B(N₃ INIT H36 R3)`

In this case, agreement is impossible, we call it, voting result is *DRAW*ed. `N₀` and the others also should move to *JOIN* node state and join again to node network.

### All nodes has same blocks, but different rounds

`N₀` collected these *INITBallot*s,

* `B(N₀ INIT H33 R0)`
* `B(N₁ INIT H33 R1)`
* `B(N₂ INIT H33 R2)`
* `B(N₃ INIT H33 R3)`

In this case, every nodes has it's own round with same block. ISAAC+ will initialize round to `R0`, so every nodes should start new round, `H33` and `R0`.

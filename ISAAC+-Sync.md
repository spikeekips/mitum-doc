# Sync

If node notices the global state is different from node itself, node should try to sync it's block state to global's. In ISAAC+, syncing process is extremely simple. There are some differences in various sync cases, but basically node requests the block state from the other nodes of *Consensus Group*. The node outside *Consensus Group* can not request the block data from *Consensus Group* directly, but the MITUM API server or other services can be used.

Simply the basic process is,

1. Node notices it's block state is different from the global state.
1. Node requests *BlockProof* of the missing block to the other nodes of *Consensus Group*.
1. The recieved *BlockProof* data are valid and then, node tries to join node network again.

## Requesting *BlockProof*

Node should be request from lower block to higher. In fact, the order of block is not important, but blocks are chained by hash as time sequence, so to validate higher block we need the previous blocks. :)

## Completing Catching Up

If node does complete to catch up the latest block state, node can join the consensus. To do it safely, node can wait for incoming agreement of the nodes in *Validator Group*. Node keeps watching the active voting stage and also should be ready to store the active *proposal*. After node verifies the *ACCEPT* agreement, node will join the network.

The detailed process will be like this,

| global state  | `N0`'s state  |
|---------------|---------------|
|  `H105`       | `H33 `        |
|  ...          | ...           |
|  `H110`       | `H105`        |
|  ...          | ...           |
|  `H120`       | `H110`        |
|  ...          | ...           |
|  `H130`       | `H130`        |

* `N0` is one of *Consensus Group*.
* `N0` is trying to sync from `H33` to `H105`.
* `N0` keeps to catch up the global state until the state is same by requesting *BlockProof*.
* `N0` reaches `H130`, this is same state with global.
* `N0` also tries collect the *proposal*, *SIGNBallot*s and *ACCEPTBallot*s for joining again node network.

| global state       | `N0`'s state  |
|--------------------|---------------|
| `H131`(*Proposal*) | `H131`        |
| `H131`(*SIGN*)     | `H131`        |
| `H131`(*ACCEPT*)   | `H131`        |

* After `H131` is finished in global, `N0` also stores `H131`.
* `N0` waits the *INITBallot* for `H131`.
* *INITBallot*s for `H131` reaches agreement, `N0` also waits *proposal* for `H131`.
* `N0` validates the *proposal* and waits the incoming *SIGN* and *ACCEPTBallot*s to reach agreement like other nodes of *Validator Group*.
* Naturally `N0` can finish `H132`(the next block of `H131`) and ready to join again.
* If `N0` is selected as one of *Validator Group*, `N0` starts new round for `H132`.


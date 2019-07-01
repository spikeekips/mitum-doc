# Joining Node Network

Node starts, it has *BOOTING* state and then, it tries to join node network, *JOIN* state. During joining node network, node checks whether it's current state is identical with the others.

1. Node checks it's last *block* state.
1. Node requests *BlockProof*s to the nodes of Suffrage Group.
1. Node chooses the highest and valid *BlockProof*.
1. If the selected *BlockProof* is different(higher or lower) from node's, node tries to sync.
1. If same, starts to join
1. If not, tries *SYNC*

After *SYNC*, node can store the last block, but the other nodes still continues the consensus process for next block.

* joining node: `N₀`
* other working node: `N₁`


| `N₀` | `N₁` | |
| ---- | ----- | ----- |
| `H33` | `H35` |  |
| (requests *BlockProof*) |  |  |
| | (sends *BlockProof* of `H35`)  |  |
| (starts to sync) |  |  |
| | (sends *BlockProof* of `H34`, `H35`)  |  |
| (validates *BlockProof* of `H34` and `H35`) |  |  |
| `H35` | `H36` | `N₁` stored `H36` during syncing |
| (requests last *BlockProof*) |  |  |
| | (sends *BlockProof* of `H36`)  |  |
| `H36` | `H36` | |
| (requests last *BlockProof*) |  |  |
| | (sends *BlockProof* of `H36`)  |  |
| `H36` | `H36` | `N₁` almost finishes the next block `H37` |

* When `N₀` verifies the last block is same with `N₁`, `N₀` collects *INITBallot*s of `H36` for the next block of `H36`.

| `N₀` | `N₁` | |
| ---- | ----- | ----- |
| `H36` | `H36` |  |
|  |  | `INIT(H36)`s are agreed |
| (moves to *JOIN* state) |  | |
| `H36` | `H37` |  |
| (requests last *BlockProof*) |  |  |
| | (sends *BlockProof* of `H37`)  |  |
| (stores `H37`) |  |  |
| (also process *proposal* for `H37`) |  |  |
| (follows voting) |  |  |
| `H38` | `H38` |  |
| (moves to *CONSENSUS* state) |  | |

---
***BlockProof*** :

*BlockProof* is usually used for joining node network. It contains several informations,

* Current *block* state : *height* and *hash*
* *Proposal* and *INITBallot* seals of current *block*(, not their *hash*es)
* block data

---

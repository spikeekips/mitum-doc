# ISAAC+ and Mechanism

## ISAAC+ vs. PBFT

ISAAC+ is based on tranditional PBFT. The basic rules of PBFT are,

* Consensus can be reached through the majority of voting
* Each round(or view) has leader and it propose the next block
* Each node can validate and vote the next block of leader

ISAAC+ is also based these rules and has some additional rules,

* Consensus can be reached through the majority of voting
* Each round has proposer(leader) and it propose propsal(the transactions of next block)
* Each node can validate the proposal and vote the state result of proposal
* If round is failed to get agreement, goes to next round
* To start new round, all the node in *Validator Group* should agree to INIT ballot
* If failed to agree to INIT ballot, next round will be initialized to 0

Like PBFT, the recommended threshold for *Validator Group* is at least 67%.

## Seal

All messages should be signed by sender, even client transaction also should be singed by account owner. MITUM use *Ed25519S* based keypair for signing and it is basically identical with [Stellar keypair](https://godoc.org/github.com/stellar/go/keypair).

The signed message, it is called *Seal*, it holds the message content. In MITUM there are several built-in seals,

### Consensus Related Seals
* *Proposal*: *proposer* will propose the transactions for next *block*
* *Ballot*s: votes for *Proposal* in each *stage*
    - *INITBallot*
    - *SIGNBallot*
    - *ACCEPTBallot*
* *Transaction*

### Block Related Seals

* *BlockProof*: When node tries to join node network and it requests the last blocks and it's proof to the nodes of Consensus Group.

## Limitations

TODO

## Detailed Consensus Mechanism

In the next, the detailed consensus mechanisms will be explained. For simple explanation, we assume the simple node network,

* 4 nodes: one faulty node can be possible(according to `3f+1` rule)
    - `[N₀ N₁ N₂ N₃]`
* All the node is the node of *Consensus Group* and *Validator Group*
    - *Consensus Group*: `[N₀ N₁ N₂ N₃]`
    - *Validator Group*: `[N₀ N₁ N₂ N₃]`
* Every node can receive the transactions from outside of the network
* ~~All the nodes has same block state: `BL0`~~
* Each node is very closely connected with the others: low network latency

<dl>
  <dt>
  
  *Faulty Node*:
  
  </dt>
  <dd>

Faulty node is the failed or non-functioning node to the other nodes. This node,

* Can be crashed,
* Has the different states to other nodes,
* reponses teh different acts to other nodes
  </dd>
</dl>

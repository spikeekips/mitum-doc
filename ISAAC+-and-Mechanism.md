# ISAAC+ and Mechanism

## ISAAC+ vs. PBFT

ISAAC+ is based on tranditional *PBFT*. The basic rules of *PBFT* are,

* Consensus can be reached through the majority of voting
* Each round(or view) has leader and it propose the next block
* Each node can validate and vote the next block of leader

ISAAC+ is also based these rules and has some additional rules,

* Consensus can be reached through the majority of voting
* Each round has proposer(leader) and it propose proposal(the transactions for next block)
* Each node can validate the proposal and vote the state result of proposal
* If active round is failed to get agreement, goes to next round
* To start new round, all the nodes in *Validator Group* should agree to INIT ballot
* If failed to agree to INIT ballot, next round will be initialized to 0

Like *PBFT*, the recommended agreement threshold within *Validator Group* is at least 67%.


### Phases and Stages

Traditionally PBFT has 4 phases, each phase represents how the incoming request from client reaches to the consensus.

1. *Request*
1. *Pre-Prepare*
1. *Prepare*
1. *Commit*

ISAAC and ISAAC+ has also similar 4 phases(in ISAAC+, it is called voting *Stage*),

1. *INIT*
1. *SIGN*
1. *ACCPET*
1. *ALL-CONFIRM*

Each phase does have similar meaning.

* *INIT* : similar to the *Pre-Prepare*, the selected proposer(leader in PBFT) broadcast it's proposal to the network
* *SIGN* : similar to the *Prepare*, each node will validate the proposal
* *ACCEPT* : similar to the *Commit*, if the proposal is passed the SIGN stage, and then each node will store the proposal
* *ALL-CONFIRM* : this stage is not broadcasted, it just internal stage for starting next block.

## ISAAC+

As explained in the brief history of MITUM, MITUM was started from [SEBAK](https://github.com/bosnet/sebak) and ISAAC consensus protocol was developed for SEBAK. The one of the major things which MITUM adopted from SEBAK is ISAAC consensus protocol. In the MITUM, the more advanced and patched version of ISAAC will be used, we call it ISAAC+.

ISAAC+ shares also the limitations of PBFT, but ISAAC+ will fill the hole by the enginerring mechanisms and achieves, *safety* of state and *fault tolerance* in decentralized way.

ISAAC and ISAAC+ share the basic idaes and both of them is based on PBFT(Miguel Castro and Babara Liskov at 1999, [Practical Byzantine Fault Tolerance](http://pmg.csail.mit.edu/papers/osdi99.pdf)). At the first time, ISAAC was based on FBA, but it changed it's way to PBFT. The centralized network shape of FBA(especially [SCP](https://www.stellar.org/papers/stellar-consensus-protocol.pdf)) does not fit to the open and public consensus network.


## Limitations

TODO

## Detailed Consensus Mechanism

In the next, the detailed consensus mechanisms will be explained. For simple explanation, we assume the simple node network,

* 4 nodes : one faulty node can be possible(according to `3f+1` rule)
    - `[N₀ N₁ N₂ N₃]`
* All the nodes is the node of *Consensus Group* and *Validator Group*
    - *Consensus Group* : `[N₀ N₁ N₂ N₃]`
    - *Validator Group* : `[N₀ N₁ N₂ N₃]`
* Every node can receive the transactions from outside of the network
* ~~All the nodes has same block state : `BL0`~~
* Each node is very closely connected with the others : low network latency

---
***Faulty Node*** :

Faulty node is the failed or non-functioning node to the other nodes. This node,

* Can be crashed,
* Has the different states to other nodes,
* reponses teh different acts to other nodes

---

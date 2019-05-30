# MITUM Consensus: ISAAC+

As explained in the brief history of MITUM, MITUM was started from [SEBAK](https://github.com/bosnet/sebak) and ISAAC consensus protocol was developed for SEBAK. The one of the major things which MITUM adopted from SEBAK is ISAAC consensus protocol. In the MITUM, the more advanced and patched version of ISAAC will be used, we call it ISAAC+.

ISAAC+ shares also the limitations of PBFT, but ISAAC+ will fill the hole by the enginerring mechanisms and achieves, *safety* of state and *fault tolerance* in decentralized way.

## ISAAC and ISAAC+

ISAAC and ISAAC+ share the basic idaes and both of them is based on PBFT(Miguel Castro and Babara Liskov at 1999, [Practical Byzantine Fault Tolerance](http://pmg.csail.mit.edu/papers/osdi99.pdf)). At the first time, ISAAC was based on FBA, but it changed it's way to PBFT. The centralized network shape of FBA(especially [SCP](https://www.stellar.org/papers/stellar-consensus-protocol.pdf)) does not fit to the open and public consensus network.

### Phases and Stages

Traditionally PBFT has 4 phases, each phase represents how the incoming request from client reaches to the consensus.

1.*Request*
1.*Pre-Prepare*
1.*Prepare*
1.*Commit*

ISAAC and ISAAC+ has also similar 4 phases(in ISAAC+, it is called voting *Stage*),

1.*INIT*
1.*SIGN*
1.*ACCPET*
1.*ALL-CONFIRM*

Each phase does have similar meaning.

* *INIT* : similar to the *Pre-Prepare*, the selected proposer(leader in PBFT) broadcast it's proposal to the network
* *SIGN* : similar to the *Prepare*, each node will validate the proposal
* *ACCEPT* : similar to the *Commit*, if the proposal is passed the SIGN stage, and then each node will store the proposal
* *ALL-CONFIRM* : this stage is not broadcasted, it just internal stage for starting next block.

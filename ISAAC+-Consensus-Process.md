# Consensus Process in ISAAC+

Like *PBFT*, ISAAC+ has 4 consensus phases, but not like *PBFT* ISAAC+ has different stages.

In ISAAC+, there are 4 consensus stage,

* *INIT*
* *SIGN*
* *ACCEPT*
* *ALL-CONFIRM*

Each stage has it's own ballot.

***Ballot***:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Ballot*, the name explains, is the seal type for voting. It is basic seal for consensus. Each consensus stage has it's own ballot type and informations.

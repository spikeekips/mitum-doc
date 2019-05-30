# Ballot

*Ballot* is the special *seal* for voting.

Each voting state has the unique *ballot* types,

* *INIT*: *INITBallot*
* *SIGN*: *SIGNBallot*
* *ACCEPT*: *ACCEPTBallot*

## Specification

### INITBallot

*INITBallot* should have these informations,

* *Block* : last block state, usually *block* *height* will be used
* *Round* : voting round, usually it starts from *0*
* *Proposer* : *Proposer* node of *Block* and *Round*; naturally *Proposer* is one of *Validator Group*

Like *Proposer*, nodes in *Validator Group* also should be selected by the specific block height and the round.

### SIGNBallot

*SIGNBallot* has these kind of informations,

* *Proposal*
* *Block* : next *block* state, which is applied *Proposal*

### ACCEPTBallot

*ACCEPTBallot* has these kind of informations,

* *Proposal*

================================================================================
Failure Of Proposing
================================================================================

:Under situation:

    * Proposer is selected after INIT stage.
    * Proposer node does not propose the proposal within a given time.
    * Timed out in a given time, each node fails to get the proposal from the proposer.

:Expected actions:

    * Each node tries to move the next round.
    * Each node broadcasts next INIT ballots for next round.

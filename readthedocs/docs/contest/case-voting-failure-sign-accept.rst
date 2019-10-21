================================================================================
Failure Of SIGN, ACCEPT Stages
================================================================================

:Under situation:

    * Suffrage group members should vote for SIGN stage.
    * But some nodes in **acting suffrage group** does not offer the SIGN ballot.
    * Timed out in a given time, each node fails to get enough ballots for SIGN
      stage.

:Expected actions:

    * Each node stops the current vote,
    * Each node broadcasts next INIT ballots for next round.

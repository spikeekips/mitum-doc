================================================================================
Voting Failure: Timeout
================================================================================

INIT Stage
--------------------------------------------------------------------------------

:Under situation:

    * Suffrage group members votes for INIT stage.
    * Some of nodes does not offer the INIT ballot,
    * The number of these nodes is over *blocking number*.
    * Timed out in a given time, each node fails to get enough ballots for INIT stage.

.. note::
    .. glossary::
        *blocking number*

            In voting, to reach a majority for YES, the YES ballots must be over
            threshold. *blocking number* is the minimum number to prevent to reach the majority. For example,

                * there are 4 total voters,
                * threshold for majority is 3,

            At this condition, *blocking number* is 2. Simply to say,

            .. code-block:: none

                blocking number = <voters> - <threshold> + 1


:Expected actions:

    * Each node stops the consensus process and changes it's state to *Joining*.
    * Each node will request *VoteProof* to the others.


Proposing
--------------------------------------------------------------------------------

:Under situation:

    * Proposer is selected after INIT stage.
    * Proposer node does not propose the proposal within a given time.
    * Timed out in a given time, each node fails to get the proposal from the proposer.

:Expected actions:

    * Each node tries to move the next round.
    * Each node broadcasts next INIT ballots for next round.


SIGN, ACCEPT Stages
--------------------------------------------------------------------------------

:Under situation:

    * Suffrage group members votes for SIGN stage.
    * Some of nodes in **acting suffrage group** does not offer the SIGN ballot.
    * Timed out in a given time, each node fails to get enough ballots for SIGN
      stage.

:Expected actions:

    * Each node stops the current vote,
    * Each node broadcasts next INIT ballots for next round.

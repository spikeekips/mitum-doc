================================================================================
Voting Failure: Timeout
================================================================================

Failure Nodes Over Blocking Number At INIT Stage
--------------------------------------------------------------------------------

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


:Under situation:

    * Suffrage group members should vote for INIT stage.
    * But some nodes does not offer the INIT ballot,
    * The number of these nodes is over *blocking number*.
    * Timed out in a given time, each node fails to get enough ballots for INIT stage.

:Expected actions:

    * Each node stops the consensus process and changes its state to *Joining*.
    * :strike:`Each node will request *VoteProof* to the others.`


.. literalinclude:: config/failure-voting-init-over-blocking-number.yml
   :caption: `failure-voting-init-over-blocking-number.yml <https://github.com/spikeekips/mitum-doc/raw/proto2/readthedocs/docs/contest/config/failure-voting-init-over-blocking-number.yml>`_
   :language: yaml
   :linenos:
   :emphasize-lines: 36,37,88

.. code-block:: sh
   :linenos:
   :emphasize-lines: 1,2

    $ ./contest run failure-voting-init-over-blocking-number.yml \
        --log ./contest-failure-voting-init-over-blocking-number
    $ echo $?
    0

This is the filtered majority checking messages:

.. code-block:: sh
   :linenos:
   :emphasize-lines: 27,28

   $ cat ./contest-failure-voting-init-over-blocking-number/n0.log | \
        grep -i 'check majority' | \
        jq -c '[.t, .node, .height, .round, .stage, .total, .threshold, .is_finished, .m]' | \
        column -s ',' -t
   ["11"  0  "INIT"    4  3  false  1     "check majority"]
   ["11"  0  "INIT"    4  3  false  2     "check majority"]
   ["11"  0  "INIT"    4  3  true   3     "check majority"]
   ["11"  0  "SIGN"    4  3  false  1     "check majority"]
   ["11"  0  "SIGN"    4  3  false  2     "check majority"]
   ["11"  0  "SIGN"    4  3  true   3     "check majority"]
   ["11"  0  "SIGN"    4  3  true   null  "check majority    but closed"]
   ["11"  0  "ACCEPT"  4  3  false  1     "check majority"]
   ["11"  0  "ACCEPT"  4  3  false  2     "check majority"]
   ["11"  0  "ACCEPT"  4  3  true   3     "check majority"]
   ["11"  0  "ACCEPT"  4  3  true   null  "check majority    but closed"]
   ["12"  0  "INIT"    4  3  false  1     "check majority"]
   ["12"  0  "INIT"    4  3  false  2     "check majority"]
   ["12"  0  "INIT"    4  3  true   3     "check majority"]
   ["12"  0  "SIGN"    4  3  false  1     "check majority"]
   ["12"  0  "SIGN"    4  3  false  2     "check majority"]
   ["12"  0  "SIGN"    4  3  true   3     "check majority"]
   ["12"  0  "SIGN"    4  3  true   null  "check majority    but closed"]
   ["12"  0  "ACCEPT"  4  3  false  1     "check majority"]
   ["12"  0  "ACCEPT"  4  3  false  2     "check majority"]
   ["12"  0  "ACCEPT"  4  3  true   3     "check majority"]
   ["12"  0  "ACCEPT"  4  3  true   null  "check majority    but closed"]
   ["13"  0  "INIT"    4  3  false  1     "check majority"]
   ["13"  0  "INIT"    4  3  false  2     "check majority"]

This shows the node, ``n0`` checks majority on the incoming ballots. As we expected, the voting was done from the block, ``11`` to ``13``.

Failure Nodes Under Blocking Number At INIT Stage
--------------------------------------------------------------------------------

:Under situation:

    * Suffrage group members should vote for INIT stage.
    * But some nodes does not offer the INIT ballot,
    * The number of these nodes is **under** *blocking number*.

:Expected actions:

    * Consensus does not stop.


.. literalinclude:: config/failure-voting-init-under-blocking-number.yml
   :caption: `failure-voting-init-under-blocking-number.yml <https://github.com/spikeekips/mitum-doc/raw/proto2/readthedocs/docs/contest/config/failure-voting-init-under-blocking-number.yml>`_
   :language: yaml
   :linenos:
   :emphasize-lines: 36,37,105

.. code-block:: sh
   :linenos:
   :emphasize-lines: 1,2

    $ ./contest run failure-voting-init-under-blocking-number.yml \
        --log ./contest-failure-voting-init-under-blocking-number
    $ echo $?
    0

This is the filtered majority checking messages:

.. code-block:: sh
   :linenos:
   :emphasize-lines: 27-29

   $ cat ./contest-failure-voting-init-over-blocking-number/n0.log | \
        grep -i 'check majority' | \
        jq -c '[.height, .round, .stage, .total, .threshold, .is_finished, .m]' | \
        column -s ',' -t
   ["11"  0  "INIT"    4  3  false  "check majority"]
   ["11"  0  "INIT"    4  3  false  "check majority"]
   ["11"  0  "INIT"    4  3  true   "check majority"]
   ["11"  0  "SIGN"    4  3  false  "check majority"]
   ["11"  0  "SIGN"    4  3  false  "check majority"]
   ["11"  0  "SIGN"    4  3  true   "check majority"]
   ["11"  0  "SIGN"    4  3  true   "check majority     but closed"]
   ["11"  0  "ACCEPT"  4  3  false  "check majority"]
   ["11"  0  "ACCEPT"  4  3  false  "check majority"]
   ["11"  0  "ACCEPT"  4  3  true   "check majority"]
   ["11"  0  "ACCEPT"  4  3  true   "check majority     but closed"]
   ["12"  0  "INIT"    4  3  false  "check majority"]
   ["12"  0  "INIT"    4  3  false  "check majority"]
   ["12"  0  "INIT"    4  3  true   "check majority"]
   ["12"  0  "SIGN"    4  3  false  "check majority"]
   ["12"  0  "SIGN"    4  3  false  "check majority"]
   ["12"  0  "SIGN"    4  3  true   "check majority"]
   ["12"  0  "SIGN"    4  3  true   "check majority     but closed"]
   ["12"  0  "ACCEPT"  4  3  false  "check majority"]
   ["12"  0  "ACCEPT"  4  3  false  "check majority"]
   ["12"  0  "ACCEPT"  4  3  true   "check majority"]
   ["12"  0  "ACCEPT"  4  3  true   "check majority     but closed"]
   ["13"  0  "INIT"    4  3  false  "check majority"]
   ["13"  0  "INIT"    4  3  false  "check majority"]
   ["13"  0  "INIT"    4  3  true   "check majority"]
   ["13"  0  "SIGN"    4  3  false  "check majority"]
   ["13"  0  "SIGN"    4  3  false  "check majority"]
   ["13"  0  "SIGN"    4  3  true   "check majority"]
   ["13"  0  "SIGN"    4  3  true   "check majority     but closed"]
   ["13"  0  "ACCEPT"  4  3  false  "check majority"]
   ["13"  0  "ACCEPT"  4  3  false  "check majority"]
   ["13"  0  "ACCEPT"  4  3  true   "check majority"]
   ["13"  0  "ACCEPT"  4  3  true   "check majority     but closed"]
   ["14"  0  "INIT"    4  3  false  "check majority"]
   ["14"  0  "INIT"    4  3  false  "check majority"]
   ["14"  0  "INIT"    4  3  true   "check majority"]

As the result, the consensus process did not stop, ``n0`` stores the next block, ``13``.

Failure Of Proposing
--------------------------------------------------------------------------------

:Under situation:

    * Proposer is selected after INIT stage.
    * Proposer node does not propose the proposal within a given time.
    * Timed out in a given time, each node fails to get the proposal from the proposer.

:Expected actions:

    * Each node tries to move the next round.
    * Each node broadcasts next INIT ballots for next round.


Failure Of SIGN, ACCEPT Stages
--------------------------------------------------------------------------------

:Under situation:

    * Suffrage group members should vote for SIGN stage.
    * But some nodes in **acting suffrage group** does not offer the SIGN ballot.
    * Timed out in a given time, each node fails to get enough ballots for SIGN
      stage.

:Expected actions:

    * Each node stops the current vote,
    * Each node broadcasts next INIT ballots for next round.

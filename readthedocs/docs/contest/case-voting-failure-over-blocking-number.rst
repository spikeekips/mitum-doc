================================================================================
Failure Nodes Over Blocking Number At INIT Stage
================================================================================

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
   :emphasize-lines: 30-32,75

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

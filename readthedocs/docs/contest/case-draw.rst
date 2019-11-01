================================================================================
DRAW: Voting Result Ends in Tie
================================================================================

:Under situation:

    * Suffrage group members should vote for INIT stage.
    * But some nodes does offer the different INIT ballot,
    * The number of these nodes is over *blocking number*.
    * Timed out in a given time, each node fails to get enough ballots for INIT stage.

:Expected actions:

    * Each node stops the current round and tries to start new round.

.. literalinclude:: config/failure-voting-init-draw.yml
   :caption: `failure-voting-init-draw.yml <https://github.com/spikeekips/mitum-doc/raw/proto2/readthedocs/docs/contest/config/failure-voting-init-draw.yml>`_
   :language: yaml
   :linenos:
   :emphasize-lines: 8,10,16,18,27,30,33,39

.. code-block:: sh
   :linenos:
   :emphasize-lines: 1,2

    $ ./contest run failure-voting-init-draw.yml \
        --log ./contest-failure-voting-init-draw
    $ echo $?
    0

This is the filtered majority checking messages:


.. code-block:: sh
   :linenos:
   :emphasize-lines: 11,15,27

   $ cat ./contest-failure-voting-init-draw/n0.log | \
        grep -i 'check majority' | \
        jq -c '[.height, .round, .stage, .total, .threshold, .is_finished, .m]' | \
        column -s ',' -t
    ["12"  0  "ACCEPT"  4  3  false  "NOTYET"    "check majority"]
    ["12"  0  "ACCEPT"  4  3  false  "NOTYET"    "check majority"]
    ["12"  0  "ACCEPT"  4  3  true   "MAJORITY"  "check majority"]
    ["12"  0  "ACCEPT"  4  3  true   null        "check majority     but closed"]
    ["13"  0  "INIT"    4  3  false  "NOTYET"    "check majority"]
    ["13"  0  "INIT"    4  3  false  "NOTYET"    "check majority"]
    ["13"  0  "INIT"    4  3  true   "DRAW"      "check majority"]
    ["13"  0  "INIT"    4  3  true   null        "check majority     but closed"]
    ["12"  1  "INIT"    4  3  false  "NOTYET"    "check majority"]
    ["12"  1  "INIT"    4  3  false  "NOTYET"    "check majority"]
    ["12"  1  "INIT"    4  3  true   "MAJORITY"  "check majority"]
    ["12"  1  "INIT"    4  3  true   null        "check majority     but closed"]
    ["12"  1  "SIGN"    4  3  false  "NOTYET"    "check majority"]
    ["12"  1  "SIGN"    4  3  false  "NOTYET"    "check majority"]
    ["12"  1  "SIGN"    4  3  true   "MAJORITY"  "check majority"]
    ["12"  1  "SIGN"    4  3  true   null        "check majority     but closed"]
    ["12"  1  "ACCEPT"  4  3  false  "NOTYET"    "check majority"]
    ["12"  1  "ACCEPT"  4  3  false  "NOTYET"    "check majority"]
    ["12"  1  "ACCEPT"  4  3  true   "MAJORITY"  "check majority"]
    ["12"  1  "ACCEPT"  4  3  true   null        "check majority     but closed"]
    ["13"  0  "INIT"    4  3  false  "NOTYET"    "check majority"]
    ["13"  0  "INIT"    4  3  false  "NOTYET"    "check majority"]
    ["13"  0  "INIT"    4  3  true   "MAJORITY"  "check majority"]

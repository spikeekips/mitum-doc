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

.. literalinclude:: config/failure-proposing.yml
   :caption: `failure-voting-init-over-blocking-number.yml <https://github.com/spikeekips/mitum-doc/raw/proto2/readthedocs/docs/contest/config/failure-proposing.yml>`_
   :language: yaml
   :linenos:
   :emphasize-lines: 5,13,14,32,33

.. code-block:: sh
   :linenos:

    $ ./contest run failure-proposing.yml --log ./contest-failure-proposing
    $ echo $?
    0

To verify how each node did the consensus process,

.. code-block:: sh
   :linenos:
   :emphasize-lines: 11-36

   $ cat ./contest-failure-voting-init-under-blocking-number/n0.log | \
        grep -i 'check majority' | \
        jq -c '[.height, .round, .stage, .total, .threshold, .is_finished, .m]' | \
        column -s ',' -t
    ["n1"  "12"  0     "ACCEPT"  4     3     false  "check majority"]
    ["n2"  "12"  0     "ACCEPT"  4     3     false  "check majority"]
    ["n3"  "12"  0     "ACCEPT"  4     3     false  "check majority"]
    ["n0"  "12"  0     "ACCEPT"  4     3     false  "check majority"]
    ...
    ["n2"  "12"  0     "ACCEPT"  4     3     true   "check majority but closed"]
    ["n2"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n0"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n1"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n3"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n2"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n0"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n0"  "13"  0     "INIT"    4     3     true   "check majority"]
    ["n1"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n3"  "13"  0     "INIT"    4     3     false  "check majority"]
    ["n3"  "13"  0     "INIT"    4     3     true   "check majority"]
    ["n3"  "13"  0     "INIT"    4     3     true   "check majority but closed"]
    ["n1"  "13"  0     "INIT"    4     3     true   "check majority"]
    ["n2"  "13"  0     "INIT"    4     3     true   "check majority"]
    ["n2"  "13"  0     "INIT"    4     3     true   "check majority but closed"]
    ["n0"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n3"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n2"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n1"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n0"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n3"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n1"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n1"  "13"  1     "INIT"    4     3     true   "check majority"]
    ["n3"  "13"  1     "INIT"    4     3     true   "check majority"]
    ["n2"  "13"  1     "INIT"    4     3     false  "check majority"]
    ["n2"  "13"  1     "INIT"    4     3     true   "check majority"]
    ["n0"  "13"  1     "INIT"    4     3     true   "check majority"]
    ["n3"  "13"  1     "SIGN"    4     3     false  "check majority"]
    ["n1"  "13"  1     "SIGN"    4     3     false  "check majority"]
    ["n3"  "13"  1     "SIGN"    4     3     false  "check majority"]
    ["n0"  "13"  1     "SIGN"    4     3     false  "check majority"]
    ...
    ["n3"  "13"  1     "SIGN"    4     3     true   "check majority"]

The fixed proposer, ``n3`` did not propose the proposal for height, ``13``, round, ``0``, the other nodes moved to the next round, ``11`` for the height, ``13``, and then eventually all the nodes did keep the consensus process.

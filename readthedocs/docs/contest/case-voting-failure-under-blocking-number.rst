================================================================================
Failure Nodes Under Blocking Number At INIT Stage
================================================================================

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
   :emphasize-lines: 8-10,25

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

   $ cat ./contest-failure-voting-init-under-blocking-number/n0.log | \
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

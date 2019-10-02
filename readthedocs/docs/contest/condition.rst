============================================================
Condition
============================================================

``condition`` field can be defined in the top-level of The config file. The sub fields can be defined with condition expressions.

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 8-18
   :caption: sample.yml


    global:
      policy:
          threshold: 67
          interval_broadcast_init_ballot_in_join: 5s
          timeout_wait_vote_result_in_join: 6s
          timeout_wait_ballot: 6s

    condition:
        all:
            node_state:
                - current_state = "booting" AND new_state = "joining"

            new_block:
                - m LIKE "new block created" AND block.height >= 12

        proposer:
            n1:
                - m LIKE "propose new proposal" AND vr.height = 11 AND vr.round = 0 AND vr.stage = "INIT" AND vr.agreement = "MAJORITY"


Basically the section of condition field has these structure:

.. code-block:: yaml

    condition:
        section_name:
            name #0:
                - experssion #0
                - experssion #1

            name #1:
                - experssion #2
                - experssion #3

``all`` section is predefined section, the conditions in ``all`` section, will be applied to all the nodes. For example, the conditions under ``node_state`` should be matched to all nodes. ``new_block`` also too.

.. note::

    For debugging or testing condition expressions, contest command has ``query`` sub-command.

    .. code-block:: sh
       :emphasize-lines: 13

        $ contest query -h
        query logs

        Usage:
          contest query <log> [flags]

        Flags:
          -h, --help                help for query
              --pretty              pretty json output
              --query stringArray   query

        $ contest query /tmp/contest.log \
            --query 'current_state = "booting" AND new_state = "joining"'
        ...
        {
          "level": "info",
          "node": "n1",
          "module": "state-controller",
          "current_state": "booting",
          "new_state": "join",
          "t": "2019-09-30T23:00:09.107501+09:00",
          "caller": "/Users/spikeekips/workspace/mitum/src/isaac/state_controller.go:93",
          "m": "state changed"
        }

        $ echo $?
        0

.. note::

    If ``contest query`` fails to find the matched condition, exit code will be ``1``.


Condition Matching
================================================================================

Condition expression works like SQL *WHERE* clause, almost same. Like SQL, expression can be defined by the SQL rule.

.. code-block:: none

    <column name> <comparison or operators> <value>

In contest, ``<column name>`` of the condition expression is the nested field name of one json log message. For example, to check the highlighted parts,

.. code-block:: json
   :emphasize-lines: 2,18


   {
     "level": "debug",
     "node": "n4",
     "module": "state-controller",
     "seal": {
       "type": "ballot",
       "hash": "sl:2qQNQGcsquu731Z13NtSA1Qtcovgso7atzXYRi6vuxVB",
       "header": {
         "signer": "GCX3QWQFFSOQFBX3TWYHVB62VX7GKRGEN6GTLI3SNVU7OMRSOKCEE3LW:public:stellar",
         "signature": "29cZuExcnZMCWL2xdUhLUbLMAneXcQ5jcCQ6J5YuAuYjqKaQZmEbC5daRPSxLsYsrzdiY2nYadcz2D1LRqk4xKJ4",
         "bodyHash": "ballot:DgMWNQew8tr4XbQw2n4dYy1j9jMGZphvWijhbVEe2yfC",
         "signedAt": "2019-09-30T17:05:58.423751+09:00"
       },
       "body": {
         "hash": "ballot:DgMWNQew8tr4XbQw2n4dYy1j9jMGZphvWijhbVEe2yfC",
         "node": "na:EYdsb4wfdNnup25RL97LBC5HMf8d56C79fTj3R8iKU4C",
         "stage": "INIT",
         "height": "11",
         "round": 0,
         "proposal": "pp:C6Z3RcavkBCWLa5yw6vsMYDugyYqRiL9FJ6JSpkDwLf6",
         "block": "bk:8w2xSGEKqvKL51ne6Wk4Wum8b6UzQustLgzkcAhXHxxE",
         "last_block": "bk:52FK4q8CmpYutvbWmQr4Q7HuY7yrSJZerPG5neE6fDqi",
         "last_round": 11
       }
     },
     "t": "2019-09-30T17:05:58.428867+09:00",
     "caller": "/Users/spikeekips/workspace/mitum/src/isaac/state_controller.go:150",
     "m": "seal received; ballot"
   }

The condition will be,

.. code-block:: none

    level = "debug" AND "body.height = "11"

The interesting expression is ``body.height``. The sub field can be defined as ``.`` connected fields.

In contest, these operators is supported:

.. hlist::
    :columns: 6

    * ``=``
    * ``<``
    * ``>``
    * ``<=``
    * ``>=``
    * ``!=``
    * ``in``
    * ``not in``
    * ``like``
    * ``not like``
    * ``regexp``
    * ``not regexp``

.. seealso::

    The detailed usage of each operator can be found at `Where (SQL) <https://en.wikipedia.org/wiki/Where_(SQL)>`_ .

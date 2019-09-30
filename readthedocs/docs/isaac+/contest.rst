============================================================
Contest: ISAAC+ Consensus Simulator
============================================================

There are huge amount of documentations for various kind of consensus protocol
and also there are lots of implementations for helping to understand it's
mechanism. Contest is the implementation for simulating the detailed mechanism
of ISAAC+.

Contest provides these features:

* All the settings for network can be set by simple configuration file, YAML.
* The size of network can be set.
* New features can be easily added.
* SQL-like expression can be used for checking node state and network.

Brief Introduction
================================================================================

With configuration file, you can build your own test mitum network with the
number of consensus nodes and can run it. The network of contest will produce
the log messages and with it, you can watch how ISAAC+ and mitum works.

For example, this is simple contest configuration file:

.. code-block:: yaml
   :linenos:
   :caption: sample.yml


    condition:
        all:
            node_state:
                - current_state="booting" AND new_state="join"

            new_block:
                - m="new block created" AND block.height>=12

This config will check the 2 conditions on *all* nodes from json **log messages** and if matched log found, the output will be printed. The first condition is,

.. code-block:: sql

    current_state="booting" AND new_state="join"

This expression is from SQL-like, especially it is similar with a part of
*WHERE* expression of SQL. This expression will check if the state of node changes
from ``booting`` to ``join``.

.. code-block:: sql

    m="new block created" AND block.height>=12


This expression will check if the message of log(``m``) is ``new block created``
and it's block height(``block.height``) is over ``12``.

With this config file, contest can be run like this:

.. code-block:: sh
   :linenos:
   :emphasize-lines: 3

    $ ./contest run sample.yml \
        --log ./contest-sample \
        --number-of-nodes 4 \
        --exit-after 10s

The output will be:

.. code-block:: none
   :linenos:

    ...

    query: (and:(node = [n2]), (m = [new block created]), (block.height >= [12]), (block.round = [0]))
    matched log:
    {
      "level": "info",
      "node": "n2",
      "m": "new block created"
    }
    ================================================================================
    query: (and:(node = [n3]), (m = [new block created]), (block.height >= [12]), (block.round = [0]))
    matched log:
    {
      "level": "info",
      "node": "n3",
      "m": "new block created"
    }
    ================================================================================
    query: (and:(node = [n1]), (m = [new block created]), (block.height >= [12]), (block.round = [0]))
    matched log:
    {
      "level": "info",
      "node": "n1",
      "m": "new block created"
    }
    ================================================================================
    query: (and:(node = [n4]), (m = [new block created]), (block.height >= [12]), (block.round = [0]))
    matched log:
    {
      "level": "info",
      "node": "n4",
      "m": "new block created"
    }
    ================================================================================
    query: (and:(node = [n2]), (current_state = [booting]), (new_state = [join]))
    matched log:
    {
      "level": "info",
      "node": "n2",
      "current_state": "booting",
      "new_state": "join",
      "m": "state changed"
    }
    ================================================================================
    query: (and:(node = [n3]), (current_state = [booting]), (new_state = [join]))
    matched log:
    {
      "level": "info",
      "node": "n3",
      "current_state": "booting",
      "new_state": "join",
      "m": "state changed"
    }
    ================================================================================
    query: (and:(node = [n4]), (current_state = [booting]), (new_state = [join]))
    matched log:
    {
      "level": "info",
      "node": "n4",
      "current_state": "booting",
      "new_state": "join",
      "m": "state changed"
    }
    ================================================================================
    query: (and:(node = [n1]), (current_state = [booting]), (new_state = [join]))
    matched log:
    {
      "level": "info",
      "node": "n1",
      "current_state": "booting",
      "new_state": "join",
      "m": "state changed"
    }
    ================================================================================

    ...

    exit 0


The output of command will produce the result of checking conditions with the
matched log messages.

Installation
================================================================================

The detailed instruction about installation is at
`Contest project page <https://github.com/spikeekips/mitum/tree/proto2/contrib/contest>`_.

Usage By Examples
================================================================================

.. note::

    The current contest and mitum is under heavily development and is based on `proto2 <https://github.com/spikeekips/mitum/tree/proto2>`_.


Custom Policy
--------------------------------------------------------------------------------

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 3,4,5

    global:
      policy:
          threshold: 67
          interval_broadcast_init_ballot_in_join: 5s
          timeout_wait_vote_result_in_join: 6s
          timeout_wait_ballot: 6s

    condition:
        all:
            node_state:
                - current_state="booting" and new_state="join"

            new_block:
                - m="new block created" and block.height>=12 and block.round=0

In mitum, there are several factors for policy, these factors can control how mitum and consensus works.:

.. note::

    The default value of each factor will be found at `defaultPolicyConfig <https://github.com/spikeekips/mitum/blob/proto2/contrib/contest/config.go#L319>`_.


``threshold``
    By default, ``threshold`` is ``67`` percent. This means how many node should agree on voting stage. ``67`` percent needs 2/3 of all nodes. If it is ``100``, nodes agree unanimously.

``interval_broadcast_init_ballot_in_join``
    This factor can control how often node will send *INIT* ballot in *join* state. If ``3s``, node will send *INIT* ballot every 3 seconds.

``timeout_wait_vote_result_in_join``
    Node is in *join* state and waits *INIT* ballots from others, but fails to get enough ballots within ``timeout_wait_vote_result_in_join`` time, node will analyze the exact situation of network.

``timeout_wait_ballot``
    In consensus state, node will wait ballots for ``timeout_wait_ballot`` and if fails to get enough ballots within ``timeout_wait_ballot``, node will move to next round.


.. note::

    You can find all the policy factors at `PolicyConfig <https://github.com/spikeekips/mitum/blob/proto2/contrib/contest/config.go#L313-L316>`_ in source.

.. note::

    By default, contest will set the latest *block height* to ``11`` with *round* ``0``.


Run contest:

.. code-block:: sh
   :linenos:
   :caption: custom-policy.yml

    $ ./contest run custom-policy.yml \
        --log ./contest-sample \
        --number-of-nodes 4 \
        --exit-after 10s

If all the condition are matched, contest will exit with exit code, ``0`` with the matched logs.

Condition
================================================================================

``condition`` field can be defined in the top level of The config file. The sub fields can be defined with condition expressions.

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
                - current_state = "booting" AND new_state = "join"

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

``all`` section is pre-defined section, the conditions in ``all`` section, will be applied to all the nodes. For example, the conditions under ``node_state`` should be matched to all nodes. ``new_block`` also too.

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
            --query 'current_state = "booting" AND new_state = "join"'
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
--------------------------------------------------------------------------------

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

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
   :emphasize-lines: 8,9


    blocks:
        - height: 10
          round: 10

    condition:
        all:
            node_state:
                - current_state="booting" AND new_state="join"
                - m="new block created" AND block.height>=12

This config will check the 2 conditions on *all* nodes from log messages and if matched log found, the output will be printed. The first condition is,

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

.. code-block::
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

Usage
================================================================================

...

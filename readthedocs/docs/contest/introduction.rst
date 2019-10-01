================================================================================
Introduction
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



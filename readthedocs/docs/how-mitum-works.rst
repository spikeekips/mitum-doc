============================================================
How mitum Works
============================================================

.. include: common.rst

TL;DR
============================================================

As described in the section, ":doc:`introduction`", the mitum network consists of the multiple consensus nodes.

.. seealso::

    Standalone mode
        For development or research purpose, you can compose the network with only one node. In standalone mode, every operation will be same, even with the consensus process.

As mitum is blockchain, basically mitum network tries to store the incoming data by trusted way. This is simple process for new data.

1. New message is received by one of nodes in the network.
2. New message contains the user data.
3. Message and it's data are validated by the nodes.
4. Each node tries to get the agreement for the new message and it's data.
5. If nodes get agreement to store new data, the new data will be established in the next block.

The important things in the process are,

* The agreement will be done by the consensus protocol, ISAAC+, and the agreement is made by voting with consensus nodes
* All the incoming message is validated by consensus nodes.
* Only agreed data is established(stored) in the block.

This is the normal process of PBFT based blockchain. Mitum follows the classic scenario of PBFT.

Uncompressed Version
============================================================

For detailed explanation, we can assume the simple situation,

* 10 nodes: ``m0``, ``m1``, ``m2``, ``m3``, ``m4``, ``m5``, ``m6``, ``m7``, ``m8``, ``m9``
* suffrage group members: all node
* number of acting suffrage group members: 4 nodes
* Each node can reach others.
* Each node does not share the storage and network with others.
* Nodes, ``m0``, ... , ``m8`` are already working and ``m9`` is just booted.

This example situation will be applied throughout this document.

.. seealso::
    4 nodes is the minimum number of consensus nodes. The detailed mitum network will be described in the section, ":doc:`network/designing-network`".

.. seealso::
    :strike:`The detailed information about the bootstrapping mitum, will be described in the section, ""`

.. seealso::
    About the consensus process, the section, ":doc:`isaac+/isaac+-introduction`".


``m9`` is booted
------------------------------------------------------------

* After ``m9`` are booted, each node will check it's current block state and environment to join the network. At this time, node also tries to check the global network consensus state, which block height and round are  proceeded currently.
* When everything is OK for joining consensus, ``m9`` joins consensus.
* The next consensus voting is for the next block, which has the height, ``H33`` and it's round is ``R0``.

New data message received
------------------------------------------------------------

* ``m9`` got the new data message, ``B1``. It has the data, ``D1``. 
* ``m9`` tries to broadcast ``B1`` to the other consensus nodes.
* The network selects ``m1`` as the new proposer for the next block(``H33`` and ``R0``)
* ``m1`` will propose the new proposal, ``P1`` with ``B1``.
* All the consensus nodes tries to establish ``P1`` for the next block.
* To establish ``m1``'s ``P1``, the majority should be reached for 2 steps.
* When each node receives the new proposal, ``P1`` from the legitimated proposer, it estimates ``P1`` and vote on ``P1``.
* After ``P1`` is passed thru *SIGN* and *ACCEPT* voting stage, ``P1`` will be established in the next block(``H33``, ``R0``)

============================================================
Node State
============================================================

Node in mitum network has 5 different state.

* *Booting*
* *Syncing*
* *Joining*
* *Consensus*
* *Stopped*

The basic life cycle of node state is:

::

    Booting -> Syncing -> Joining -> Consensus -> Stopped

Node decides it's condition and transit it's state. For example:

* Node finds it's block state is different from majority:

::

    Consensus -> Syncing ... -> Joining -> Consensus

* Node is not in suffrage group:

::

    Booting -> Syncing ...

* During Joining state, node finds it's block state is different from majority:

::

    Joining -> Syncing ... -> Joining -> Consensus


States
------------------------------------------------------------

Booting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Node is just deployed and prepare it's resources to join the network.

Syncing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* The newly started node tries to sync it's block state to the latest of network.
* If node can not participate consensus, that means, it is not in suffrage group, it will stay the *Syncing* state for syncing the latest block state.

Joining
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* After node finishes *Syncing*, node tries to join consensus process.
* Node checks the current acting block height and round.
* If acting block height and round is acceptable to node, move to *Consensus* state.

Consensus
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* At this state, node can participate consensus process.

Stopped
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* By any reason  when node is stopping or stopped.


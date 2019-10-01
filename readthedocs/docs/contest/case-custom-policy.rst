============================================================
Custom Policy
============================================================

.. literalinclude:: config/custom-policy.yml
    :caption: `custom-policy.yml <https://github.com/spikeekips/mitum-doc/raw/proto2/readthedocs/docs/contest/config/custom-policy.yml>`_
    :language: yaml
    :linenos:


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

    $ ./contest run custom-policy.yml \
        --log ./contest-sample \
        --number-of-nodes 4 \
        --exit-after 10s

If all the condition are matched, contest will exit with exit code, ``0`` with the matched logs.

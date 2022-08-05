============================================================
Run node: `init`
============================================================

To deploy, mitum needs to be initialized it's database and storage fs. With node
config, ``init`` needs another config, which defines operations for genesis
block, initial network policy and other configurations.


Genesis Config
============================================================

.. literalinclude:: file/genesis-design.yml
   :language: yaml
   :linenos:
   :lines: -15
   :caption: genesis-design.yml

* ``facts`` lists the facts of genesis operations. It's shape is almost
  identical of json output of operation fact.


Facts
------------------------------------------------------------

* ``_hint: suffrage-genesis-join-fact-v0.0.1``

    Defines the initial suffrage nodes


* ``_hint: genesis-network-policy-fact-v0.0.1``

    Defines the initial network policy


``init``
============================================================

  .. code-block:: sh

     $ ./mitum-example init first-node.yml genesis-degign.yml

This will initialize storage and generates genesis block.

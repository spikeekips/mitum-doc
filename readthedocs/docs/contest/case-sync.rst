================================================================================
Sync
================================================================================

:Under situation:

    * But some nodes make different block,
    * The number of these nodes is under *blocking number*.

:Expected actions:

    * These nodes will move to sync state for syncing their block state with network.

.. literalinclude:: config/sync-bad-block.yml
   :caption: `sync-bad-block.yml <https://github.com/spikeekips/mitum-doc/raw/proto2/readthedocs/docs/contest/config/sync-bad-block.yml>`_
   :language: yaml
   :linenos:
   :emphasize-lines: 14,17,28-29,32

.. code-block:: sh
   :linenos:

    $ ./contest run sync-bad-block.yml --log ./contest-sync-bad-block
    $ echo $?
    0

This is the filtered new block messages:


.. code-block:: sh
   :linenos:
   :emphasize-lines: 17-

   $ cat ./contest-sync-bad-block/all.log | \
        grep -i 'new block created' | \
        jq -c '[.node, .block.height, .block.round, .block.hash.hash]' | \
        column -s ',' -t
    ["n0",10,0,"bk:8rZSbCCNeEh1e6cecsfWa6Zx6ZuxbhhriEp8gGtsU5qQ"]
    ["n1",10,0,"bk:8rZSbCCNeEh1e6cecsfWa6Zx6ZuxbhhriEp8gGtsU5qQ"]
    ["n2",10,0,"bk:8rZSbCCNeEh1e6cecsfWa6Zx6ZuxbhhriEp8gGtsU5qQ"]
    ["n3",10,0,"bk:8rZSbCCNeEh1e6cecsfWa6Zx6ZuxbhhriEp8gGtsU5qQ"]
    ["n0",11,0,"bk:DobUDexxfWjLznXGLEajtDQzGfgQ9yQYg3JxHJkmm1To"]
    ["n1",11,0,"bk:DobUDexxfWjLznXGLEajtDQzGfgQ9yQYg3JxHJkmm1To"]
    ["n2",11,0,"bk:DobUDexxfWjLznXGLEajtDQzGfgQ9yQYg3JxHJkmm1To"]
    ["n3",11,0,"bk:DobUDexxfWjLznXGLEajtDQzGfgQ9yQYg3JxHJkmm1To"]
    ["n0",12,0,"bk:C6JyiHt9q5GPDenoNxPzohCB52XXBZ7BcuwyzPbgpi5P"]
    ["n1",12,0,"bk:C6JyiHt9q5GPDenoNxPzohCB52XXBZ7BcuwyzPbgpi5P"]
    ["n2",12,0,"bk:C6JyiHt9q5GPDenoNxPzohCB52XXBZ7BcuwyzPbgpi5P"]
    ["n3",12,0,"bk:C6JyiHt9q5GPDenoNxPzohCB52XXBZ7BcuwyzPbgpi5P"]
    ["n0",13,0,"bk:4CdvUY1w3jsn1cT1KW1AoGFicBHe3SeQDgzHy4YjjHSr"]
    ["n1",13,0,"bk:4CdvUY1w3jsn1cT1KW1AoGFicBHe3SeQDgzHy4YjjHSr"]
    ["n2",13,0,"bk:4CdvUY1w3jsn1cT1KW1AoGFicBHe3SeQDgzHy4YjjHSr"]
    ["n0",14,0,"bk:AXLi5g43jiyAXiK6G6dpE5uX6wjExWZEMF3ki1CnT7us"]
    ["n1",14,0,"bk:AXLi5g43jiyAXiK6G6dpE5uX6wjExWZEMF3ki1CnT7us"]
    ["n2",14,0,"bk:AXLi5g43jiyAXiK6G6dpE5uX6wjExWZEMF3ki1CnT7us"]
    ["n0",15,0,"bk:ANVfJE2gufoX2yc6ByyaHgMyb5Dbd7tZCszjrbviuyzc"]
    ["n1",15,0,"bk:ANVfJE2gufoX2yc6ByyaHgMyb5Dbd7tZCszjrbviuyzc"]
    ["n2",15,0,"bk:ANVfJE2gufoX2yc6ByyaHgMyb5Dbd7tZCszjrbviuyzc"]

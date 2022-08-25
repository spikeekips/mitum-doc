Command: `import`
============================================================


.. code-block:: sh

    $ ./mitum-example import --help

     Usage: a import <node design> <from directory>
    
     import from block data
    
     Arguments:
       <from directory>    block data directory to import
    
     Flags:
       -h, --help    Show context-sensitive help.
    
     logging
       --log.out="stderr"         log output file: {stdout, stderr, <file>}
       --log.format="terminal"    log format: {json, terminal}
       --log.level=debug          log level: {trace, debug, info, warn, error}
       --[no-]log.force-color     log force color

     design
       --design=./config.yml               design uri; 'file:///config.yml', 'https://a.b.c.d/config.yml'
       --[no-]design.https.tls_insecure    https tls insecure


You can import the existing block data. By default, mitum creates and manges
block data like this;

.. code-block:: sh

   $ find ./no0
    .
    ./data
    ./data/000/000/000/000/000/019/454
    ./data/000/000/000/000/000/019/454/map.json
    ./data/000/000/000/000/000/019/454/voteproofs.ndjson
    ./data/000/000/000/000/000/019/454/proposal.json
    ./data/000/000/000/000/000/000/000
    ./data/000/000/000/000/000/000/000/map.json
    ./data/000/000/000/000/000/000/000/voteproofs.ndjson
    ./data/000/000/000/000/000/000/000/states.ndjson.gz
    ./data/000/000/000/000/000/000/000/operations.ndjson.gz
    ./data/000/000/000/000/000/000/000/proposal.json
    ./data/000/000/000/000/000/000/000/operations_tree.ndjson.gz
    ./data/000/000/000/000/000/000/000/states_tree.ndjson.gz
    ./data/temp
    ./db
    ./db/000277.ldb
    ./db/000281.ldb
    ./info.json

For importing from this block data, set ``./no0/data``.

.. code-block:: sh

    $ ./mitum-example import first-node.yml ./no0/data


Command: `init`
============================================================


.. code-block:: sh

    $ ./mitum-example init --help
     Usage: a init <node design> <genesis design>

     init node

     Arguments:
       <genesis design>    genesis design

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


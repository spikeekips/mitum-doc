Command: `run`
============================================================


.. code-block:: sh

    $ ./mitum-example run --help

     Usage: a run <node design>
   
     run node
   
     Flags:
       -h, --help                      Show context-sensitive help.
   
           --discovery=ConnInfo,...    member discovery
           --hold=HEIGHT-FLAG          hold consensus states
   
     logging
       --log.out="stderr"         log output file: {stdout, stderr, <file>}
       --log.format="terminal"    log format: {json, terminal}
       --log.level=debug          log level: {trace, debug, info, warn, error}
       --[no-]log.force-color     log force color

     design
       --design=./config.yml               design uri; 'file:///config.yml', 'https://a.b.c.d/config.yml'
       --[no-]design.https.tls_insecure    https tls insecure

Flags
------------------------------------------------------------

* ``--discovery``

  *Discovery* flag is used to find the other suffrage nodes through *gossip*
  protocol. With valid *discovery* connection inforamtion, you can connect to
  the other suffrage nodes and vice versa.

  *Discovery* connection information format is,
  ``<host>:<port>[#tls_insecure]``. *host* and *port* should not be omitted. and
  *tls insecure* is optional. If host does not use public signed certificates,
  set ``#tls_insecure``.

  Examples:

  .. hlist::
     :columns: 1

     * ``localhost:4320``: ok
     * ``localhost``: bad
     * ``localhost:4320#tls_insecure``: ok
     * ``1.2.3.4:4320``: ok
     * ``1.2.3.4:4320#tls_insecure``: ok


* ``--hold``

  It is used only for testing. If ``--hold`` is given, node will stop every
  processes and do nothing.

  Examples:

  .. hlist::
     :columns: 1

     * ``--hold``: At start time, node does not do anything
     * ``--hold=10``: After node stores block, *height*, 10, node holds

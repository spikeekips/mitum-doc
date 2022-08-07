Command: `network client`
============================================================


.. code-block:: sh

    $ ./mitum-example network client --help

     Usage: a network client <header> [<remote>]
  
     network client
  
     Arguments:
       <header>      request header; 'example' will print example headers
       [<remote>]    remote node conn info
  
     Flags:
       -h, --help                Show context-sensitive help.
  
           --timeout=duration    timeout
           --body=BODY           body
           --dry-run             don't send
  
     logging
       --log.out="stderr"         log output file: {stdout, stderr, <file>}
       --log.format="terminal"    log format: {json, terminal}
       --log.level=debug          log level: {trace, debug, info, warn, error}
       --[no-]log.force-color     log force color


Arguments
------------------------------------------------------------

* ``header``

  Request header. Currently mitum supports these requests by header.

  .. code-block:: sh

      $ ./mitum-example network client example
       example headers:
       - blockmap: 
           {"_hint":"blockmap-header-v0.0.1","height":33}
       - blockmap_item: 
           {"item":"blockmapitem_operations","height":33,"_hint":"blockmap-item-header-v0.0.1"}
       - exists_instate_operation: 
           {"fact":"9a4vpzrBNpSb18HsMv2sSEASHuCW732az7on5w7RjWbm","_hint":"exists-instate-operation-header-v0.0.1"}
       - last_blockmap: 
           {"manifest":"Fri87d7BMCF7hv6gWwQ6mrQyeBQycW4SBFfS5uLzKRN8","_hint":"last-blockmap-header-v0.0.1"}
       - last_suffrage_proof: 
           {"state":"rLeHwzRPegvRnUBTYpkrsvhTEFLfXie4bHLun9ZXrwK","_hint":"last-suffrage-proof-header-v0.0.1"}
       - node_challenge: 
           {"input":"WFXHRFu1RVWtL64c+Z3z1Q==","_hint":"node-challenge-header-v0.0.1"}
       - node_info: 
           {"_hint":"node-info-header-v0.0.1"}
       - operation: 
           {"operation":"EgvRAnZANRfjxQRSkE7A64m7puz5kh7zq5PEQzDsuxRg","_hint":"operation-header-v0.0.1"}
       - pprof: 
           {"label":"heap","seconds":5,"gc":true,"_hint":"pprof-header-v0.0.1"}
       - proposal: 
           {"proposal":"E7gga4PaWPorzAXMAahkZwcgtwUjjCyJEizqka5cSzdx","_hint":"proposal-header-v0.0.1"}
       - request_proposal: 
           {"_hint":"request-proposal-header-v0.0.1","proposer":"proposersas","point":{"height":33,"round":1}}
       - send_operation: $ cmd <header> --body=<json body>
           {"_hint":"send-operation-header-v0.0.1"}
       - state: 
           {"hash":"676Gug3J4Ugf8YTrNU2nN7mFZKCxwEvJrVhJVQBLNqsZ","key":"suffrage","_hint":"state-header-v0.0.1"}
       - suffrage_node_conninfo: 
           {"_hint":"suffrage-node-conninfo-header-v0.0.1"}
       - suffrage_proof: 
           {"_hint":"suffrage-proof-header-v0.0.1","suffrage_height":44}
       - sync_source_conninfo: 
           {"_hint":"sync-source-conninfo-header-v0.0.1"}
      
       * see isaac/network/header.go

  * For example, you can request ``blockmap``:

    .. code-block:: sh

       $ ./mitum-example network client \
           '{"_hint":"blockmap-header-v0.0.1","height":33}' \
           "localhost:4320#tls_insecure" \
           --timeout=3s

  * Send *operation*:

    .. code-block:: sh

       $ cat "new-operation.json" | ./mitum-example network client \
           '{"_hint":"send-operation-header-v0.0.1"}' \
           "localhost:4320#tls_insecure" \
           --timeout=3s \
           -body=-

       $ ./mitum-example network client \
           '{"_hint":"send-operation-header-v0.0.1"}' \
           "localhost:4320#tls_insecure" \
           --timeout=3s \
           -body=new-operation.json


* ``remote``

  Remote node connection information. It is same format with ``--discovery`` of
  ``run`` command.


Flags
------------------------------------------------------------

* ``--timeout``

  Set timeout for request. If not set, will wait until finished  by server.

  .. hlist::
     :columns: 1

     * ``3s``: 3 seconds
     * ``3000000000``: 3 seconds in nanoseconds

* ``--body``

  Set request body to upload to server. It should be file or *stdin*. If
  *stdin*, set ``-`` instead of file name.


* ``--dry-run``

  It will not send request to server, just read body.

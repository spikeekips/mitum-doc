============================================================
Command Usage
============================================================

.. code-block:: sh

    $ ./mitum-example --help
      Usage: mitum-example <command>

      Flags:
        -h, --help    Show context-sensitive help.

      logging
        --log.out="stderr"         log output file: {stdout, stderr, <file>}
        --log.format="terminal"    log format: {json, terminal}
        --log.level=debug          log level: {trace, debug, info, warn, error}
        --[no-]log.force-color     log force color

      Commands:
        import <node design> <from directory>
          import from block data

        init <node design> <genesis design>
          init node

        run <node design>
          run node

        network client <header> [<remote>]
          network client

        key new [<seed>]
          generate new key

        key load <key string>
          load key

        key sign <privatekey> <network-id> <body>
          sign

      Run "mitum-example <command> --help" for more information on a command.

.. toctree::
   :caption: Sub commands
   :maxdepth: 1
   :numbered:

   cmd-init
   cmd-run
   cmd-import
   cmd-network-client
   cmd-key


.. toctree::
   :maxdepth: 1


============================================================
Build
============================================================


Requirement
============================================================

* POSIX-compliatnt env
* Install latest golang

.. note::

   We have tested in Linux(amd64 and arm64) and the latest Darwin machine. If you are in other platform, you can easily build and run it.


Get source from github
============================================================

Official mitum github respository is https://github.com/spikeekips/mitum2 .

.. note::
   Originally official mitum was https://github.com/spikeekips/mitum2, but at this time, we are preparing `mitum2`, previous `mitum` will be obsolete for restricted usage.

.. code-block:: sh

   $ git clone https://github.com/spikeekips/mitum2
   $ cd mitum2/example
   $ go build -o ./mitum-example *.go

You can build easily without warnings or errors.

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


Get from release
============================================================

You can find the latest release from https://github.com/spikeekips/mitum2/releases .

.. note::
   At this time, there are no releases. The first release will come.

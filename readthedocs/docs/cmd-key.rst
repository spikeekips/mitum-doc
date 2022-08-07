Command: `key`
============================================================


Command: `key new`
------------------------------------------------------------

Generate new mitum *keypair* (*privatekey* and *publickey*)

.. code-block:: sh

    $ ./mitum-example key new --help
     Usage: a key new [<seed>]

     generate new key

     Arguments:
       [<seed>]    seed for generating key

     Flags:
       -h, --help    Show context-sensitive help.

     logging
       --log.out="stderr"         log output file: {stdout, stderr, <file>}
       --log.format="terminal"    log format: {json, terminal}
       --log.level=debug          log level: {trace, debug, info, warn, error}
       --[no-]log.force-color     log force color


    $ ./mitum-example key new
     {
       "privatekey": "EGGQu4bCWDy1p4RhEZCdE7vP4hP1UeN2jS8U8s7zAomhmpr",
       "publickey": "29Zrw2ZgWyeeHapnxc6cU8D19f5exjqkB4Mk2Bc2ACYyrmpu",
       "hint": "mpr-v0.0.1",
       "seed": "",
       "type": "privatekey"
     }


Arguments
............................................................

* ``seed``

  Optional. With *seed* string, new kepair is generated from seed. As you
  expected, same *seed* will generated same keypair.

  Without seed, different keypair will be generated in each time.


Command: `key load`
------------------------------------------------------------

Load mitum *key* (*privatekey* or *publickey*) and validate it.

.. code-block:: sh

    $ ./mitum-example key load --help
     Usage: a key load <key string>

     load key

     Arguments:
       <key string>    key string

     Flags:
       -h, --help    Show context-sensitive help.

     logging
       --log.out="stderr"         log output file: {stdout, stderr, <file>}
       --log.format="terminal"    log format: {json, terminal}
       --log.level=debug          log level: {trace, debug, info, warn, error}
       --[no-]log.force-color     log force color

    # load the privatekey, EGGQu4bCWDy1p4RhEZCdE7vP4hP1UeN2jS8U8s7zAomhmpr
    $ ./mitum-example key load EGGQu4bCWDy1p4RhEZCdE7vP4hP1UeN2jS8U8s7zAomhmpr
     {
       "privatekey": "EGGQu4bCWDy1p4RhEZCdE7vP4hP1UeN2jS8U8s7zAomhmpr",
       "publickey": "29Zrw2ZgWyeeHapnxc6cU8D19f5exjqkB4Mk2Bc2ACYyrmpu",
       "hint": "mpr-v0.0.1",
       "string": "EGGQu4bCWDy1p4RhEZCdE7vP4hP1UeN2jS8U8s7zAomhmpr",
       "type": "privatekey"
     }

    # load the publickey, 29Zrw2ZgWyeeHapnxc6cU8D19f5exjqkB4Mk2Bc2ACYyrmpu
    $ ./mitum-example key load 29Zrw2ZgWyeeHapnxc6cU8D19f5exjqkB4Mk2Bc2ACYyrmpu
     {
       "publickey": "29Zrw2ZgWyeeHapnxc6cU8D19f5exjqkB4Mk2Bc2ACYyrmpu",
       "hint": "mpu-v0.0.1",
       "string": "29Zrw2ZgWyeeHapnxc6cU8D19f5exjqkB4Mk2Bc2ACYyrmpu",
       "type": "publickey"
     }


Arguments
............................................................

* ``key string``

  Load *key*, parse and validate it. *Key* can be *privatekey* or *publickey*.



.. include:: cmd-key-sign.rst

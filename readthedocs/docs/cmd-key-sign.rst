Command: `key sign`
------------------------------------------------------------

Sign message by the given *privatekey*

.. code-block:: sh

    $ ./mitum-example key sign --help
     Usage: a key sign <privatekey> <network-id> <body>

     sign

     Arguments:
       <privatekey>    privatekey string
       <network-id>    network-id
       <body>          body

     Flags:
       -h, --help                 Show context-sensitive help.

           --node=ADDRESS-FLAG    node address
           --token=STRING         set fact token

     logging
       --log.out="stderr"         log output file: {stdout, stderr, <file>}
       --log.format="terminal"    log format: {json, terminal}
       --log.level=debug          log level: {trace, debug, info, warn, error}
       --[no-]log.force-color     log force color


    # suffrage-candidate-no1sas.json is the oparation to be signed
    $ cat ./suffrage-candidate-no1sas.json
     {
       "fact": {
         "address": "no1sas",
         "publickey": "25AZEiKTPhNkpcj6B1mofXHFyJRR8DaEMcNjc2WSvvW8Jmpu",
         "token": "6qLkX1LfSXejcuzijomt+w==",
         "_hint": "suffrage-candidate-fact-v0.0.1"
       },
       "_hint": "suffrage-candidate-operation-v0.0.1"
     }

    # sign by the privatekey, CaSheUmWGeAYgAKwnwdYrDuJ5fkr2wsVXSpmGFTEUpYtmpr
    $ ./mitum-example key sign \
        CaSheUmWGeAYgAKwnwdYrDuJ5fkr2wsVXSpmGFTEUpYtmpr \
        "mitum; Sat 26 Dec 2020 05:29:13 AM KST" \
        ./suffrage-candidate-no1sas.json \
        --node no1sas \
        --token findme
     {
       "hash": "9PJgJA17dtCiGkTDRTFaK1fLiD3zbPYTNrYDpQhzMcYg",
       "fact": {
         "address": "no1sas",
         "publickey": "25AZEiKTPhNkpcj6B1mofXHFyJRR8DaEMcNjc2WSvvW8Jmpu",
         "hash": "GxhAT8KoWyS8E9d1zM47c5anGrNFC8XiCwWEuAdtSexZ",
         "token": "ZmluZG1l",
         "_hint": "suffrage-candidate-fact-v0.0.1"
       },
       "signed": [
         {
           "node": "no1sas",
           "signed_at": "2022-08-07T04:00:45.499676834Z",
           "signer": "25AZEiKTPhNkpcj6B1mofXHFyJRR8DaEMcNjc2WSvvW8Jmpu",
           "signature": "AN1rKvtAWGE3APxii4jFfe6gzkTBAhqpQiMcLKKQJuSrWRgjGuMUsnG4aspLs3yJbsYgtkpsBLteVTn2vi4LhVn95GRubtWqf"
         }
       ],
       "_hint": "suffrage-candidate-operation-v0.0.1"
     }


Arguments
............................................................

* ``privatekey``

  *Privatekey* for signing

* ``network-id``

  *Network ID for signing

* ``body``

  Message body to be signed


Flags
............................................................

* ``node``

  Some message needs to be signed with *node address*

* ``token``

  Update *token* of *operation*

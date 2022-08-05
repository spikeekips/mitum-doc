============================================================
Config
============================================================

This is example node configuration file.


`first-node.yml`
============================================================

.. literalinclude:: file/first-node.yml
   :caption: first-node.yml
   :language: yaml
   :linenos:
   :lines: -15


* ``address``:

  Local node mitum address. You can make new address by these rules;

  * Must ends with *hint type*, ``sas``
  * Length should be ``6 <= length <=100`` including hint type, ``sas``
  * Empty characters(space, tab, etc) should not be included
  * Regexp, ``^[a-zA-Z0-9][\w\-\.\!\$\*\@]*[a-zA-Z0-9]$`` should be passed


* ``privatekey``:

  *privatekey* for local node. It will be used to sign the messages from local
  node.

  New *privatekey* and it's *publickey* can be easily made:

  .. code-block:: sh

     $ ./mitum-example key new
     {
        "privatekey": "685WQHnt51eaETuQ1WUYEVEdMsBS5XD5SCaU6NuiqHV4mpr",
        "publickey": "gGvk6uzEDWbu7DXTNuiQGRGfUThEbst3EHL79YF3cCKkmpu",
        "hint": "mpr-v0.0.1",
        "seed": "",
        "type": "privatekey"
     }

  For more details about ``key new``, see ":doc:`cmd-usage`"

* ``network_id``:

  *network id* indicates which mitum network local node are in. *netword id*
  should not be empty and not be greater than ``300 bytes``.


* ``network.bind``:

  bind address. *port* should be set. For example,

  .. hlist::
     :columns: 1

     * ``0.0.0.0:4320``: Listen from anywhere
     * ``:4320``: same with ``0.0.0.0:4320``
     * ``127.0.0.1:4320``: Listen only from localhost

* ``network.tls_insecure``:

  If local node uses self-signed TLS certificate, it should be ``true``.


* ``storage.base``:

  *base* indicates the directory for produced data. If not set, current
  directory will be used.

* ``storage.database``:

  *database* indicates the database uri. By default, ``leveldb://``. If not set,
  default database will be used, ``leveldb://<storage.base>/db``.

* ``sync_sources``:

  *Trust nodes*. You can set multiple *trust nodes*.


* ``sync_sources.type``:

  *type* indicates how to fetch the *source_source*.

  .. hlist::
     :columns: 1

     * ``sync-source-node``: node
     * ``sync-source-suffrage-nodes``: get it's suffrage nodes from other node
     * ``sync-source-sync-sources``: get it's sync source nodes from other node
     * ``sync-source-url``: get sync source nodes thru url


* ``sync_sources.type=sync-source-node``:
    .. literalinclude:: file/first-node.yml
       :language: yaml
       :linenos:
       :lines: 11-15


* ``sync_sources.type=sync-suffrage-nodes``:
    .. literalinclude:: file/first-node.yml
       :language: yaml
       :linenos:
       :lines: 16-18


* ``sync_sources.type=sync-source-sync-sources``:
    .. literalinclude:: file/first-node.yml
       :language: yaml
       :linenos:
       :lines: 19-21


* ``sync_sources.type=sync-source-url``: Set url; remote url should return the json list of *NodeConnInfo*.
    .. literalinclude:: file/first-node.yml
       :language: yaml
       :linenos:
       :lines: 22

    .. literalinclude:: file/node_conn_infos.json
       :language: json




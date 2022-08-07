.. toctree::
   :maxdepth: 1


============================================================
Build
============================================================


Requirement
============================================================

* POSIX-compliatnt environment
* Install latest golang

.. note::

   We have tested in Linux(amd64 and arm64) and the latest Darwin machine. If you are in other platform, you can easily find the way to build.


Get source from github
============================================================

Official mitum github respository is https://github.com/spikeekips/mitum2 .

.. note::
   Originally official mitum was https://github.com/spikeekips/mitum2, but at this time, we are preparing `mitum2`, previous `mitum` will be obsolete for restricted usage.

.. code-block:: sh

   $ git clone https://github.com/spikeekips/mitum2
   $ cd mitum2/example
   $ go build -o ./mitum-example *.go

You can build without warnings or errors.


Get from release
============================================================

You can find the latest release from https://github.com/spikeekips/mitum2/releases .

.. note::
   At this time, there are no releases. The first release will come.

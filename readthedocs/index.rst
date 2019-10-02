.. mitum documentation master file, created by
   sphinx-quickstart on Sun Sep 22 15:35:29 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to mitum's documentation!
=================================

.. image:: docs/images/mitum-logo-1000.png
   :scale: 50 %
   :align: center

.. toctree::
   :maxdepth: 1
   :caption: Introduction


   docs/introduction
   docs/how-mitum-works


.. toctree::
   :maxdepth: 1
   :caption: ISAAC+


   docs/isaac+/isaac+-introduction
   docs/isaac+/how-isaac+-works
   docs/isaac+/isaac+-compares-with-classic-pbft
   docs/isaac+/node-states
   docs/isaac+/voting-stages
   docs/isaac+/isaac+-weakness-and-limitations
   docs/contest/index


.. toctree::
   :maxdepth: 1
   :caption: Network


   docs/network/network
   docs/network/node-and-group
   docs/network/designing-network


.. toctree::
   :maxdepth: 1
   :caption: About Project


   docs/contribution


.. include: common.rst

.. this js script will hide side menu from the index page.
.. raw:: html

    <style type="text/css">
    @media screen and (min-width: 1100px) {
        .wy-nav-content-wrap {
            background: inherit;
        }
    }

    .wy-nav-content {
        margin: 0 auto;
    }
    </style>

    <script type="text/javascript">
        $('nav.wy-nav-side').hide();
        $('section.wy-nav-content-wrap').css('marginLeft', 0);
    </script>

.. Theo documentation master file, created by
   sphinx-quickstart on Fri Nov 30 06:30:25 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Theo's documentation!
================================

`Theo App`_ simplifies your SSH servers management
by centralizing AuthorizedKeys.




First steps
-----------

**Theo** is based on 3 components:

1. `theo`_, the core HTTP application
2. `theo-cli`_, the command line interface to administer Theo
3. `theo-agent`_, the program that will be executed by sshd to retrieve AuthorizedKeys

* **Getting started**:
  :doc:`Cookbook for impatients <setup/cookbook>`

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Setup

   setup/setup

.. _Theo App: https://github.com/theoapp/
.. _theo: https://github.com/theoapp/theo-node/
.. _theo-agent: https://github.com/theoapp/theo-agent/
.. _theo-cli: https://github.com/theoapp/theo-cli/

Theo documentation
------------------

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: theo

   theo/installation

Theo-cli documentation
----------------------

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: theo-cli

   theo-cli/installation
   theo-cli/signed_keys

Theo-agent documentation
------------------------

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: theo-agent

   theo-agent/installation

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

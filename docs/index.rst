Welcome to Theo's documentation!
================================

`Theo App`_ is a public key manager, you can use it as replacement for all of your `authorized_keys`
It allows you to set fine permissions (specific user and host) or to use wildcard (ex, using host `%.test.sample.com`)


First steps
-----------

**Theo** is based on 3 components:

1. `theo`_, the core HTTP application
2. `theo-cli`_, the command line interface to administer Theo
3. `theo-agent`_, the program that will be executed by sshd to retrieve AuthorizedKeys

* **Getting started**:
  :doc:`Cookbook <setup/cookbook>`

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Setup

   setup/setup

.. _Theo App: https://github.com/theoapp/
.. _theo: https://github.com/theoapp/theo-node/
.. _theo-agent: https://github.com/theoapp/theo-agent/
.. _theo-cli: https://github.com/theoapp/theo-cli/


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: theo

   theo/installation

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: theo-cli

   theo-cli/installation
   theo-cli/signed_keys

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

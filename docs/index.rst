Welcome to Theo's documentation!
================================

.. figure:: _static/theo-logo.png
    :width: 400
    :alt: Theo logo
    :align: center

`Theo App`_ is the authorized keys manager, you can use it as replacement for all of your `authorized_keys`
It allows you to set fine permissions (specific user and host) or to use wildcard (ex, using host `%.test.sample.com`)


First steps
-----------

**Theo** is based on 3 components:

1. `theo`_, the core HTTP application
2. `theo-cli`_, the command line interface to administer Theo
3. `theo-agent`_, the program that will be executed by sshd to retrieve AuthorizedKeys

* **Getting started**:
  :doc:`Cookbook <setup/cookbook>`


Public test instance
--------------------

A public test instance is available at `theo.test.authkeys.io`_

Database will be reset every 6 hours (0am 6am 12pm 18pm UTC)

Configured tokens:

::

    ADMIN_TOKEN=RMkqF4B8h6jtv3upvy3QubzNyTrMdgn8

    CLIENT_TOKENS=h8LYYwGgTqKFYQ3mRN2hv8vK5CBGJvMs,gAWXaG9ZnhHAXsDbF6dv3NYEbPNuZKR7


Instance has the `REQUIRE_SIGNED_KEY` flag on, so you need to enable key sign/verify on your side

**Be aware that the instance is public, so everyone has access to the data, please use fake email**

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Setup

   setup/setup

.. _Theo App: https://github.com/theoapp/
.. _theo: https://github.com/theoapp/theo-node/
.. _theo-agent: https://github.com/theoapp/theo-agent/
.. _theo-cli: https://github.com/theoapp/theo-cli/
.. _theo.test.authkeys.io: https://theo.test.authkeys.io

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
   theo-cli/usage

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: theo-agent

   theo-agent/installation
   theo-agent/verify_signed_keys

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

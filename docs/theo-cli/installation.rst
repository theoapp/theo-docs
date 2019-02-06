theo-cli installation
=====================

NPM
---

::

    $ npm i -g theoapp-cli

Sources
-------

Clone repo
^^^^^^^^^^
::

    $ git clone https://github.com/theoapp/theo-cli.git

Install dependencies
^^^^^^^^^^^^^^^^^^^^

::

    $ npm install

Build
^^^^^

::

    $ npm run build


Configuration
-------------

**theo-cli** needs 2 variables to work: `THEO_URL` and `THEO_TOKEN`.
They can be set as environment variables:

::

    THEO_URL=https://your.server.name THEO_TOKEN=your_secret_admin_token theo accounts list

Or they can be stored in a file:

::

    THEO_URL=https://your.server.name
    THEO_TOKEN=your_secret_admin_token

**theo-cli** will look at (in this order):

::

  $PWD/.env
  $HOME/.theo/env
  /etc/theo/env

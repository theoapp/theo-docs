Cookbook
===============================

While it's possible to install **theo** and the other components on one single server, you will appreciate all the power of **theo** with multiple servers.
We'll illustrate here a scenario with 2 servers (one for **theo**, the other for **theo-agent**) and a computer for **theo-cli**.

Let's assume the server on which we will install **theo** is ``server`` and the other is ``node-a``

theo
------------

Install with docker
^^^^^^^^^^^^^^^^^^^

On ``server`` you can easily run **theo** as docker container


**NOTE** don't forget to replace *ADMIN_TOKEN* and *CLIENT_TOKENS* values!

::

    $ docker run --rm -v /tmp/theo:/data \
        -e DB_STORAGE=/data/theo.db \
        -e ADMIN_TOKEN=12345 \
        -e CLIENT_TOKENS=abcde,fghij \
        -p 9100:9100 theoapp/theo

Executing the command will result in a running instance of **Theo** listening on port *9100*
and accepting calls from:

* `theo-agent`_ using token *fghij* [1]
* `theo-cli`_ using token *12345* [1]


[1] Token are sent as HTTP header `Authorization: Bearer *token*`

.. _theo-agent: https://github.com/theoapp/theo-agent/
.. _theo-cli: https://github.com/theoapp/theo-cli/

Install from sources
^^^^^^^^^^^^^^^^^^^^

| Please refert to
  :doc:`Full install <install>`
  to install ``theo`` from sources



theo-cli
----------------

Install
^^^^^^^^^^^

To manage ``theo`` we use ``theo-cli``

``theo-cli`` is a node app, available on npm, install it on your computer

::

 $ npm install -g theoapp-cli

``theo-cli`` needs 2 variables: `THEO_URL` and `THEO_TOKEN`.
You can set them as environment variables:

::

    $ export THEO_URL=http://server:9100
    $ export THEO_TOKEN=12345


| **Note** Refer to ``theo-cli``
     :doc:`install document <../theo-cli/installation>` for other ways to set these variables


Create first account
^^^^^^^^^^^^^^^^^^^^


Now you are ready to create the first account on ``theo``

::

    $ theo \
        accounts add \
        --name john.doe \
        --email john.doe@sample.com

Add public key to account
^^^^^^^^^^^^^^^^^^^^^^^^^

Now you need to add a public key to john.doe, you'll use your public key

| **Note** if you don't have it or want to generate another one see
     :doc:`generate ssh key <./generate-sshkey>`


::

    $ theo \
        keys add john.doe@sample.com \
        -k "$(cat ~/.ssh/id_rsa.pub)"

Add permission to account
^^^^^^^^^^^^^^^^^^^^^^^^^

Now we need to add permission to john.doe@sample.com  to access ``server`` as ``root`` (or other existing linux user of ``server``)

::

    $ theo \
        add \
        --user john.doe@sample.com \
        --host node-a \
        --user root

theo-agent
----------------

Download
^^^^^^^^^^^

**theo-agent** is a program written in go. You need to connect to ``node-a`` and run

::

    $ sudo curl -L -o /usr/sbin/theo-agent \
        https://github.com/theoapp/theo-agent/releases/download/$(curl -L -s -H 'Accept: application/json' https://github.com/theoapp/theo-agent/releases/latest |sed -e 's/.*"tag_name":"\([^"]*\)".*/\1/')/theo-agent-linux-amd64

And make it executable

::

    $ sudo chmod 755 /usr/sbin/theo-agent

Install
^^^^^^^

You need to create a system user:

::

    sudo useradd \
        --comment 'Theo Agent' \
        --shell /bin/false \
        --system \
        theo-agent

Configure
^^^^^^^^^

You can let **theo-agent** to configure itself automatically:

With this command you will: disable ssh password authentication, disable AuthorizedKeysFile from user's home (sshd will look for them in /var/cache/theo-agent/%u)

::

    $ sudo theo-agent -install \
        -no-interactive \
        -sshd-config \
        -url http://server:9100 \
        -token fghij



Final check
----------------

Now you're ready to test if everything is working, connect from your computer to ``node-a``

::

    ssh root@node-a

Congratulations!! You made it!

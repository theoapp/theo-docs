Generate SSH keys
=================

To generate SSH

::

    $ ssh-keygen -b 4096

Leaving all the defaults, the command creates a new key in ``~/.ssh/id_rsa``.

The public key is ``~/.ssh/id_rsa.pub``

The public key will be used by the remote server to authorize the connection.

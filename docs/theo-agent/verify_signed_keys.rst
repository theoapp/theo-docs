Verify SSH keys
###############


Use authorized key signature
============================

If you store authorized key' signature along with the authorized key, **theo-agent** is able to verify it before returning it to sshd.
This will guarantee you that no one, in any case, will be able to inject unsolicited authorized keys and consequently get access to your server.

Setup
=====

| Follow
    :doc:`theo-cli guide <../theo-cli/signed_keys>` to create private/public key. Then copy only the public key to the server where **theo-agent** will run.

Configure
=========

With the ``-verify`` flag on, or ``verify: True`` in config file,  **theo-agent** will use the public key indicated in the ``/etc/theo-agent/config.yml`` to verifiy each signature.

This is an example of `config.yml`:

::

    url: https://keys.sample.com
    token: XXXXXXXX
    verify: True
    public_key: /etc/theo-agent/public.pem

``/etc/ssh/sshd_config`` must include the ``-verify`` flag in ``AuthorizedKeysCommand`` :

::

    [...]
    AuthorizedKeysCommand /usr/sbin/theo-agent
    AuthorizedKeysCommandUser theo-user
    [...]

Remember to reload sshd

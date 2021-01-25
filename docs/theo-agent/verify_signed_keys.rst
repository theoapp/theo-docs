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

``public_key`` property in config.yml can be a path to a public key file, a public key, or an array

This is an example of `config.yml` using path value:

::

    url: https://keys.sample.com
    token: XXXXXXXX
    verify: True
    public_key: /etc/theo-agent/public.pem

This is an example of `config.yml` using an array of public keys paths

::

    url: https://keys.sample.com
    token: XXXXXXXX
    verify: True
    public_key:
    - /etc/theo-agent/public.pem
    - /etc/theo-agent/public2.pem

Here's an example og using embed public key

::
    url: https://keys.sample.com
    token: XXXXXXXX
    verify: True
    public_key: |
        -----BEGIN PUBLIC KEY-----
        MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAvz9gLQyHy7EAdh6NggPc
        IIe0oHKLxUrim4Lhlq/xN1Eg+g5Iq9NSnMTBfiC4VS207X0G76tygOerh1m9ReqL
        FqUmaBB2g0OupcayKgJttKMC1jxRD6TWrvXVTHIgYya3FGD6/yBOiNztJccRgkbg
        pSLe5Nd3n8piJmVvaAmIjQmrAqGzV02Axjv/WY+qFVPvdG+YG4O18ypMJvdPAlBR
        z6A9V7J1DHQNZTCWVPbjGTS0LZtgJeUXuKTQlNikqBz88IzTNDRpbMaUa2DCxzvL
        U4N5qfhZjiVoYzEZtf91iXPC+Yl+Pj4yfZBxTMEgILWwWSZwd9M2EiHtJ+KDLcsb
        lnoTKSJfmeu8pgBXvaFA8usBNi2sACPclwNDUq5CG4APmP3/AHKPfzR+3BLUTQ+s
        wzT8AIJENRF4jMPzxcCUW4M2SjLElNan1F8lZdp8XwxNRlAOe6gBfyidAwGFRfmC
        Wn1Y9x/sLyCBQG0FCGvuCvqxSVOLnYf4T0N5tK9OUJkaJvMnA98i0DvgYM6TbVjB
        ULTiuVkBZ75qCicwMcfEvNN2SewYW2zZeJtnWDpZKXIEuv+ifG7mRXRzK75cIDsW
        AFD/GwweoEG9WPf62um7BpKC3ewd+nERIjGrag+/+3OF8IW/xlicIVMtw+L9ZQ0T
        o881E5rKe5WzEX90LbTD3xMCAwEAAQ==
        -----END PUBLIC KEY-----

``/etc/ssh/sshd_config`` must include the ``-verify`` flag in ``AuthorizedKeysCommand`` :

::

    [...]
    AuthorizedKeysCommand /usr/sbin/theo-agent -verify
    AuthorizedKeysCommandUser theo-user
    [...]

Remember to reload sshd

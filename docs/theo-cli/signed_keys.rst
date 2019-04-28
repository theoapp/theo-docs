Sign SSH keys
###############


Use authorized key signature
----------------------------

Storing authorized key' signature along with the authorized key, let **theo-agent** to verify it before returning it to sshd.
This will guarantee you that no one in any case will be able to inject unsolicited authorized keys and consequently get access to your server.

Setup
-----

First, you need to create private/public keys, we'll use ``openssl``

::

    openssl genrsa -aes128 -out private.pem 4096


It will prompt you to insert a pass phrase, memorize it!

now we need to extract the public key (we will use it with `theo-agent` to verify the signatures)

::

    openssl rsa -in private.pem -pubout -out public.pem


It will ask you the pass phrase to unlock the private key.

| The public key has to be copied on all the servers where **theo-agent** will run.
    :doc:`See theo-agent VERIFY <../theo-agent/verify_signed_keys>`

Configure
---------

To enable signing, you could set 2 variables: `THEO_PRIVATE_KEY` and `THEO_PRIVATE_KEY_PASSPHRASE`.

You can do it in 2 ways:

* Adding them as environment variables while executing `theo`.
* Adding them to the config file (the first file found will be used):

::

    $PWD/.env
    $HOME/.theo/env
    /etc/theo/env

`THEO_PRIVATE_KEY` must point to your private key (use full path).
`THEO_PRIVATE_KEY_PASSPHRASE` is the pass phrase to unlock the private key.

Since theo-cli 0.9.0 it's possible to pass private key path and passphrase as arguments.

::

    --certificate, -c       Path to private key                           [string]
    --passphrase, -p        passphrase for private key                    [string]
    --passphrase-stdin, -i  read passphrase for private key from stdin   [boolean]


Usage
-----

When adding a new authorized key to a user, to let `theo` signs the SSH public key add the `--sign` flag


::

    theo keys add john.doe@example.com \
        --sign \
        --key "ssh-rsa AAAAB3NzaC1yc2E[...]7xUw== john.doe@laptop"

::

    theo keys add john.doe@example.com \
        --passphrase-stdin \
        --sign \
        --key "ssh-rsa AAAAB3NzaC1yc2E[...]7xUw== john.doe@laptop"


::

    theo keys add john.doe@example.com \
        --passphrase your-passphrase \
        --sign \
        --key "ssh-rsa AAAAB3NzaC1yc2E[...]7xUw== john.doe@laptop"

::

    theo keys add john.doe@example.com \
        --passphrase-stdin \
        --certificate $HOME/private/theo-private.pem
        --sign \
        --key "ssh-rsa AAAAB3NzaC1yc2E[...]7xUw== john.doe@laptop"


::

    theo keys add john.doe@example.com \
        --passphrase your-passphrase \
        --certificate $HOME/private/theo-private.pem
        --sign \
        --key "ssh-rsa AAAAB3NzaC1yc2E[...]7xUw== john.doe@laptop"


Since `theo-cli` `0.10.0`, if you prefer to get the signature yourself (using OpenSSH or other tool) you can pass it to theo with the `--signature` argument

::
    theo keys add john.doe@example.com \
        --key "ssh-rsa AAAAB3NzaC1yc2E[...]7xUw== john.doe@laptop" \
        --signature "81db52ca9a0d6d2[...]31a62663c0ce0a38c24cd7"

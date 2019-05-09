theo-agent installation
================================

ATTENTION: OpenSSH must be version 6.2 or higher

Download
-------------

1. Download one of the binaries for your system:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    THEO_AGENT_LATEST=$(curl -L -s -H 'Accept: application/json' https://github.com/theoapp/theo-agent/releases/latest |sed -e 's/.*"tag_name":"\([^"]*\)".*/\1/')
    sudo curl -L -o /usr/sbin/theo-agent \
        https://github.com/theoapp/theo-agent/releases/download/${THEO_AGENT_LATEST}/theo-agent-$(uname -s)-$(uname -m)

2. Make it executable
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo chmod 755 /usr/sbin/theo-agent

3. Create a Theo Agent user:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    sudo useradd \
        --comment 'Theo Agent' \
        --shell /bin/false \
        --system \
        theo-agent

4. Install
^^^^^^^^^^

4.1. Full Automatic install
"""""""""""""""""""""""""""


    ATTENTION!!!

    This command will:

    * disable tunneled clear text passwords (no more user/password login!)
    * disable users' .ssh/authorized_keys
    * set theo-agent as unique source for authorized_keys

    We suggest to keep an open session until you're sure everything works as expected

    ::

        sudo theo-agent -install \
            -no-interactive \
            -sshd-config \
            -url ${THEO_URL} \
            -token ${THEO_CLIENT_TOKEN}



4.2. Semi-Automatic install
"""""""""""""""""""""""""""
    ::

        sudo theo-agent -install \
            -no-interactive \
            -url ${THEO_URL} \
            -token ${THEO_CLIENT_TOKEN}

    Edit ``/etc/ssh/sshd_config`` as suggested

4.3. Semi-manual install
"""""""""""""""""""""""""""
    ::

        sudo theo-agent -install

    Answer to the questions and edit ``/etc/ssh/sshd_config`` as suggested

4.4. Manual install
"""""""""""""""""""""""""""

    *ATTENTION: with OpenSSH older than 6.9 jump to section 4.5*

    Create a ``config.yml`` file (default is */etc/theo-agent/config.yml*):

    ::

        url: THEO_URL
        token: THEO_CLIENT_TOKEN

    Create a cache directory (default is */var/cache/theo-agent*):

    ::

        mkdir /var/cache/theo-agent
        chmod 755 /var/cache/theo-agent
        chown theo-agent /var/cache/theo-agent

    Modify `/etc/ssh/sshd_config` (if you changed the default path, add the options to the command)

    ::

        PasswordAuthentication no
        AuthorizedKeysFile /var/cache/theo-agent/%u
        AuthorizedKeysCommand /usr/sbin/theo-agent [-config-file /path/to/config.yml] [-cache-path /path/to/cache/dir] %u
        AuthorizedKeysCommandUser theo-agent


4.5. Manual install with OpenSSH older than 6.9
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

    OpenSSH older than 6.9 does not support passing arguments to the command set with `AuthorizedKeysCommand`, you must use the default values:

    Create a ``config.yml`` file in */etc/theo-agent/config.yml*:

    ::

        url: THEO_URL
        token: THEO_CLIENT_TOKEN


    Create a cache directory */var/cache/theo-agent*:

    ::

        mkdir /var/cache/theo-agent
        chmod 755 /var/cache/theo-agent
        chown theo-agent /var/cache/theo-agent

    Modify `/etc/ssh/sshd_config`

    ::

        PasswordAuthentication no
        AuthorizedKeysFile /var/cache/theo-agent/%u
        AuthorizedKeysCommand /usr/sbin/theo-agent
        AuthorizedKeysCommandUser theo-agent


5. Restart openssh
^^^^^^^^^^^^^^^^^^

    ::

        sudo systemctl restart ssh.service

6. SELinux
^^^^^^^^^^

If you're on a system with SELinux enabled (You can check it with: `getenforce`), you must switch sshd to permissive mode:

    ::

         sudo semanage permissive -a sshd_t

Installation
############

With docker
============

::

    $ docker pull theoapp/theo

From sources
============

Clone repo
----------

::

    $ git clone https://github.com/theoapp/theo-node.git

Install dependencies
--------------------

::

    $ npm i --no-optional

Build
----------

::

    $ npm run build


Configure
----------

To configure there are 2 ways:

1. Using environment variables
2. Using ``settings.json``

1. Environment variables
^^^^^^^^^^^^^^^^^^^^^^^^

+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| Name             | Mandatory | Default value                      | Meaning                                   | Type        |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| PORT             | NO        | 9100                               | The port on wichh the http                | int         |
|                  |           |                                    | server will listen                        |             |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| DB_ENGINE        | NO        | sqlite                             | Use sqlite3 as database. Needs DB_STORAGE | enum:       |
|                  |           |                                    +-------------------------------------------+ * sqlite    |
|                  |           |                                    | Use mariadb as database. Needs DB_HOST,   | * mariadb   |
|                  |           |                                    | DB_USER, DB_PASSWORD, DB_NAME             |             |
|                  |           |                                    |                                           |             |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| DB_STORAGE       | NO        | ./data/theo.db                     | Path to sqlite3 db. Absolute or relative  | string      |
|                  |           |                                    | to node process                           |             |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| DB_HOST          | YES(1)    |                                    | Mariadb server hostname or ip             | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| DB_USER          | YES(1)    |                                    | Mariadb username                          | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| DB_PASSWORD      | YES(1)    |                                    | Mariadb password                          | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| DB_NAME          | YES(1)    |                                    | Mariadb database                          | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| ADMIN_TOKEN      | YES(2)    |                                    | Admin token                               | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| CLIENT_TOKENS    | YES(2)    |                                    | Client tokens: comma separated            | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| CORE_TOKEN       | NO        |                                    | Core token                                | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| CACHE_ENABLED    | NO        |                                    | if set, the cache server will be used     | enum:       |
|                  |           |                                    |                                           | * redis     |
|                  |           |                                    |                                           | * memcached |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| CACHE_URI        | YES(3)    | localhost:11211                    | memcached connection url                  | string      |
|                  |           +------------------------------------+-------------------------------------------+             |
|                  |           | redis://localhost:6379             | redis connection url                      |             |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+
| CACHE_OPTIONS    | NO        |                                    | Optional cache parameters                 | string      |
+------------------+-----------+------------------------------------+-------------------------------------------+-------------+



\(1) Mandatory if DB_ENGINE=mariadb

\(2) Mandatory if CORE_TOKEN is not set

\(3) Mandatory if CACHE_ENABLED=memcached or CACHE_ENABLED=redis

**NOTE** It's possible to save the variables in a `.env` file in the project's root

2. settings.json
^^^^^^^^^^^^^^^^^^^^^^^^

It possibile to use ``settings.json`` file in the project's root to load **theo** configuration.

::

    {
      "admin": {
        "token": "ch4ng3Me"
      },
      "client": {
        "tokens": [
          "njknsjd2412fnjkasnj",
          "knkjnknfjfnjenkln"
        ]
      },
      "sqlite": {
        "path": "./data/theo.db"
      },
      "server": {
        "http_port": 8890
      },
      "cache": {
        "type": "memcached",
        "settings": {
          "uri": "localhost:11211",
          "options": false
        }
      }
    }

Run
---

::

    $ npm start

# oracle12c-docker
A lightweight and configurable Oracle 12c Docker container

Before you begin
----------------

Due to Oracle licensing, you must manually download the Oracle 12c binaries from the Oracle website and agree to the Oracle license terms.

1. Clone this repository
1. Download the Oracle Database 12c binary `linuxx64_12201_database.zip` from http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html
1. Put the zip in the `database` directory. Do not unzip it.

Building
--------
Build the image:
`docker build --force-rm=true --no-cache=true --shm-size=1G -t steveswinsburg/oracle12c-ee .`

Run it:
`docker run steveswinsburg/oracle12c-ee`

Optional configuration
----------------------
TODO


Connecting to Oracle
--------------------

* Hostname: localhost
* Port: 1521
* SID: orcl
* All passwords are `password`.

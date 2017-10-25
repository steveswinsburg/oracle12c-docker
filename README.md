# oracle12c-docker
A lightweight and configurable Oracle 12c Docker container

Before you begin
----------------
Due to Oracle licensing, you must manually download the Oracle 12c binaries from the Oracle website and agree to the Oracle license terms.

1. Clone this repository
1. Download the Oracle Database 12c binary `linuxx64_12201_database.zip` from http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html
1. Put the zip in the base directory. Do not unzip it.

Building
--------
Build the image:
`docker build --force-rm=true --no-cache=true --shm-size=1G -t steveswinsburg/oracle12c-ee .`

Run it:
`docker run steveswinsburg/oracle12c-ee`

On first run, the database will be provisioned. Using the command above will set defaults for everything. You will need to monitor the output to get the database password. If you wish to set your own password and SID, see the *Optional configuration* section below.
Also, you must set the `-v` parameter if you want the database to be persisted over container recreation.

Configuration
-------------
The default run command above will get you up and running but should be modified according to your needs. See the *Parameters* section below.

A more complete run command might look like:

```
docker run --name steveswinsburg/oracle12c-ee \
-p 1521:1521 \
-e ORACLE_SID=orcl \
-e ORACLE_PWD=password \
-v /opt/oracle/oradata \
steveswinsburg/oracle12c-ee
```

**Parameters:**
```
   --name:        The name of the container (default: auto generated)
   -p:            The port mapping of the host port to the container port.
                  Two ports are exposed: 1521 (Oracle Listener)
   -e ORACLE_SID: The Oracle Database SID that should be used (default: ORCLCDB)
   -e ORACLE_PWD: The Oracle Database SYS, SYSTEM and PDB_ADMIN password (default: auto generated)
   -e ORACLE_CHARACTERSET:
                  The character set to use when creating the database (default: AL32UTF8)
   -v /opt/oracle/oradata
                  The data volume to use for the database.
                  Has to be writable by the Unix "oracle" (uid: 54321) user inside the container!
                  If omitted the database will not be persisted over container recreation.
   -v /opt/oracle/scripts/startup | /docker-entrypoint-initdb.d/startup
                  Optional: A volume with custom scripts to be run after database startup.
                  For further details see the "Running scripts after setup and on startup" section below.
   -v /opt/oracle/scripts/setup | /docker-entrypoint-initdb.d/setup
                  Optional: A volume with custom scripts to be run after database setup.
                  For further details see the "Running scripts after setup and on startup" section below.
```

Connecting to Oracle
--------------------

Once the container has been started you can connect to it like any other database. For example:
`sqlplus sys/<your password>@//localhost:1521/<your SID> as sysdba`

If you did not set the `ORACLE_PWD` parameter, check the docker run output for the password.

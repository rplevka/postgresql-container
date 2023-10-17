Extending PostgreSQL image by installing TimescaleDB
====================================================

Timescaledb is an extension that must be built first. For each PostgreSQL version, we need a binary compatible build, which is not available for RHEL builds of PostgreSQL.

One can build it pretty easily by consuming Fedora RPM and build it with a concrete RHEL version. For example, this is a copr repository with timescaledb built for RHEL-9 RPMs of PostgreSQL 15: https://src.fedoraproject.org/rpms/timescaledb

To install and enable timescaledb from this copr repository, use a Dockerfile in this directory and run:

```
$ podman build . -t timescaledb-pgsql:15
```

Then, run the resulting image as usually:

```
$ podman run -d -e POSTGRESQL_ADMIN_PASSWORD=password --name pgsql-with-timescaledb timescaledb-pgsql:15
```

And see the extension is enabled:
```
$ podman exec -ti pgsql-with-timescaledb bash -c psql
psql (15.2)
Type "help" for help.

postgres=# \dx
                                               List of installed extensions
    Name     | Version |   Schema   |                                     Description                                      
-------------+---------+------------+--------------------------------------------------------------------------------------
 plpgsql     | 1.0     | pg_catalog | PL/pgSQL procedural language
 timescaledb | 2.12.0  | public     | Enables scalable inserts and complex queries for time-series data (Apache 2 Edition)
(2 rows)

```

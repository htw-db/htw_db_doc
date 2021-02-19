# Insights

## Gathering general information

Login to your system as user postgres and connect the database.

```text
$ psql
psql (13.2 (Debian 13.2-1.pgdg110+1))
Type "help" for help.
```

To check login info use following command from the database command prompt.

```text
postgres=# \conninfo
You are connected to database "postgres" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
```

List roles

```text
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

There is another way to display all roles.  Notice that the roles that start with with `pg_` are system roles.

```text
postgres=# SELECT rolname FROM pg_roles;
          rolname
---------------------------
 pg_monitor
 pg_read_all_settings
 pg_read_all_stats
 pg_stat_scan_tables
 pg_read_server_files
 pg_write_server_files
 pg_execute_server_program
 pg_signal_backend
 postgres
```

List databases

```text
postgres=# \l
                             List of databases
   Name    |  Owner   | Encoding  | Collate | Ctype |   Access privileges
-----------+----------+-----------+---------+-------+-----------------------
 postgres  | postgres | SQL_ASCII | C       | C     |
 template0 | postgres | SQL_ASCII | C       | C     | =c/postgres          +
           |          |           |         |       | postgres=CTc/postgres
 template1 | postgres | SQL_ASCII | C       | C     | =c/postgres          +
           |          |           |         |       | postgres=CTc/postgres
```

## Understanding the workflow

Authentication takes place via LDAP. So that these users are all assigned to one group. This group has already been created in the deployment in the form of a role.

```text
postgres=# CREATE ROLE ldap_users;
CREATE ROLE
```

When a user authenticates for the first time, a new role is created in the database and added to that specific group.

```text
postgres=# CREATE ROLE s0558151 WITH NOSUPERUSER LOGIN CONNECTION LIMIT 10 IN ROLE ldap_users;
CREATE ROLE
```




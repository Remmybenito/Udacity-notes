# Postgres / Psql

### Postgres server commands - command line

```markdown
pg_ctl -D "C:\Program Files\PostgreSQL\15\data" start
```
```markdown
pg_ctl -D "C:\Program Files\PostgreSQL\15\data" stop
```
```markdown
pg_ctl -D "C:\Program Files\PostgreSQL\15\data" restart
```

>Note: These commands will start the postgres server in which we can run psql commands with. The server must be started in the above folder on a local computer in order to function.

---

### Psql commands - cmd

```markdown
* \l
List all databases on the server, their owners, and user access levels

* \c <dbname>
Connect to a database named <dbname>

* \dt
Show database tables

* \d <tablename>
Describe table schema

* \q
Quit psql, returning to terminal

* \?
Get help, see list of available commands
```

>Note:  This will access the running server as user ‘postgres’. Password will be requested after this command is run. Default password is “password”

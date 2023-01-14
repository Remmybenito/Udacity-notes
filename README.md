# Udacity-notes
# Postgres

### Postgres server commands
We can start, stop, and restart a Postgres server on a local machine by using the follow commands that point to our installation of PostgreSQL>data folder. Use these within command line:

| Command          | Notes |
|----              |-------|
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" start`    |Starts Postgres server   |
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" stop`     |Stops Postgres server    |
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" restart`  |Restarts Postgres server |



# Psql commands - cmd

First, we have to connect to our running Postgres server (see above). Use the command below to connect as user 'postgres'

```
psql -U postgres
```
>Note:  This will access the running server as user ‘postgres’. Password will be requested after this command is run. Default password is “password” or is set through postgres installation.

Once connected, we are then able to use the commands below to view our data.

| Command          | Notes |
| :---:            |-------|
|`\l`              | List all databases on the server, their owners, and user access levels |
|`\c <dbname>`     |Connect to a database named <dbname>
|`\dt`             |Show database tables
|`\d` <tablename>  |Describe table schema
|`\q`              |Quit psql, returning to terminal
|`\?`              |Get help, see list of available commands


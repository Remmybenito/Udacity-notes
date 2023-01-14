# Udacity-notes
# Postgres

### Installation
links to installation sites

### Postgres server commands
We can start, stop, and restart a Postgres server on a local machine by using the follow commands that point to our installation of PostgreSQL>data folder. Use these within command line:

| Command          | Notes |
|----              |-------|
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" start`    |Starts Postgres server   |
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" stop`     |Stops Postgres server    |
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" restart`  |Restarts Postgres server |



# PSQL

### Connect to a live server on local machine
First, we have to connect to our running Postgres server (see above). Use the command below to connect as user 'postgres'

```
psql -U postgres
```
>Note:  This will access the running server as user ‘postgres’. Password will be requested after this command is run. Default password is “password” or is set through postgres installation.


### PSQL Commands
Once connected, we are then able to use the commands below to view our data.

| Command          | Notes |
|    ---           |-------|
|`\l`              | List all databases on the server, their owners, and user access levels |
|`\c <dbname>`     |Connect to a database named dbname
|`\dt`             |Show database tables
|`\d <tablename> ` |Describe table schema
|`\q`              |Quit psql, returning to terminal
|`\?`              |Get help, see list of available commands


# FLASK

### Flask Basics

Import Flask for use in a python script and initialize it into a variable. Conventionally, the variable is called 'app'


```python
from flask import FLASK

app = Flask(__name__)
```

We use the @ python decorator to set up Flask routing to '/', which is essentially a blank default home page route

```python
@app.route('/')
def index():
    return 'Hellow World!'
```
# SQLAlchemy

### SQLAlchemy Basics

```python 
db.Model
```
We can use the db variable above to create tables, columns, and data within a database using classes and objects as follows:

```python 
class Person(db.Model):
   __tablename__ = ‘persons’
   id = db.Column(db.Integer, primary_key=True)
   name = db.Column(db.String(), nullable=False)
```

```python
db.create_all( )
```
Creates tables based on the db.Model. In this case of db.Model created above, it will create the table ‘persons’ with all of the data we initialized in our class above.

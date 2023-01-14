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


### Flask Migrations

##### Migrations Basics
Migrations deal with how we manage modifications to our data schema over time. A migration is a file that keeps track of changes to our database schema (structure of our database).

##### Upgrades and Rollbacks
Migrations stack together in order to form the latest version of our database schema. We can upgrade our database schema by applying migrations, and we can roll back our database schema to a former version by reverting migrations that we have applied.
 
##### Migration command-line scripts
There are generally 3 scripts needed, for migrate: 
- **migrate:** creating a migration script template to fill out; generating a migration file based on changes to be made
- **upgrade:** applying migrations that hadn't been applied yet ("upgrading" our database)
- **downgrade:** rolling back applied migrations that were problematic ("downgrading" our database)
 
 
```
$ flask db init
```
This will add a migrations folder to your application. The contents of this folder need to be added to version control along with your other source files.
You can then generate an initial migration:
```
$ flask db migrate -m "Initial migration."
```
Then you can apply the changes described by the migration script to your database:
```
$ flask db upgrade
```
Each time the database models change, repeat the migrate and upgrade commands.



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


### Select Records
Once the initial functionality of our Flask app is set up and connected with SQLAlchemy to our database, we can use functions to query a model created within our app.

| Function | Example | Notes |
| :---:    |:---: | ---- |
|`all()`   | MyModel.query.all() | same as doing a `SELECT *`, fetching all records from the model's table. Returns a list of objects
|`first()` | |
---
## Filtering
| Function     | Example | Notes |
|--------------|---------|-------|
|`filter_by()` |`MyModel.query.filter_by(attr='some value')`               |Similar to `SELECT * from ... WHERE`
|`filter()`    |`MyModel.query.filter(MyOtherModel.some_attr='some value')`|Similar to `filter_by` , but instead, you specify attributes on a given Model.
|`like()`      ||
|`ilike()`     ||


>Select statement cheat sheet: https://video.udacity-data.com/topher/2019/August/5d5a52af_query-cheat-sheet/query-cheat-sheet.pdf

# Udacity-notes
# Postgres

### Installation
Download Postgresql [here](https://www.postgresql.org/download/)

### Postgres server commands
On **Windows**, we can start, stop, and restart a Postgres server on a local machine by using the follow commands that point to our installation of PostgreSQL>data folder. Use these within command line:

| Command          | Notes |
|----              |-------|
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" start`    |Starts Postgres server   |
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" stop`     |Stops Postgres server    |
|`pg_ctl -D "C:\Program Files\PostgreSQL\15\data" restart`  |Restarts Postgres server |

>Instructions for starting and stopping a Postgres server [here](https://tableplus.com/blog/2018/10/how-to-start-stop-restart-postgresql-server.html)

# PSQL

### Connect to a live server on local machine
First, we have to connect to our running Postgres server (see above). Use the command below to connect as user 'postgres'

```
psql -U postgres
```
>Note:  This will access the running server as user ‘postgres’. Password will be requested after this command is run. Default password is “password” or is set through postgres installation.


### PSQL Command Line
Once connected, we are then able to use the commands below to view our data.

| Command          | Notes |
|    ---           |-------|
|`\l`              | List all databases on the server, their owners, and user access levels |
|`\c <dbname>`     |Connect to a database named dbname
|`\dt`             |Show database tables
|`\d <tablename> ` |Describe table schema
|`\q`              |Quit psql, returning to terminal
|`\?`              |Get help, see list of available commands

### Working with Databases (PSQL Command Line on Windows)
Here are a few more commands that you can use to manipulate databases through PSQL:

| Command                        | Notes |
|    ---                         |-------|
|`CREATE DATABASE <dbname>;`     |Creates a database called dbname on our PSQL server. (Remove the brackets<> when naming) |
|`DROP DATABASE <dbname>;`       |Deletes database dbname|
|`exit`                          |Exits PSQL command line|

We can then use SQL to manipulate the data within our created databases:
**example**


``create table table1( id INTEGER PRIMARY KEY, description VARCHAR NOT NULL); ``<br />
``\d table1`` <br />
``INSERT INTO table1 (id, description) VALUES (1,"This is a thing");`` <br />
``SELECT * FROM table1;`` <br />
``SELECT * FROM table1 WHERE id = 1;`` <br />
``SELECT * FROM table1 WHERE id = 2;`` <br />



# FLASK

### Installation
You can install Flask SQL Alchemy using pip3 or pip if you haven't linked to pip3,

```
pip install flask-sqlalchemy
```
Flask documentation can be found [here](https://flask.palletsprojects.com/en/2.2.x/)
FlaskSQLAlchemy documenation can be found [here](https://flask-sqlalchemy.palletsprojects.com/en/3.0.x/)



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
    return 'Hello World!'
```

### Running the Flask app

**Option 1**
- Make sure you are in the directory that contains app.py
- We run a flask app defined at app.py by running this line of code on one line
- ``FLASK_APP=app.py FLASK_DEBUG=true flask run``
- ``FLASK_APP`` must be set to the server file path with an equal sign in between. No spaces.``FLASK_APP = app.py`` will not work.
- ``FLASK_DEBUG=true`` will enable debug mode which allows live reload
- ``flask run`` actually executes the flask server code in the ``app.py`` file

**Option 2**
- Make sure you are in the directory that contains app.py
- Do not enter any of the flask code mentioned in option 1
- Simply include the following in your python file:

```python
from flask import Flask

app = Flask(__name__)

#Your program goes here

#always include this at the bottom of your code
if __name__ == '__main__':
   app.run(host="0.0.0.0")
```

- Then, in the terminal, run the app by typing
```
python app.py
```

All together, our simple Hello World Flask app should look as follows:

```python
#imported Flask into python app
from flask import Flask

#initialized this app as a Flask application
app = Flask(__name__)

#created the index route/view
@app.route('/')
def index():
    return 'Hello World!'

#allows us to run in debug mode without bulky commands in terminal
if __name__ == '__main__':
   app.run(host="0.0.0.0")
```

### Connect to our Database in a Flask application
1. Import the Flask-SQLAlchemy library.
2. Set the app.config to our database:

```python
from flask import Flask
# import SQLAlchemy into our python application
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
# app.config will point to our database below
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://postgres:abc@localhost:5432/example'
db = SQLAlchemy(app)
```
![Image](https://video.udacity-data.com/topher/2019/August/5d4df44e_database-connection-uri-parts/database-connection-uri-parts.png)

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


>Select statement [cheat sheet](https://video.udacity-data.com/topher/2019/August/5d5a52af_query-cheat-sheet/query-cheat-sheet.pdf)

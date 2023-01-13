# Flask-SQLAlchemy

### Python SQL Toolkit
SQLAlchemy is an end-to-end toolkit for working with relational databases without writing SQL. It offers an ORM (Object Relational Mapping Library), where tables and columns in a 
database are mapped to class objects and attributes within SQLAlchmemy

## Flask Basics

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
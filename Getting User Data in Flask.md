## Getting User Data in Flask (Part 1)

#### Using a form with Flask
- Forms take an ``action`` (name of the route) and ``method`` (route method) to submit data to our server.
- The name attribute on a form control element is the key used to retrieve data from ``request.get(<key>)``.
- All forms either define a submit button, or allow the user to hit **ENTER** on an input to submit the form.

**Example**
```html
#action (name of the route) and method (route method)
<form method="post" action="/todos/create">
      <input type="text" name="description" />
      <input type="submit" value="Create" />
</form>
```

### Developing the Controller

```python
@app.route('/todos/create', method=['POST'])
def create_todo():
  # name attribute on a form control element is the key used to retrieve data from request.get, or request.form.get in this case
  description = request.form.get('description', '')
  todo = Todo(description=description)
  db.session.add(todo)
  db.session.commit()
  return redirect(url_for('index'))
```


All together, in order to display our list, our Html and Python scripts should look similar to the following:

### HTML
```html
<html>
  <head>
    <title>Todo App</title>
  </head>
  <body>
    <form method="post" action="/todos/create">
      <input type="text" name="description" />
      <input type="submit" value="Create" />
    </form>
    <ul>
      {% for d in data %}
      <li>{{ d.description }}</li>
      {% endfor %}
    </ul>
  </body>
</html>
```

### Python
```python
from flask import Flask, render_template, abort, url_for, jsonify
from flask_sqlalchemy import SQLAlchemy
from flask import request

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgres://postgres:abc@localhost:5432/todoapp'
db = SQLAlchemy(app)

class Todo(db.Model):
  __tablename__ = 'todos'
  id = db.Column(db.Integer, primary_key=True)
  description = db.Column(db.String(), nullable=False)

  def __repr__(self):
    return f'<Todo {self.id} {self.description}>'

db.create_all()

@app.route('/')
def index():
  return render_template('index.html', data=Todo.query.all())

#always include this at the bottom of your code
if __name__ == '__main__':
   app.run(host="0.0.0.0", port=3000)
```
---
## Getting User Data in Flask (Part 2)

#### Using AJAX and Fetch to display data
From the example in Part 1, we can convert our standard data retrieval into AJAX requests using the ``fetch`` method.

The boilerplate code looks similar to the following and is to be inserted into our HTML using a ``<script>`` tag:
```javascript
fetch('/my/request', {
  method: 'POST',
  body: JSON.stringify({
    'description': 'some description here'
  }),
  headers: {
    'Content-Type': 'application/json'
  }
});
```
In the context of our **To-do List example**, our HTML will look similar to the following:
```javascript
<form id="form">
        <input type="text" id="description" name="description" />
        <input type="submit" value="Create" />
    </form>
    <div id="error" class="hidden"> Something went wrong! </div>
    <ul id="todos">
        {% for d in data %}
        <li>{{ d.description }}</li>
        {% endfor %}
    </ul>
    
<!-- To hide an error display message in case something happens to our data -->
<div class = "hidden" id = "error" style="display:none;"> Something went wrong! </div>

<!-- Script tag inserted -->
    <script>
        document.getElementById('form').onsubmit = function (e) {
           e.preventDefault();
           
           #fetch method
           fetch('/todos/create', {
                method: 'POST',
                body: JSON.stringify({
                    'description': document.getElementById('description').value
                }),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(function(response) {
                return response.json();
            })
            .then(function(jsonResponse) {
                console.log(jsonResponse);
                const liItem = document.createElement('LI');
                liItem.innerHTML = jsonResponse['description'];
                document.getElementById('todos').appendChild(liItem);
                document.getElementById('error').className = 'hidden';
            })
            .catch(function() {
                document.getElementById('error').className = '';
            })
        
        }
    </script>
```

Whereas our python will change slightly to:

```python
from flask import Flask, render_template, request, redirect, url_for, jsonify

#rest of Flask app here...

@app.route('/todos/create', methods=['POST'])
def create_todo():
  description = request.get_json()['description']
  todo = Todo(description=description)
  db.session.add(todo)
  db.session.commit()
  return jsonify({
    'description': todo.description
  })
```
---
#### Error handling data requests 
- Commits can succeed or fail. On fail, we want to rollback the session to avoid potential implicit commits done by the database on closing a connection.
- Good practice is to close connections at the end of every session used in a controller, to return the connection back to the connection pool.

We can implement error handling in a Flask app by using the following pattern:
```python
 import sys

 try:
   todo = Todo(description=description)
   db.session.add(todo)
   db.session.commit()
 except:
   db.session.rollback()
   error=True
   print(sys.exc_info())
 finally:
   db.session.close()
```

In the context of implementing within our To-do app, it would similar to the following:

```python
@app.route('/todos/create', methods=['POST'])
def create_todo():   
   body={}
   error = False
   try: 
       description =  request.get_json()['description']
       todo = Todo(description=description)
       body['description'] = todo.description
       db.session.add(todo)
       db.session.commit()
   except:        
        error = True
        db.session.rollback()
        print(sys.exc_info())
   finally:
        db.session.close()           
        if  error == True:
            abort(400)
        else:            
            return jsonify(body)
```




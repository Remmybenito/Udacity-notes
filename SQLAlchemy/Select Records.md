# Select Records
Once the initial functionality of our Flask app is set up and connected with SQLAlchemy to our database, we can use functions to query a model created within our app.

| Function | Example | Notes |
| :---: |:---: | ---- |
|`all()`   | MyModel.query.all() | same as doing a SELECT *, fetching all records from the model's table. Returns a list of objects
|`first()`  ||Connect to a database named <dbname>
---
## Filtering
| Function | Example | Notes |
| :---: |:---: | ---- |
|`filter_by()` |`MyModel.query.filter_by(attr='some value')`|Similar to SELECT * from ... WHERE
|`filter()`    |`MyModel.query.filter(MyOtherModel.some_attr='some value')`|Similar to filter_by , but instead, you specify attributes on a given Model.
|`like()`   ||
|`ilike()`  ||


>Cheat Sheet: https://video.udacity-data.com/topher/2019/August/5d5a52af_query-cheat-sheet/query-cheat-sheet.pdf
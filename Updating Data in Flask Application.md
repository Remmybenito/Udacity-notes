# Updating Data in a Flask Application
An **update** involves setting the attributes of an existing object in the database.

In SQL:
```SQL
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

in SQLAlchemy ORM:
```python
user = User.query.get(some_id)
user.name = 'Some new name'
db.session.commit()
```

### Modifying the view in HTML for updating To-Do List Items


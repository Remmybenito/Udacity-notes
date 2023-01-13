# SQLAlchemy DB commands

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
Creates tables based on the db.Model that was configured with the associated table. In this case of db.Model created above, it will create the table ‘persons’ with all of the data we initialized in our class above.
# Migrations Basics
**Migrations** deal with how we manage modifications to our data schema over time. A migration is a file that keeps track of changes to our database schema (structure of our database).

##### Upgrades and Rollbacks. 
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

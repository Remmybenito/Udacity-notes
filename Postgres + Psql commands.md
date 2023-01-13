# Postgres / Psql

### Postgres server commands - command line

Start / stop / restart a Postgres server on local machine by directing to local installation \data folder 

```markdown
pg_ctl -D "C:\Program Files\PostgreSQL\15\data" start
```
```markdown
pg_ctl -D "C:\Program Files\PostgreSQL\15\data" stop
```
```markdown
pg_ctl -D "C:\Program Files\PostgreSQL\15\data" restart
```

>Note: These commands will start the postgres server in which we can run psql commands with. The server must be started in the above folder on a local computer in order to function.

### Psql commands - cmd

>Note:  This will access the running server as user ‘postgres’. Password will be requested after this command is run. Default password is “password”

List all databases on the server, their owners, and user access levels
```markdown
# \l

Connect to a database named <dbname>
# \c <dbname>

Show database tables
# \dt

Describe table schema
# \d <tablename>

Quit psql, returning to terminal
# \q

Get help, see list of available commands
# \?
```

### Breaking Changes

- A complete list of breaking changes (preferably there are none, unless this is a major version).
- List out, as concretely as possible, any steps users have to take when they upgrade beyond just dumping the dependency.
- Write pseudocode that highlights what code should change and how.
- Call out if users are recommended to upgrade because of known problems with older releases.
- Preferably, there's nothing here.

### New Features

- Describe the new feature and when/why to use it. Add some pictures! Call out any caveats/warnings? Is it a beta feature?

### Bug Fixes

- Call out any existing feature/functionality that now works as intended or expected.

### Improvements

- Improvements/enhancements to a workflow, performance, logging, error messaging, or user experience

### Other Changes

- Other miscellaneous changes that don't fit into any of the above categories. Try to leave this empty - ideally, all changes fit into the categories above

------

#### Copy and paste this template

```markdown
## [0.0.2](https://github.com/andreasonny83/twilio-remote-cli/compare/v0.0.1...v0.0.2) (2019-07-21)

> Description

### Upgrade Steps
* [ACTION REQUIRED]
* 

### Breaking Changes
* 
* 

### New Features
* 
* 

### Bug Fixes
* 
* 

### Performance Improvements
* 
* 

### Other Changes
* 
* 
```

Example:

```markdown
## [0.5.2](https://github.com/andreasonny83/twilio-remote-cli/compare/v0.5.1...v0.5.2) (2019-07-21)

### Performance Improvements

* **dependencies:** Bump dependencies  4a4ee13

### Other Changes

* **chore(conventionalChangelog):** Add Conventional Changelog  aafcdd9
* **docs(CHANGELOG):** Add changelog  e2c7435
```
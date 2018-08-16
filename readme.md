# postgres-1-psql
## Setup
1. Install PostgreSQL
2. Verify `psql` is accessible via command line

        psql --version
3. If `psql` isn't found, add the path to the PostgreSQL `bin` folder to your `PATH` environment variable (actual paths may differ)

    Windows: Add `C:\Program Files\PostgreSQL\9.6\bin` to user `Path` via System Properties

    OSX: Add `export PATH=$PATH:/Library/PostgreSQL/9.6/bin` to `~/.bash_profile`

4. Configure the default username if necessary

    https://www.postgresql.org/docs/current/static/libpq-envars.html

    By default psql uses your computer user name as the default user name for database connections.
    If you entered a different user name when installing PostgreSQL you can change the default by setting the
    `PGUSER` environment variable.

    Windows: Add new `PGUSER` variable to user variables via System Properties with the default user name as the value

    OSX: Add `export PGUSER={USER_NAME}` to `~/.bash_profile` where `{USER_NAME}` is the new default

5. Configure the default password

    https://www.postgresql.org/docs/current/static/libpq-pgpass.html

    Create the following file and add the line `localhost:5432:*:{USER_NAME}:{PASSWORD}` where `{USER_NAME}` and `{PASSWORD}`
    are the defaults that you would like `psql` to use

    Windows: `%APPDATA\postgresql\pgpass.conf`

    OSX: `~/.pgpass`

6. Verify everything is working by creating, listing and dropping a database

        psql --command='CREATE DATABASE test;'
        > CREATE DATABASE

        psql --command='\list'
        > List of databases
        Name     |  Owner   | Encoding |          Collate           |           Ctype            |   Access privileges
        ------+----------+----------+----------------------------+----------------------------+-----------------------
        test | postgres | UTF8     | English_United States.1252 | English_United States.1252 |

        psql --command='DROP DATABASE test;'
        > DROP DATABASE

## Notes
- The full `psql` documentation is available here: https://www.postgresql.org/docs/current/static/app-psql.html
- `psql` also has an interactive mode that can be entered by running `psql` without `command` or `file` arguments
- `--command=\list` is an example of using a meta-command instead of SQL
- Database-level commands require the `--dbname` parameter to be present

    Example: `psql --dbname='test' --command='CREATE TABLE item (id int PRIMARY KEY)'`
# Database.py for PostgreSQL

This `database.py` can be directly used with your PostgreSQL connection.

If you want to learn more about Python and PostgreSQL, our [comprehensive course](https://www.udemy.com/the-complete-python-postgresql-developer-course/?couponCode=GITHUB) is a great place to start.

## Usage

The first thing to do is initialise the database, which starts all the connections to your database server.

We use connection pooling so that whenever you want to execute a query against your database, you can have a connection ready without having to create it on the fly. Creating connections takes slightly longer than using them, so having a pool of connections ready to go can be very useful.

By default, we create 10 connections when you initialise your database. You can edit this to an appropriate number for your deployment (which will depend, amongst other things, on the amount of RAM on your database server).

Once the database is initialised, use `CursorFromConnectionPool` to get a new connection out of the pool and a cursor from it.

When the context manager ends, the connection will automatically be committed for you. If you do not want this, you can always get and return connections from the database manually.

### Get a cursor from the connection pool

```python
from database import Database, CursorFromConnectionPool

Database.initialise(
    host='localhost'
    database='testdb'
    user='youruser'
    password='yourpw'
)

with CursorFromConnectionPool() as cursor:
    cursor.execute('SELECT * FROM users')
    rows = cursor.fetchall()
    print(rows)
```

### Get a connection manually from the pool

```python
from database import Database

Database.initialise(
    host='localhost'
    database='testdb'
    user='youruser'
    password='yourpw'
)

conn = Database.get_connection()
cursor = conn.cursor()
cursor.execute('SELECT * FROM users')
rows = cursor.fetchall()
print(rows)
cursor.close()
Database.return_connection(conn)
```
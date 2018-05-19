# Database.py for PostgreSQL

This `database.py` can be directly used with your PostgreSQL connection.

## Usage

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
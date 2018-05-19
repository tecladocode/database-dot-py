- [Database.py for MongoDB](#databasepy-for-mongodb)
    - [Usage](#usage)
    - [Interface](#interface)
        - [`insert`](#insert)
        - [`find`](#find)
        - [`find_one`](#find_one)
        - [`update`](#update)
        - [`remove`](#remove)

# Database.py for MongoDB

This `database.py` can be directly used with your PostgreSQL connection.

If you want to learn more about Python and MongoDB, our [Python Web Course](https://www.udemy.com/the-complete-python-web-course-learn-by-building-8-apps/?couponCode=GITHUB) is a great place to start.

## Usage

Usage of this `database.py` is simple. Before using, initialise the library connection. Then, use the provided interface to interact with MongoDB.

Before initialising make sure to have exported a `MONGODB_URI` environment variable. For a local server, this would be `mongodb://localhost:27017

```python
from database import Database

Database.inititialise()

Database.insert(
    collection='users',
    data={
        'username': 'jose',
        'password': '123'
    })
```

## Interface

Available methods are:

- [`insert(collection, data)`](#insert)
- [`find(collection, query)`](#find)
- [`find_one(collection, query)`](#find_one)
- [`update(collection, query, data)`](#update)
- [`remove(collection, query)`](#remove)

### `insert`

To insert a new user in a collection `'users'`, with username `'jose'` and password `'123'`.

```python
from database import Database

Database.initialise()

Database.insert(
    collection='users',
    data={
        'username': 'jose',
        'password': '123'
    })
```

### `find`

To find all users created before or exactly on timestamp `'1524754833'`.

```python
from database import Database

Database.initialise()

Database.find(
    collection='users',
    query={'created': { '$lte': '1524754833'}})
```

### `find_one`

This retrieves the top element from the collection matching the query.

To find one user with username `'jose'`.

```python
from database import Database

Database.initialise()

Database.find_one(
    collection='users',
    query={'username': 'jose'})
```

### `update`

To update the user with username `'jose'` to having username `'rolf'`.

```python
from database import Database

Database.initialise()

Database.update(
    collection='users',
    query={'username': 'jose'},
    data={'username': 'rolf'})
```

### `remove`

To remote a user with username `'jose'`.

```python
from database import Database

Database.initialise()

Database.remove(
    collection='users',
    query={'username': 'jose'})
```

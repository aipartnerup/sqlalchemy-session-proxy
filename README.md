# sqlalchemy-session-proxy

A lightweight proxy for SQLAlchemy sessions that seamlessly supports both synchronous (`Session`) and asynchronous (`AsyncSession`) usage. This library provides a unified interface to interact with SQLAlchemy sessions, making it easy to write code that works in both sync and async environments.

## Features

- **Unified API**: Use the same methods for both sync and async SQLAlchemy sessions.
- **Automatic Async Detection**: Automatically detects if the session is async and dispatches calls accordingly.
- **Proxy Pattern**: Forwards all attribute and method calls to the underlying session.
- **Supports Core Session Methods**: Includes common session operations like `add`, `commit`, `rollback`, `execute`, `scalars`, `get`, `merge`, and more.
- **Type Hints**: Fully type-annotated for better IDE support and static analysis.

## Installation

```bash
pip install sqlalchemy-session-proxy
```

## Usage

```python
from sqlalchemy.orm import Session
from sqlalchemy.ext.asyncio import AsyncSession
from session_proxy import SqlalchemySessionProxy

# For synchronous session
sync_session = Session(...)
proxy = SqlalchemySessionProxy(sync_session)

# For asynchronous session
async_session = AsyncSession(...)
proxy = SqlalchemySessionProxy(async_session)

# Use proxy in your code
data = proxy.execute(statement)
# or, in async context:
data = await proxy.execute(statement)
```

## Example: Unified Session Usage

```python
from sqlalchemy.orm import Session
from sqlalchemy.ext.asyncio import AsyncSession
from session_proxy import SqlalchemySessionProxy

# Synchronous usage
session = Session(...)
proxy = SqlalchemySessionProxy(session)
proxy.add(obj)
proxy.commit()

# Asynchronous usage
async def main():
    async_session = AsyncSession(...)
    proxy = SqlalchemySessionProxy(async_session)
    await proxy.add(obj)
    await proxy.commit()
```

## API Overview

- `SqlalchemySessionProxy(session)` — Initialize with a `Session` or `AsyncSession`.
- `.is_async` — Returns `True` if using `AsyncSession`.
- `.session` — Access the underlying session object.
- Methods: `add`, `add_all`, `commit`, `rollback`, `close`, `flush`, `merge`, `delete`, `get`, `get_one`, `execute`, `scalars`, `refresh`, `expire`, `expire_all`, `expunge`, `expunge_all`, `is_modified`, `in_transaction`, `in_nested_transaction`, and more.

All methods are automatically dispatched to the correct sync/async implementation.

## API Summary

| Method                | Sync | Async | Description                                      |
|----------------------|------|-------|--------------------------------------------------|
| `add`                | ✔️   | ✔️    | Add an object to the session                     |
| `add_all`            | ✔️   | ✔️    | Add multiple objects                             |
| `commit`             | ✔️   | ✔️    | Commit the transaction                           |
| `rollback`           | ✔️   | ✔️    | Rollback the transaction                         |
| `close`              | ✔️   | ✔️    | Close the session                                |
| `flush`              | ✔️   | ✔️    | Flush changes to the database                    |
| `merge`              | ✔️   | ✔️    | Merge an object                                  |
| `delete`             | ✔️   | ✔️    | Mark an object as deleted                        |
| `get`                | ✔️   | ✔️    | Get object by primary key                        |
| `get_one`            | ✔️   | ✔️    | Get one object or raise if not found             |
| `execute`            | ✔️   | ✔️    | Execute a statement                              |
| `scalars`            | ✔️   | ✔️    | Execute and return scalar results                |
| `refresh`            | ✔️   | ✔️    | Refresh an object from the database              |
| `expire`             | ✔️   | ✔️    | Expire attributes on an object                   |
| `expire_all`         | ✔️   | ✔️    | Expire all objects in the session                |
| `expunge`            | ✔️   | ✔️    | Remove an object from the session                |
| `expunge_all`        | ✔️   | ✔️    | Remove all objects from the session              |
| `is_modified`        | ✔️   | ✔️    | Check if object is modified                      |
| `in_transaction`     | ✔️   | ✔️    | Check if a transaction is in progress            |
| `in_nested_transaction` | ✔️ | ✔️    | Check if a nested transaction is in progress     |

See the source code for the full list and details.

## License

Apache-2.0

## Author

Tercel (<tercel.yi@gmail.com>)

## [0.2.0] - 2026-01-19

### Added
- Added `query` method for legacy ORM queries (sync/async).
- Added `scalar` method for executing statements and returning a single scalar result (sync/async).
- Added `run_sync` method to allow running synchronous functions in async context (AsyncSession only).
- Updated README.md to document new methods and clarify usage and import paths.


## [0.1.0] - 2026-01-18

### Added
- Initial release of `sqlalchemy-session-proxy`.
- Unified proxy for both synchronous (`Session`) and asynchronous (`AsyncSession`) SQLAlchemy sessions.
- Automatic detection and dispatch for sync/async session methods.
- Proxy pattern: forwards all attribute and method calls to the underlying session.
- Supports core session methods: `add`, `add_all`, `commit`, `rollback`, `close`, `flush`, `merge`, `delete`, `get`, `get_one`, `execute`, `scalars`, `refresh`, `expire`, `expire_all`, `expunge`, `expunge_all`, `is_modified`, `in_transaction`, `in_nested_transaction`, and more.
- Full type hints for better IDE support and static analysis.

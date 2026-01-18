## [0.1.0] - 2026-01-18

### Added
- Initial release of `sqlalchemy-session-proxy`.
- Unified proxy for both synchronous (`Session`) and asynchronous (`AsyncSession`) SQLAlchemy sessions.
- Automatic detection and dispatch for sync/async session methods.
- Proxy pattern: forwards all attribute and method calls to the underlying session.
- Supports core session methods: `add`, `add_all`, `commit`, `rollback`, `close`, `flush`, `merge`, `delete`, `get`, `get_one`, `execute`, `scalars`, `refresh`, `expire`, `expire_all`, `expunge`, `expunge_all`, `is_modified`, `in_transaction`, `in_nested_transaction`, and more.
- Full type hints for better IDE support and static analysis.

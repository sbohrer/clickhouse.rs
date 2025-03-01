# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.10.0] - 2022-01-18
### Added
- client: `Client::with_http_client` to use custom `hyper::Client`, e.g. for https ([@iwinux](https://github.com/iwinux)).

### Changed
- watch: run `WATCH` queries with `max_execution_time=0`.
- bind: implement `Bind` for all `Serialize` instances, [#33](https://github.com/loyd/clickhouse.rs/issues/33).

### Fixed
- Implement `Primitive` for `f64`, [#31](https://github.com/loyd/clickhouse.rs/issues/31).

## [0.9.3] - 2021-12-21
### Added
- Implement `Primitive` for `f64` and `f32`, [#29](https://github.com/loyd/clickhouse.rs/issues/29).

### Fixed
- Reset quantities on errors to support reusing `Inserter` after errors ([@00nktk](https://github.com/00nktk)).

## [0.9.2] - 2021-11-01
### Changed
- HTTP Keep-alive timeout is restricted to 2s explicitly.

### Fixed
- watch: make a cursor cancellation safe.

## [0.9.1] - 2021-10-25
### Added
- mock: add `record_ddl` handler to test DDL queries.
- mock: add `watch` and `watch_only_events` handlers to test WATCH queries.

## [0.9.0] - 2021-10-25
### Fixed
- query: support borrowed long strings, [#22](https://github.com/loyd/clickhouse.rs/issues/22).
- query: read the whole response of DDL queries.

### Changed
- **BREAKING**: watch: require the `watch` feature.
- **BREAKING**: watch: only struct rows are allowed because JSON requires names.
- query: queries with invalid URLs fail with `Error::InvalidParams`.
- watch: use `JSONEachRowWithProgress` because of [the issue](https://github.com/ClickHouse/ClickHouse/issues/22996), [#23](https://github.com/loyd/clickhouse.rs/issues/23).

## [0.8.1] - 2021-08-26
### Fixed
- Support `?` inside bound arguments, [#18](https://github.com/loyd/clickhouse.rs/issues/18).
- Use the `POST` method if a query is bigger than 8KiB, [#19](https://github.com/loyd/clickhouse.rs/issues/19).

## [0.8.0] - 2021-07-28
### Fixed
- `RowBinarySerializer::is_human_readable()` returns `false`.

## [0.7.2] - 2021-05-07
### Added
- `Watch::refresh()` to specify `REFRESH` clause.

### Fixed
- `derive(Row)`: handle raw identifiers.

## [0.7.1] - 2021-06-29
### Fixed
- Get rid of "socket is not connected" errors (found by [@let4be](https://github.com/let4be)).

### Changed
- Set TCP keepalive to 60 seconds.

## [0.7.0] - 2021-05-31
### Changed
- Replace `reflection::Reflection` with `clickhouse::Row`. It's enough to implement `Row` for top-level `struct`s only.

### Added
- `#[derive(Row)]`

## [0.6.8] - 2021-05-28
### Fixed
- docs: enable the `doc_cfg` feature.

## [0.6.7] - 2021-05-28
### Fixed
- docs: show features on docs.rs.
- Now `test-util` implies `hyper/server`.

## [0.6.6] - 2021-05-28
### Added
- `test` module (available with the `test-util` feature).
- `#[must_use]` for `Query`, `Watch`, `Insert` and `Inserter`.

## [0.6.5] - 2021-05-24
### Added
- `&String` values binding to SQL queries.

## [0.6.4] - 2021-05-14
### Fixed
- Depend explicitly on `tokio/macros`.

## [0.6.3] - 2021-05-11
### Added
- Support for `bool` values storage ([@quasiyoke](https://github.com/quasiyoke)).
- `array`s' binding to SQL queries — useful at [`IN` operators](https://clickhouse.tech/docs/en/sql-reference/operators/in/), [etc](https://clickhouse.tech/docs/en/sql-reference/functions/array-functions/) ([@quasiyoke](https://github.com/quasiyoke)).
- `String` values binding to SQL queries ([@quasiyoke](https://github.com/quasiyoke)).
- `Query::fetch_all()`
- `sql::Identifier`

### Changed
- Expose `query::Bind` ([@ods](https://github.com/ods)).
- Deprecate `Compression::encoding()`.

## [0.6.2] - 2021-04-12
### Fixed
- watch: bind fileds of the type param.

## [0.6.1] - 2021-04-09
### Fixed
- compression: decompress error messages ([@ods](https://github.com/ods)).

## [0.6.0] - 2021-03-24
### Changed
- Use tokio v1, hyper v0.14, bytes v1.

## [0.5.1] - 2020-11-22
### Added
- Decompression: lz4.

## [0.5.0] - 2020-11-19
### Added
- Decompression: gzip, zlib and brotli.

## [0.4.0] - 2020-11-17
### Added
- `Query::fetch_one()`, `Watch::fetch_one()`.
- `Query::fetch()` as a replacement for `Query::rows()`.
- `Watch::fetch()` as a replacement for `Watch::rows()`.
- `Watch::only_events().fetch()` as a replacement for `Watch::events()`.

### Changed
- `Error` is `StdError + Send + Sync + 'static` now.

## [0.3.0] - 2020-10-28
### Added
- Expose cursors (`query::RowCursor`, `watch::{RowCursor, EventCursor}`).

## [0.2.0] - 2020-10-14
### Added
- `Client::inserter()` for infinite inserting into tables.
- `Client::watch()` for `LIVE VIEW` related queries.

### Changed
- Renamed `Query::fetch()` to `Query::rows()`.
- Use `GET` requests for `SELECT` statements.

## [0.1.0] - 2020-10-14
### Added
- Support basic types.
- `Client::insert()` for inserting into tables.
- `Client::query()` for selecting from tables and DDL statements.

[unreleased]: https://github.com/loyd/clickhouse.rs/compare/v0.10.0...HEAD
[0.10.0]: https://github.com/loyd/clickhouse.rs/compare/v0.9.3...v0.10.0
[0.9.3]: https://github.com/loyd/clickhouse.rs/compare/v0.9.2...v0.9.3
[0.9.2]: https://github.com/loyd/clickhouse.rs/compare/v0.9.1...v0.9.2
[0.9.1]: https://github.com/loyd/clickhouse.rs/compare/v0.9.0...v0.9.1
[0.9.0]: https://github.com/loyd/clickhouse.rs/compare/v0.8.1...v0.9.0
[0.8.1]: https://github.com/loyd/clickhouse.rs/compare/v0.8.0...v0.8.1
[0.8.0]: https://github.com/loyd/clickhouse.rs/compare/v0.7.2...v0.8.0
[0.7.2]: https://github.com/loyd/clickhouse.rs/compare/v0.7.1...v0.7.2
[0.7.1]: https://github.com/loyd/clickhouse.rs/compare/v0.7.0...v0.7.1
[0.7.0]: https://github.com/loyd/clickhouse.rs/compare/v0.6.8...v0.7.0
[0.6.8]: https://github.com/loyd/clickhouse.rs/compare/v0.6.7...v0.6.8
[0.6.7]: https://github.com/loyd/clickhouse.rs/compare/v0.6.6...v0.6.7
[0.6.6]: https://github.com/loyd/clickhouse.rs/compare/v0.6.5...v0.6.6
[0.6.5]: https://github.com/loyd/clickhouse.rs/compare/v0.6.4...v0.6.5
[0.6.4]: https://github.com/loyd/clickhouse.rs/compare/v0.6.3...v0.6.4
[0.6.3]: https://github.com/loyd/clickhouse.rs/compare/v0.6.2...v0.6.3
[0.6.2]: https://github.com/loyd/clickhouse.rs/compare/v0.6.1...v0.6.2
[0.6.1]: https://github.com/loyd/clickhouse.rs/compare/v0.6.0...v0.6.1
[0.6.0]: https://github.com/loyd/clickhouse.rs/compare/v0.5.1...v0.6.0
[0.5.1]: https://github.com/loyd/clickhouse.rs/compare/v0.5.0...v0.5.1
[0.5.0]: https://github.com/loyd/clickhouse.rs/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/loyd/clickhouse.rs/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/loyd/clickhouse.rs/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/loyd/clickhouse.rs/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/loyd/clickhouse.rs/releases/tag/v0.1.0

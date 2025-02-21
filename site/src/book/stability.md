# Stability policy

This section contains information on how cargo-nextest will evolve in a backwards-compatible way over time.

## The cargo-nextest binary

The cargo-nextest binary follows [semantic versioning](https://semver.org/), where the [public API](https://semver.org/#spec-item-1) consists of exactly the following:

1. command-line arguments, options and flags
2. [machine-readable output](machine-readable.md)
3. the [configuration file format](configuration.md)

[Experimental features](experimental-features.md) are not part of the public API. They may change or be removed in a patch release.

Within a version series, the public API will be append-only. New options or keys may be added, but existing keys will continue to be as they were. Existing options may be deprecated but will not be removed within a version series.

The public API does _not_ include human-readable output generated by nextest, or in general anything printed to stderr.

## Libraries

The libraries used by cargo-nextest, [nextest-metadata](https://crates.io/crates/nextest-metadata) and [nextest-runner](https://crates.io/crates/nextest-runner), follow the standard Rust library versioning policy.

### nextest-metadata

nextest-metadata contains data structures for deserializing cargo-nextest's [machine-readable output](machine-readable.md).

**nextest-metadata is forward-compatible with cargo-nextest**. A given version of nextest-metadata will continue to work with all future versions of cargo-nextest (within the same version series).

However, currently, **nextest-metadata is not backwards-compatible**: a new version of nextest-metadata may not be able to parse metadata generated by older versions of cargo-nextest. In other words, each version of nextest-metadata has a minimum supported cargo-nextest version, analogous to a crate's [minimum supported Rust version (MSRV)](https://rust-lang.github.io/rfcs/2495-min-rust-version.html).

A bump to the minimum supported cargo-nextest version is considered a breaking change, and will be paired with a major version bump.

(The policy around backwards compatibility may be relaxed in the future based on user needs.)

### nextest-runner

nextest-runner is built to serve the needs of cargo-nextest. Every `cargo-nextest` release is likely to correspond to a breaking change to nextest-runner.

## Minimum supported Rust version (MSRV)

The MSRV of cargo-nextest or dependent crates may be changed in a patch release. At least the last 3 versions of Rust will be supported at any time.

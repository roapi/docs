# Installation

## Pre-built binary

Platform specific pre-built binaries for each release is hosted on our [Github
release page](https://github.com/roapi/roapi/releases).

You can download and install them with a signle command using pip:

```bash
pip install roapi-http
```

## Docker

Pre-built docker images are hosted at
[ghcr.io/roapi/roapi-http](https://github.com/orgs/roapi/packages/container/package/roapi-http).


## Build from source

You need to install [Rust toolchain](https://rustup.rs/) if you haven't done so.

```bash
cargo install --locked --git https://github.com/roapi/roapi --branch main --bin roapi-http
```

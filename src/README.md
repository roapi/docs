# ROAPI Documentation

[![Project repository](https://img.shields.io/badge/repo-github-blue)](https://github.com/roapi/roapi)

[ROAPI](https://github.com/roapi/roapi) automatically spins up read-only APIs
for static datasets without requiring you to write a single line of code. It
builds on top of [Apache Arrow](https://github.com/apache/arrow) and
[Datafusion](https://github.com/apache/arrow/tree/master/rust/datafusion). The
core of its design can be boiled down to the following:

* Query frontends to translate SQL, GraphQL and REST API queries into
Datafusion plans.
* Datafusion for query plan execution.
* Data layer to load datasets from a variety of sources and formats with
automatic schema inference.
* Response encoding layer to serialize intermediate Arrow record batch into
various formats requested by client.

See below for a high level diagram:

<img alt="roapi-design-diagram" src="./images/roapi.svg">

> If you'd like to share feedback on how you're using ROAPI, please [fill out this survey](https://docs.google.com/forms/d/1M1s1scZX39UouuVF8WzIFQoSyeKX5dMVQgQMtYJKGZU). Thanks!
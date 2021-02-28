# Blob store

ROAPI currently supports the following blob storages:

* Filesystem
* HTTP/HTTPS
* S3 (WIP)

## Filesystem

Uri without a scheme prefix is treated as filesystem backed data source by
ROAPI. For example, to serve a local parquet file `test_data/blogs.parquet`, you
can just set the uri to the file path.

Filesystem store supports loading partitioned tables. In other words, you can
split up the table into mulitple files and load all of them into a single table
by setting uri to the directory path.


## HTTP/HTTPS

ROAPI can build tables from datasets served through HTTP protocols. However, one
thing to keep in mind is HTTP store doesn't support partitioned datasets because
there is no native directory support in HTTP.

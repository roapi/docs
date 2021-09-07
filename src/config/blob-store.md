# Blob store

ROAPI currently supports the following blob storages:

* Filesystem
* HTTP/HTTPS
* S3

## Filesystem

Filesystem store can be specified using `file:` or `filesystem:` schemes.  In a
Windows environment, the scheme is mandatory.  On Unix systems, a uri without a
scheme prefix is treated as filesystem backed data source by ROAPI. 

For example, to serve a local parquet file `test_data/blogs.parquet`, you can
just set the uri to the file path:

```yaml
tables:
  - name: "blogs"
    uri: "test_data/blogs.parquet"
```

Filesystem store supports loading partitioned tables. In other words, you can
split up the table into mulitple files and load all of them into a single table
by setting uri to the directory path. When loading a partitioned dataset, you
will need to manually specify table format since the uri will not contain table
format as a suffix:

```yaml
tables:
  - name: "blogs"
    uri: "test_data/blogs/"
    option:
        format: "parquet"
```


## HTTP/HTTPS

ROAPI can build tables from datasets served through HTTP protocols. However, one
thing to keep in mind is HTTP store doesn't support partitioned datasets because
there is no native directory support in HTTP protocol.


## S3

ROAPI can build tables from datasets hosted in S3 buckets. Configuration is
similar to filesystem store:

```yaml
tables:
  - name: "TABLE_NAME"
    uri: "s3://BUCKET/TABLE/KEY"
    option:
        format: "csv"
```

Note that AWS region needs to be manually specified through `AWS_REGION`
environment variable.

To configure S3 credentials, you can use IAM role or set the following
environment variables if you are using IAM user:

* `AWS_SECRET_ACCESS_KEY`
* `AWS_ACCESS_KEY_ID`

# Parquet

When a table uri ends in `.parquet`, ROAPI will try to load it as Parquet table if no
`format` option is specified:

```yaml
tables:
  - name: "mytable"
    uri: "http://mytable.parquet"
```

You can partition a Parquet dataset into multiple partitions and load all of them
into a single table by directory path:

```yaml
tables:
  - name: "mytable"
    uri: "./table_dir"
    option:
      format: "parquet"
```

## Large Datasets

ROAPI loads the entire table into memory as the default behavior.  If your
table is large or you want to avoid loading all data during startup, you can
set an additional option `use_memory_table: false` (default: `true`). With that
configuration, ROAPI will not copy the data into memory, but instructs datafusion
to directly operate on the backing storage.

At the moment, this comes with the following limitations:

1. no nested schema: [datafusion#83](https://github.com/apache/arrow-datafusion/issues/83)
2. missing support for cloud storage: [datafusion#616](https://github.com/apache/arrow-datafusion/issues/616)

Example:

```yaml
tables:
  - name: "mytable"
    uri: "./table_dir"
    option:
      format: "parquet"
      use_memory_table: false
```

Note that when providing `use_memory_table` option, it becomes necessary to
also specify the format.

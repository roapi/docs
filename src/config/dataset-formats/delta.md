# Delta Lake

ROAPI supports loading Delta tables from [Delta Lake](https://delta.io/)
through [delta-rs](https://github.com/delta-io/delta-rs). Since a Delta table
doesn't have an extension suffix, ROAPI cannot infer table format from table
URI alone.  Therefore, the `format` option needs to be set to `delta`
explicitly for Delta table sources:

```yaml
tables:
  - name: "mytable"
    uri: "s3://bucket/delta_table/path"
    option:
      format: "delta"
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
    uri: "./path/to/delta_table"
    option:
      format: "delta"
      use_memory_table: false
```

Note that when providing `use_memory_table` option, it becomes necessary to
also specify the format.

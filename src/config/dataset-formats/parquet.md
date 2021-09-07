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

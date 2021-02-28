# CSV

When a table uri ends in `.csv`, ROAPI will try to load it as CSV table if no
`format` option is specified:

```yaml
tables:
  - name: "mytable"
    uri: "http://mytable.csv"
```

You can partition a CSV dataset into multiple partitions and load all of them
into a single table by directory path:

```yaml
tables:
  - name: "mytable"
    uri: "./table_dir"
    option:
      format: "csv"
```

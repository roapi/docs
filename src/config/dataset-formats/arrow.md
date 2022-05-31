# Arrow

When a table uri ends in `.arrow` or `.arrows`, ROAPI will try to load it as
Arrow IPC file or stream if no `format` option is specified:

```yaml
tables:
  - name: "mytable"
    uri: "http://mytable.arrow" # or .arrows
```


You can partition an Arrow dataset into multiple partitions and load all of them
into a single table by directory path:

```yaml
tables:
  - name: "mytable"
    uri: "./table_dir"
    option:
      format: "arrow" # or arrows
```

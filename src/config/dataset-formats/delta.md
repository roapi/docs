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

# NDJSON

[NDJSON](http://ndjson.org/) stands for Newline delimited JSON. It is a
convenient format for storing or streaming structured data that may be
processed one record at a time.

When a table uri ends in `.ndjson`, ROAPI will try to load it as NDJSON table
if no `format` option is specified:

```
tables:
  - name: "mytable"
    uri: "http://mytable.ndjson"
```

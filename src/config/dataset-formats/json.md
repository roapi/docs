# JSON

When a table uri ends in `.json`, ROAPI will try to load it as JSON table if no
`format` option is specified:

```yaml
tables:
  - name: "mytable"
    uri: "http://mytable.json"
```

## Filter by JSON pointer

Sometimes the JSON array you want to serve might be stored inside a JSON
object. To support this use-case, ROAPI supports loading JSON using a [JSON
pointer](https://tools.ietf.org/html/rfc6901).

Take the following JSON data as an example:

```json
{
    "x": {
        "y": [{"col1": "z"}, {"col1": "zz"}]
    }
}
```

In order to only serve `[{"col1": "z"}, {"col1": "zz"}]` through ROAPI, you can
configure the JSON table source as:

```yaml
tables:
  - name: "mytable"
    uri: "http://mytable.json"
    option:
      format: "json"
      pointer: "/x/y"
```


## Array encoding

Each row in JSON data can be encoded using array for size reduction. This
convention allows us to avoid repeating column names in every row.

For example:

```json
[
    {"col1": 1, "col2": "abc"},
    {"col1": 2, "col2": "efg"}
]
```

Can be stored as:


```json
[
    [1, "abc"],
    [2, "efg"]
]
```

When loading JSON rows using array encoding, one needs to explicily specify the
schema since there is no column name in the datasource anymore for ROAPI to
perform the schema inference:

```yaml
tables:
  - name: "mytable"
    uri: "http://mytable.json"
    option:
      format: "json"
      array_encoded: true
    schema:
      columns:
        - name: "col1"
          data_type: "Int64"
        - name: "col2"
          data_type: "Utf8"
```

# REST

Query tables through REST API by sending `GET` requests to
`/api/tables/{table_name}`. Query operators are specified as query params.

REST query frontend currently supports the following query operators:

* columns
* sort
* limit
* filter

To sort column `col1` in ascending order and `col2` in descending order, set
query param to: `sort=col1,-col2`.

To find all rows with `col1` equal to string `'foo'`, set query param to:
`filter[col1]='foo'`. You can also do basic comparisons with filters, for
example predicate `0 <= col2 < 5` can be expressed as
`filter[col2]gte=0&filter[col2]lt=5`.

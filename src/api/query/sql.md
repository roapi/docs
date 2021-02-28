# SQL

To query tables using a subset of standard SQL, send the query payload through
`POST` request to `/api/sql` endpoint. This is the only query interface that
supports table joins.

SQL query frontend is the more flexible and powerful compared to
[REST](rest.html) and [GraphQL](graphql.html). It is the only query frontend
that supports table joins.

# GraphQL

To query tables through GraphQL, send the query through `POST` request to
`/api/graphql` endpoint.

GraphQL query frontend supports the same set of operators supported by [REST
query frontend](rest.html). Here how is you can apply various operators in a query:

```graphql
{
    table_name(
        filter: {
            col1: false
            col2: { gteq: 4, lt: 1000 }
        }
        sort: [
            { field: "col2", order: "desc" }
            { field: "col3" }
        ]
        limit: 100
    ) {
        col1
        col2
        col3
    }
}
```

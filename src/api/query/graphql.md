# GraphQL

To query tables through GraphQL, send the query through `POST` request to
`/api/graphql` endpoint.

GraphQL query interface supports the same set of operators supported by REST
API. Here how you can apply various operators to your query:

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

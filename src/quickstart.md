# Quick start

Spin up APIs for `test_data/uk_cities_with_headers.csv` and
`test_data/spacex-launches.json`:

```bash
roapi-http \
    --table 'uk_cities:test_data/uk_cities_with_headers.csv' \
    --table 'spacex_launches:test_data/spacex-launches.json'
```

## Query API

Query tables using SQL, GraphQL or REST:

```bash
curl -X POST -d "SELECT city, lat, lng FROM uk_cities LIMIT 2" localhost:8080/api/sql
curl -X POST -d "query { uk_cities(limit: 2) {city, lat, lng} }" localhost:8080/api/graphql
curl "localhost:8080/api/tables/uk_cities?columns=city,lat,lng&limit=2"
```

Sample response:

```json
[
  {
    "city": "Elgin, Scotland, the UK",
    "lat": 57.653484,
    "lng": -3.335724
  },
  {
    "city": "Stoke-on-Trent, Staffordshire, the UK",
    "lat": 53.002666,
    "lng": -2.179404
  }
]
```

See [Query frontends](api/query) for details on different operators supported
by each frontend.


## Schema API

Get inferred schema for all tables:

```bash
curl localhost:8080/api/schema
```

Sample response:

```json
{
  "uk_cities": {
    "fields": [
      {
        "name": "city",
        "data_type": "Utf8",
        "nullable": false,
        "dict_id": 0,
        "dict_is_ordered": false
      },
      {
        "name": "lat",
        "data_type": "Float64",
        "nullable": false,
        "dict_id": 0,
        "dict_is_ordered": false
      },
      {
        "name": "lng",
        "data_type": "Float64",
        "nullable": false,
        "dict_id": 0,
        "dict_is_ordered": false
      }
    ]
  }
}
```

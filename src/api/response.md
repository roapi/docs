# Response serialization

By default, ROAPI encodes responses in JSON format, but you can request
different encodings by specifying the `ACCEPT` header:

```bash
curl -X POST \
    -H 'ACCEPT: application/vnd.apache.arrow.stream' \
    -d "SELECT launch_library_id FROM spacex_launches WHERE launch_library_id IS NOT NULL" \
    localhost:8080/api/sql
```

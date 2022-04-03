# Key value lookup

Query key value stores through REST API by sending `GET` requests to
`/api/kv/{kv_name}/{key}`.

For example, the kvstore defined in [the sample
config](/config/config-file.html#key-value-stores) can be queried like below:

```bash
$ curl -v localhost:8080/api/kv/spacex_launch_name/600f9a8d8f798e2a4d5f979e
Starlink-21 (v1.0)%
```

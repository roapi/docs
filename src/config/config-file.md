# YAML config

## Tables

You can configure multiple table sources using YAML config, which supports more
advanced format specific table options. For example:

```yaml
addr:
  # binding address for TCP port that speaks HTTP protocol
  http: 0.0.0.0:8084
  # binding address for TCP port that speaks Postgres wire protocol
  postgres: 0.0.0.0:5432
tables:
  - name: "blogs"
    uri: "test_data/blogs.parquet"

  - name: "ubuntu_ami"
    uri: "test_data/ubuntu-ami.json"
    option:
      format: "json"
      pointer: "/aaData"
      array_encoded: true
    schema:
      columns:
        - name: "zone"
          data_type: "Utf8"
        - name: "name"
          data_type: "Utf8"
        - name: "version"
          data_type: "Utf8"
        - name: "arch"
          data_type: "Utf8"
        - name: "instance_type"
          data_type: "Utf8"
        - name: "release"
          data_type: "Utf8"
        - name: "ami_id"
          data_type: "Utf8"
        - name: "aki_id"
          data_type: "Utf8"

  - name: "spacex_launches"
    uri: "https://api.spacexdata.com/v4/launches"
    option:
      format: "json"

  - name: "github_jobs"
    uri: "https://web.archive.org/web/20210507025928if_/https://jobs.github.com/positions.json"
```

## Key value stores

Table sources can be loaded into in-memory key value stores if you specify which two
columns to be used to load keys and values in the config:

```yaml
kvstores:
  - name: "spacex_launch_name"
    uri: "test_data/spacex_launches.json"
    key: id
    value: name
```

The above config will create a keyvalue store named `spacex_launch_name` that allows you to lookup SpaceX launch names using launch ids.


## Specify a config file on startup

Use `-c` argument to run ROAPI using a specific config file:

```bash
roapi -c ./roapi.yml
```

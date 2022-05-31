# Databases

Thanks to the [connector-x](https://github.com/sfu-db/connector-x) Rust crate,
ROAPI is able to load tables from popular relational databases like MySQL,
PostgreSQL and SQLite.

```yaml
tables:
  - name: "table_foo"
    uri: "mysql://username:password@localhost:3306/database"
  - name: "table_bar"
    uri: "mysql://username:password@localhost:3306/database"
  - name: "table_baz"
    uri: "sqlite://path/to/sqlitelite/file"
```

With this, you can now write a single SQL query to join tables between MySQL, SQLite and local CSV files!

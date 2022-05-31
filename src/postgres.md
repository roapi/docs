# Postgres wire protocol

ROAPI uses the [convergence](https://github.com/returnString/convergence) Rust
crate to read and write Postgres wire protocol. This means you will be able to
query all tables loaded in ROAPI using any Postgres Clients as if ROAPI is a
real Postgres database!

By default, ROAPI listens for Postgres traffic on address `127.0.0.1:5432`, but
you can change it using the `--addr-postgres` command line argument or add the
following to your config file:

```yaml
addr:
  # binding address for TCP port that speaks Postgres wire protocol
  postgres: 0.0.0.0:5432
```

Once ROAPI boots up, you can connect to it without authentication:

```
$ psql -h 127.0.0.1
psql (12.10 (Ubuntu 12.10-0ubuntu0.20.04.1), server 13)
WARNING: psql major version 12, server major version 13.
         Some psql features might not work.
Type "help" for help.

houqp=> select 1;
 Int64(1) 
----------
        1
(1 row)

houqp=> 
```

See [here](config/dataset-formats/gsheet.html#example) for an example on how you can query data stored in a Google spreadsheet using the `psql` Postgres client.

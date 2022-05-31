# Command line argument

You can configure ROAPI to load as many tables as you want by repeating the `--table` argument:

```
roapi --table 'table1_name=table1_uri' --table 'table2_name=table2_uri'
```

You can use `RUST_LOG` environment variable to control the logging verbosity:

```
RUST_LOG=debug roapi ...
```

Here is the output from `roapi --help`:

```
roapi 0.7.1
QP Hou
Create full-fledged APIs for static datasets without writing a single line of code.

USAGE:
    roapi [OPTIONS]

OPTIONS:
    -a, --addr-http <IP:PORT>
            HTTP endpoint bind address

    -c, --config <config>
            config file path

    -d, --disable-read-only
            Start roapi in read write mode

    -h, --help
            Print help information

    -p, --addr-postgres <IP:PORT>
            Postgres endpoint bind address

    -t, --table <[table_name=]uri[,option_key=option_value]>
            Table sources to load. Table option can be provided as optional setting as part of the
            table URI, for example: `blogs=s3://bucket/key,format=delta`. Set table uri to `stdin`
            if you want to consume table data from stdin as part of a UNIX pipe. If no table_name is
            provided, a table name will be derived from the filename in URI.

    -V, --version
            Print version information
```

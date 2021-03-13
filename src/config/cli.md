# Command line argument

You can configure ROAPI to load as many tables as you want by repeating the `--table` argument:

```
roapi-http --table 'table1_name:table1_uri' --table 'table2_name:table2_uri'
```

You can use `RUST_LOG` environment variable to control the logging verbosity:

```
RUST_LOG=debug roapi-http ...
```

Here is the output from `roapi-http --help`:

```
roapi-http 0.1.1
QP Hou
Create full-fledged APIs for static datasets without writing a single line of code.

USAGE:
    roapi-http [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -a, --addr <IP:PORT>               bind address
    -c, --config <config>              config file path
    -t, --table <table_name:uri>...    table sources to load
```

# ROAPI Document
The official `ROAPI` website based on [mdBook](https://github.com/rust-lang/mdBook).

## Preparation
Install `mdbook` and `open-on-gh`
```sh
$ cargo install mdbook
$ cargo install mdbook-open-on-gh
```

## Build Instructions

1. Fork this repository

2. Clone in your local machine
```sh
$ git clone https://github.com/<your user name>/docs.git
```

3. Build
```sh
$ mdbook build
```

You can use `watch` instead.

```sh
$ mdbook watch --open
```

It's useful to open and watch the rendered book on every file change.

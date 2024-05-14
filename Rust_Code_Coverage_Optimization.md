# Rust code coverage optimize

> [!NOTE]
> [Project Setup From Here](https://github.com/MathiasStadler/repo_template/blob/main/includes/extract_scripts_from_markdown.md)

&nbsp;

> [!TIP]
> [How to set json with comment in MS Video Studio Code](https://stackoverflow.com/questions/69379869/how-to-set-json-with-comment-in-vscode)

## Update rust to latest stable version

```bash
# show running version
rustup show

# update to latest version system wide
rustup update

# switch between stable and nightly
rustup override set stable

rustup override set nightly

# clean your project
cargo clean
cargo clean --verbose

# build your project
cargo build
cargo build --verbose # large output

```


## Check is tarpaulin already installed

```bash
cargo --list |grep tarpaulin
echo $?
```

## Install crate tarpulin

- If this package is not already installed or you want to update it, then we use the Crates cargo-edit for this

> [!TIP]
> [Install cargo-edit](https://crates.io/crates/cargo-edit)
> This tool extends Cargo to allow you to add, remove, and upgrade dependencies
> by modifying your Cargo.toml file from the command line.

```bash
cargo add tarpaulin
## for update
# cargo update tarpaulin
## build the project
cargo build 
```

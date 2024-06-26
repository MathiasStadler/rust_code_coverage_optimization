# Rust code coverage optimize

> [!NOTE] > [Project Setup From Here](https://github.com/MathiasStadler/repo_template/blob/main/includes/extract_scripts_from_markdown.md)

&nbsp;

> [!TIP] > [How to set json with comment in MS Video Studio Code](https://github.com/MathiasStadler/repo_template/blob/main/includes/update_rust_add_crates_to_last_version.md)

&nbsp;

> [!NOTE] > [Update rust to latest stable version](https://github.com/MathiasStadler/repo_template/blob/main/includes/update_rust_add_crates_to_last_version.md)

## [rust code coverage first example from here](https://medium.com/@gnana.ganesh/robust-rust-how-code-coverage-powers-rust-software-quality-417ef3ac2360)

### generate simple function and test

[no_run](https://doc.rust-lang.org/rustdoc/write-documentation/documentation-tests.html#attributes)

```rust,no_run
#!/usr/bin/env bash
export EXAMPLE_SCRIPT_FILE="01_first_test.rs"
export EXAMPLE_SCRIPT_DIR="examples/"
cat << EoF > ./$EXAMPLE_SCRIPT_DIR/$EXAMPLE_SCRIPT_FILE
// FROM HERE
// https://medium.com/@gnana.ganesh/robust-rust-how-code-coverage-powers-rust-software-quality-417ef3ac2360


pub fn is_even(n: u32) -> bool {

    if n % 2 == 0 {

        true

    } else {

        false

    }

}

#[test]
pub fn test_even() {
    assert_eq!(is_even(2), true);
}

pub fn main(){
    println!("template");
}

/*
export FILE_NAME=$EXAMPLE_SCRIPT_FILE
export FILE_DIR_NAME=$EXAMPLE_SCRIPT_DIR
echo "build prg => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo build --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "run PRG => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo run --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "";
echo "run TEST => \$(echo \$FILE_NAME | cut -d . -f 1)"
cargo test --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
# cargo test --jobs 4 --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "ReturnCode => \$?"
*/
EoF

```

### run test with code coverage

- To enable code coverage, we pass the -C instrument-coverage flag while compiling the program with the Rust compiler

- If we are using Cargo for building the program, we can enable this flag by setting the RUSTFLAGS environment variable as shown below

- This will produce something called an “instrumented” binary/executable, which has extra code injected into it to count lines, regions and branches

```bash
RUSTFLAGS="-Cinstrument-coverage" cargo test
```

- When the program exits, the raw data from these counters is written to a “profraw” file which can be used to create a coverage report.

### show generated report

> [!NOTE]
> [How open firefox on Ubuntu through the command line (Terminal)](https://askubuntu.com/questions/1423732/how-open-firefox-on-ubuntu-through-the-command-line-terminal)

&nbsp;

- in terminal

    ```bash
    # access to display
    export DISPLAY=:0
    # get the path where is firefox installed
    which firefox
    /usr/bin/firefox <WEB_PAGE>
    ```

### generate simple function and test

[no_run](https://doc.rust-lang.org/rustdoc/write-documentation/documentation-tests.html#attributes)

```rust,no_run
#!/usr/bin/env bash
export EXAMPLE_SCRIPT_FILE="02_test_w_counter.rs"
export EXAMPLE_SCRIPT_DIR="examples/"
cat << EoF > ./$EXAMPLE_SCRIPT_DIR/$EXAMPLE_SCRIPT_FILE
// FROM HERE
// https://medium.com/@gnana.ganesh/robust-rust-how-code-coverage-powers-rust-software-quality-417ef3ac2360


pub fn is_even(n: u32) -> bool {

    is_even_counter += 1;

    if n % 2 == 0 {

        is_even_true_branch_counter += 1;

        true

    } else {

        is_even_false_branch_counter += 1;

        false

    }

}

#[test]
pub fn test_even() {
    assert_eq!(is_even(2), true);
}

pub fn main(){
    println!("Prg run {:?}",\$0);
}

/*
export FILE_NAME=$EXAMPLE_SCRIPT_FILE
export FILE_DIR_NAME=$EXAMPLE_SCRIPT_DIR
echo "build prg => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo build --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "run PRG => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo run --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "";
echo "run TEST => \$(echo \$FILE_NAME | cut -d . -f 1)"
cargo test --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
# cargo test --jobs 4 --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "ReturnCode => \$?"
*/
EoF

```

### using grcov in command prompt

- follow the tutorial

```bash
# Install grcov

cargo install grcov

# Run your tests

RUSTFLAGS="-Cinstrument-coverage" cargo test

# Generate a coverage report

grcov . -s . --binary-path ./target/debug/ -t html --ignore tests/  -o ./target/debug/coverage/

# Now you can view the report by opening an HTML file in your browser

open_with_your_browser ./target/debug/coverage/index.html

```

&nbsp;
> [!TIP]
> [How to do code coverage in Rust](https://blog.rng0.io/how-to-do-code-coverage-in-rust/)

&nbsp;
> [!NOTE]
> [Rust Source based Code Coverage since 1.60.0](https://blog.rust-lang.org/2022/04/07/Rust-1.60.0.html#source-based-code-coverage)

- install vscode extension Coverage Gutters

- install cargo install cargo-xtask

[xtask](https://github.com/matklad/cargo-xtask/)

- cargo-xtask is way to add free-form automation to a Rust project, a-la make, npm run or bespoke bash scripts

[use xtask](https://betterprogramming.pub/running-rust-tasks-with-xtask-and-xtaskops-a2193e67dc25)

[here continue](https://github.com/matklad/cargo-xtask/blob/master/examples/hello-world/xtask/src/main.rs)

[here continue](https://blog.rng0.io/how-to-do-code-coverage-in-rust/)

https://blog.rng0.io/how-to-do-code-coverage-in-rust/#our-goals

### args

```rust,no_run
#!/usr/bin/env bash
export EXAMPLE_SCRIPT_FILE="97_cmd_program_args.rs"
export EXAMPLE_SCRIPT_DIR="examples/"
cat << EoF > ./$EXAMPLE_SCRIPT_DIR/$EXAMPLE_SCRIPT_FILE
//FROM HERE
//https://doc.rust-lang.org/std/env/fn.args.html
use std::env;

pub fn main(){

    // let args: Vec<String> = env::args().collect();
    // dbg!(args);

    // https://doc.rust-lang.org/std/env/fn.args.html
    // Returns the arguments that this program was started with (normally passed via the command line).
    let mut _i = 0;
    // for argument in env::args()
    for (_i, argument) in env::args().enumerate(){
        println!("Arg {:} => {:}", _i, argument);
        //#[warn(clippy::explicit_counter_loop)]
        //_i += 1; // i++
    }
    
}

/*
export FILE_NAME=$EXAMPLE_SCRIPT_FILE
export FILE_DIR_NAME=$EXAMPLE_SCRIPT_DIR
echo "build prg => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo build --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "run PRG => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo run --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "";
echo "run TEST => \$(echo \$FILE_NAME | cut -d . -f 1)"
cargo test --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
# cargo test --jobs 4 --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "ReturnCode => \$?"
# clippy
cargo clippy --example "\$(echo \$FILE_NAME | cut -d . -f 1)" --fix
*/
EoF

```

### output

```bash
cargo run  --example 97_cmd_program_args argument1 argument2
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.01s
     Running `target/debug/examples/97_cmd_program_args argument1 argument2`
Arg 0 => target/debug/examples/97_cmd_program_args
Arg 1 => argument1
Arg 2 => argument2

```

### filename_only

```rust,no_run
#!/usr/bin/env bash
export EXAMPLE_SCRIPT_FILE="98_filename_only.rs"
export EXAMPLE_SCRIPT_DIR="examples/"
cat << EoF > ./$EXAMPLE_SCRIPT_DIR/$EXAMPLE_SCRIPT_FILE
//FROM HERE
//https://stackoverflow.com/questions/70343356/is-it-possible-to-access-current-file-name
use std::path::Path;

pub fn main(){

    let this_file = file!();
    // println!("filename: {}", this_file);
    
    let name_only = Path::new(this_file).file_name().and_then(|s| s.to_str()).unwrap();
    println!("Run => {}", name_only);
}

/*
export FILE_NAME=$EXAMPLE_SCRIPT_FILE
export FILE_DIR_NAME=$EXAMPLE_SCRIPT_DIR
echo "build prg => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo build --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "run PRG => \$(echo \$FILE_NAME | cut -d . -f 1)";
cargo run --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "";
echo "run TEST => \$(echo \$FILE_NAME | cut -d . -f 1)"
cargo test --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
# cargo test --jobs 4 --example "\$(echo \$FILE_NAME | cut -d . -f 1)"
echo "ReturnCode => \$?"
*/
EoF

```

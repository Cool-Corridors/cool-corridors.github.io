# CCA Documentation

This repository holds the source code for the documentation for the cool corridors project.

The documentation is written in markdown and then a rust cli tool called `mdbook` is used to build the html files to be hosted on github pages.

## Install
Install Rust which includes Cargo, then mdbook.
The general command to install rust is:
```bash
curl https://sh.rustup.rs -sSf | sh
```
To verify the command for your specific operating system, please visit [https://www.rust-lang.org/tools/install]()
This installs rust along with `Cargo` , it's pacakge manager.
Once Rust is installed, install the mdbook cli:

```
cargo install mdbook
```

You can now host the files locally using the following command:

```bash
mdbook serve
```

This is serve the html locally and also watch for any changes to the source code.

To change the source code or any documentation, clone this repository and navigate to `/src`. Add new `.md` files or edit current ones. Mdbook will automatically update the html with changes with: 
```bash
mdbook serve
``` 
You can also just do:

```bash
mdbook build
```
to build without serving.
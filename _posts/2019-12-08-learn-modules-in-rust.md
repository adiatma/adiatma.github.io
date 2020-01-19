---
title: Learn Modules in Rust
layout: post
author: adiatma
categories: rust
image: assets/images/hero.png
---

Rust provides a module system that can be used, you can manage your module system in rust with visibility (public/private) between them.

By default, the items in a module in rust have private visibility, and you have a `pub` keyword to change the visibility module to `public`.

Okay, let's try the example, if you have installed rust in your computer, please create new project with command `cargo new example-rust-module` into your terminal.

```rust
// ./src/main.rs

// to create module in rust you just add keyword mod before statement.
mod example_module {
 // can't be accessing from outher, and just work in this current scope.
 fn private_function(name: String) -> String {
 format!("Hay {}", name)
 }

 // with pub keyword this function can be access public.
 pub fn public_function(name: String) {
 println!("{}", private_function(name))
 }
}

fn main() {
 // Call the example_module
 example_module::public_function(String::from("Adiatma")) // output: Hey Adiatma
}
```

Okay, let's create a new file with the name `another_module.rs`.

```rust
// ./src/another_module.rs

mod hello_module {
 pub fn hello_func(name: String) {
 println!("{}", name)
 }
}
```

And call the module in `./src/main.rs`.

```rust
// ./src/main.rs

mod another_module;

fn main() {
 another_module::hello_module::hello_func("Adiatma".to_string()); // output: Adiatma
}
```

How if you want to create a new directory, let's say `mod_dir`. and create a new module in `mod_dir`, to doing it you need to create a file `lib.rs` in root directory and publish them in `lib.rs` file, below the example for more detail.

```rust
// ./src/lib.rs

pub mod mod_dir;
```

And then, in `mod_dir` you just create the file with name `mod.rs`.

```rust
// ./mod_dir/mod.rs

pub fn hey(name: String) {
 println!("{}", name)
}
```

Okay, let's call the module in `./src/main.rs`.

```rust
// please add the extern crate keyword and suitable with your project name. example `example_rust_module`.
extern crate example_rust_module;

// add use keyword to call mod `mod_dir`
use example_rust_module::mod_dir;

fn main() {
 mod_dir::hey("Adiatma".to_string()); // output: Adiatma
}
```

Okay, we finish to learning module check this out the [repo](https://github.com/adiatma/example-rust-module) to read the source code, and if you are curious to learn more about the module in rust please go to [https://doc.rust-lang.org/rust-by-example/mod.html](https://doc.rust-lang.org/rust-by-example/mod.html).
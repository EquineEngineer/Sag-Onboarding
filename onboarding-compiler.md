# Welcome to SAGittarius!

- [Welcome to SAGittarius!](#welcome-to-sagittarius)
  - [What is SAGittarius?](#what-is-sagittarius)
  - [Lexers, Parsers and Compilers](#lexers-parsers-and-compilers)
    - [What's a Lexer?](#whats-a-lexer)
    - [What's a Parser?](#whats-a-parser)
    - [What are compilers?](#what-are-compilers)
  - [Sagc in a nutshell](#sagc-in-a-nutshell)
    - [Dependecies](#dependecies)
  - [Your role in the project](#your-role-in-the-project)
    - [Training](#training)
    - [Active Development](#active-development)

## What is SAGittarius?

Hi!

If you're reading this, you have received an offer to join the SAGittarius development team and are wondering where to find resources to start your journey as a researcher.

Either that, or you've hacked into my machine. In such case, kudos to you, please don't touch my duck memes collection, it is a very prized and personal possession of mine.

As you might have heard, the SAGittarius project has set for its own goal to develop a low-code platform that generates dashboards from settings files.

If any question you might have is not included in this document, please write to [me](mailto:21imc10066@fh-krems.ac.at).

## Lexers, Parsers and Compilers

### What's a Lexer?

Lexers are programs that take a string of characters and turn them into a list of tokens.

### What's a Parser?

Parsers are programs that take a string of characters and turn them into a data structure that can be used by a computer.

### What are compilers?

Compilers are programs that take source files and turn them into executable files.

## Sagc in a nutshell

Sagc is a compiler that takes a settings file and turns it into a dashboard.

How does it do that? Magic! (And Rust, but mostly magic).

Each `.ssd` file is comprised of 4 sections:
- `service`: contains the name of the service that will be used to generate the dashboard and related metadata.
- `data`: contains the data that will be used to generate the dashboard.
- `application`: describes the application to be output by the compiler.
- `deployment`: enumerates the deployment targets and environments for the finished application.

What Sagc does, is take the settings file and parse it into multiple Rust structs.
These data structures have a 1:1 mapping with the sections of the settings file and can be loaded into json without losing any information. This is done by using the `serde` crate.
By doing so, json serves as a sort-of intermediate representation (IR) of the settings file.

Then, depending on which kind of application to produce, different adapters (also called compiler backends) are used to generate the final output. Our main target that we're working on right now is `Grafana`.

### Dependecies

Sagc is written in Rust, so you'll need to install the Rust toolchain to be able to compile it. We're also working on the nightly build (`cargo 1.74.0-nightly`), so be sure to set it up properly.

We currently depend on the following crates:
- [`nom`](https://docs.rs/nom/latest/nom/): for the parser and lexer building blocks.
- [`serde`](https://docs.rs/serde/latest/serde/): for serialization and deserialization of Rust structs to json.
- [`serde_json`](https://docs.rs/serde_json/latest/serde_json/): for serialization and deserialization of json to Rust structs. (+ derive macros).
- [`strum`](https://docs.rs/strum/latest/strum/): for enum parsing.
- [`strum_macros`](https://docs.rs/strum_macros/latest/strum_macros/): for derive macros for enums.
- [`url`](https://docs.rs/url/latest/url/): for url parsing.
- [`rocket`](https://docs.rs/rocket/0.5.0-rc.3/rocket/index.html): to build a web server for the compiler.
- [`clap`](https://docs.rs/clap/latest/clap/): to use the compiler as a CLI executable.

## Your role in the project

### Training

For the first weeks, there's no expectation you'll be very productive. And that's alright, because neither are the developers working on this since the beginning.

I will take care of introducing multiple useful resources to learn about rust, compilers and the project itself.

Here follows a list of good resources to learn:

- [Brief Introduction to Rust](https://www.youtube.com/watch?v=5C_HPTJg5ek)
- [Code to the moon](https://www.youtube.com/@codetothemoon)
- [No Boilerplate](https://www.youtube.com/@NoBoilerplate)
- [Logan Smith](https://www.youtube.com/@_noisecode)
- [Let's Get Rusty](https://www.youtube.com/@letsgetrusty)
- [Docs.rs](https://docs.rs)
- [The Rust Book](https://doc.rust-lang.org/book/)
- [The Rustonomicon](https://doc.rust-lang.org/nomicon/)
- [The Nominomicon](https://tfpk.github.io/nominomicon/introduction.html)

### Active Development

Your main job will be to expand on the compiler functionality and develop the new compiler backend. You will be working together with Antonino on such task.

You will be expected to:
- Write code that is easy to read and understand.
- Compile accurate documentation when necessary.
- Respect the PR workflow.
- Communicate whenever you're stuck or need help. 

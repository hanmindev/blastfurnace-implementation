# The Ingot Programming Language

Bringing Modern Programming features to streamline Datapack Development

## Background

Datapacks are an easy, non-intrusive way to add modifications to a Minecraft save instance. They can be shipped with the world, and users do not need any sort of client-side modification to use the changes. Due to their simplicity for the end-user, they have been gaining popularity for singleplayer worlds and small servers.

Within a Datapack, developers can add functions, which as the name suggests, allows the execution of a sequence of statements after being called. However, functions can be difficult to work with, especially as the codebase becomes larger and more complex. Minecraft functions are derived from console commands, which has suffered from significant feature creep over the last decade, leading to a Turing-complete language with the ability to interact with virtually any game feature, at the expense of an incredibly convoluted language.

Many compare Minecraft functions, or mcfunction to low-level assembly languages, since they both possess a very simple instruction set. This has inspired many developers in the community to build their own macro preprocessors, code generators, and compilers, in order to avoid having to write in mcfunction.

## Why Another mcfunction Language / Compiler?

There are many different languages with “mcfunction compilers” available today, but they’re often either too low-level, leaving a lot to be desired, or too high-level, which outputs poorly-optimized code.

An obvious contender for solving these issues is by creating an mcfunction backend for LLVM. This way, developers would be able to choose from a vast array of different high-level languages, while addressing the performance concerns through LLVM’s optimization layer. However, despite the fact that LLVM tries to assume very little about its backend in order to provide an IR that can be efficiently converted into any instruction set, it’s still too much for an efficient implementation. While the specific details are out of scope for this document, writing an mcfunction backend raises very similar issues as the ones that WebAssembly faces. One such example is the performance issues derived from WASM’s restriction on arbitrary control-flow graphs due to the lack of arbitrary jumps, just like in mcfunction. Because mcfunction runs very slowly, having to run inside a Minecraft instance which runs on a JVM, we need to get as much performance out of our implementation as possible.

I was inspired by the Rust programming language, which provides developers with many abstract, high-level features which incur little to no cost at runtime.

## Requirements

The goal of this project is to create a programming language and toolchain to bring modern programming features to datapack development. There is a list of requirements that this project will need to fulfill. Note that this list is likely to expand throughout development:

* Package management system
* Module system without header files
* Implicit types, type inference, and type checking
* Type definitions for aliases and structs
* Name resolution for local and global scopes
* Language server

## Sub-Design Documents

Here are a list of links to design documents of various components of the language and compiler.
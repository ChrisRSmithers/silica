# Silica

Silica is (or will be) a rust based High Level Synthesis tool. The idea is to allow for engineers unfamiliar with Verilog development to produce high quality Verilog for use in FPGAs.

## Background

FPGAs are fast, like *really* fast. Increasingly, it is becoming necessary to utilise cloud server based FPGAs for high throughput and energy critical compute applications. Unfortunately, development for FPGA is costly and time-consuming. VHDL and Verilog are the primary means of development in this field, but both are very verbose and specialised languages. Even experienced engineers in this area produce code quite slowly, albeit very high quality. The aim of this repository is to provide (another) Open-Source means of producing Verilog in a quick and dirty way, using Rust as the backbone.

## What Silica isn't

## The alternatives

## Why Rust?

Rust is a relatively young and very popular language at the time of writing, but neither of these are the reason for the decision to utilise Rust. Generally speaking, the more expressive a language is, the more restrictive an HLS tool needs to be. Certain constructs that may be standard in a language may be meaningless in a hardware setting, or carry endless complications for the writer of a compiler. The challenge of writing an HLS tool is balancing the impact of restricting parts of the underlying language (by stating them off limits), and being similar enough to the original language that familiarity and libraries are still useful for development purposes. With this in mind, Rust enforces two key principles that make compiling into Verilog far easier:

### Data Races

Discussion of the details of rust as a language are well beyond the scope of this project, but one concept in particular is important. Ownership is the name given to the underlying mechanism by which the rust compiler decides on which memory is available to be deallocated. Importantly, unlike in other languages, rust enforces a single ownership principle, meaning the scope of a given variable is very well defined, and data races are avoided at all times. Most programmers working in a multi-threaded environment will be familiar with the concept of a race condition, where the program flow is dependent upon which of a number of threads completes first. Race conditions cause indeterminate behaviour, and data races are similar. A data race occurs when two threads try to use the same piece of memory without synchronization, and at least one is writing to that memory. In general, when working with a language like C, in a single thread application, such a concern is irrelevant. Or more precisely, it doesn't matter to the engineer writing the code, but it is a very important consideration for the creators of the compiler. We won't go into more details here but in essence, since these are a serious problem in the world of hardware, it helps that Rust will enforce an easily understood structure on the coder, making transformation to RTL simpler from the point of view of Silica.

### Concurrency

Rust is a language built with concurrency and parallelism in mind. The base language offers a number of key features that we can seamlessly incorporate into Silica. Parallelism is absolutely key to any highly performant RTL and so having a familiar and well supported set of features already available is incredibly helpful for Silica to produce performant code

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

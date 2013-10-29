# A disruptor implementation for Rust

This is an API that allows for high-performance communication between Rust
tasks, fulfilling use cases similar to the built-in pipes API, but with better
performance.

# Building

There's no fancy build infrastructure yet, but if you have a working rust
compiler on your path, you should be able to run build.sh to get an optimized
build of the unit tests and a simple set of microbenchmarks.

# License

To be compatible with Rust, this library is dual-licenced under the terms of the
MIT and Apache 2 licenses.

# Features

This is a basic proof-of-concept, currently, so most functionality is missing.
However, current users can enjoy the following features:
 * Unicast pipelines consisting of a single publisher and one or more consumers.
 * A general purpose blocking wait strategy that causes the receiver to
   eventually block if no items are sent
 * A spinning wait strategy that roughly triples performance compared to the
   blocking strategy.

# Roadmap

This is a list of things that should probably be implemented in the near future:
 * Tests for unicast pipelines with more than one consumer
 * Batch publishing APIs (it's supported in the core code, but not in the public
   API yet)
 * More convenient APIs on the consumer side, including moving values out at the
   end of the pipeline in a way similar to the pipe API
 * Consumers that process events from the same stage of the pipeline in parallel
   (in other words, each event is shared by all consumers)
 * Unsafe API to allow parallel consumers to mutate the data they're processing
   (it becomes the caller's responsibility to avoid data races)
 * A safe API to allow parallel consumers mutable access to separate parts of
   the data (using reflection to perform dynamic checks before running the
   pipeline)
 * Add more unit tests in general
 * Add a more diverse set of performance tests
 * Implement some performance tests in Rust's built-in benchmark framework
# Snappy - A fast compressor/decompressor

[![Build Status](https://travis-ci.org/bicycle1885/Snappy.jl.svg?branch=master)](https://travis-ci.org/bicycle1885/Snappy.jl)

[Snappy.jl](https://github.com/bicycle1885/Snappy.jl) is a Julia wrapper for the [snappy](https://code.google.com/p/snappy/) library - a compression/decompression library focusing on speed.


## High-level Interfaces

The `Snappy` module exports only two functions:

* `compress(input::Array{Uint8})`
* `uncompress(input::Array{Uint8})`.

The names are self-explaantory and works as such (hence, always satisfies `uncompress(compress(input)) == input`).


## Low-level Interfaces

If you digg into the module, you will find the following lower-level functions:

* `snappy_compress(input::Array{Uint8}, compressed::Array{Uint8}) -> (length, status)`
* `snappy_uncompress(compressed::Array{Uint8}, uncompressed::Array{Uint8}) -> (length, status)`
* `snappy_max_compressed_length(source_length::Uint) -> length`
* `snappy_uncompressed_length(compressed::Array{Uint8}) -> (length, status)`.
* `snappy_validate_compressed_buffer(compressed::Array{Uint8}) -> status`

These functions have one-to-one correspondance to the C-APIs and are very thin wrappers of them, so you can consult the "snappy-c.h" header file for the documentation. Moreover, even though these functions are not exported by default, you can think that they are stable as long as the original C-APIs are stable.
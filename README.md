# Rust JSON Benchmark

This is a partial port of
[nativejson-benchmark](https://github.com/miloyip/nativejson-benchmark)
to Rust. The libraries tested are:

- [serde\_json](https://github.com/serde-rs/json) 1.0.9
- [json-rust](https://github.com/maciejhirsz/json-rust) 0.11.13
- [rustc-serialize](https://github.com/rust-lang-nursery/rustc-serialize) 0.3.24

#### `$ cargo run --release --bin json-benchmark`

```
                                DOM                STRUCT
======= serde_json ======= parse|stringify === parse|stringify ===
data/canada.json          10.8ms     9.6ms     4.1ms     7.0ms
data/citm_catalog.json     5.8ms     1.3ms     1.8ms     0.8ms
data/twitter.json          2.6ms     0.7ms     1.1ms     0.6ms

======= json-rust ======== parse|stringify === parse|stringify ===
data/canada.json           7.1ms     3.4ms
data/citm_catalog.json     3.4ms     0.9ms
data/twitter.json          1.4ms     0.6ms

==== rustc_serialize ===== parse|stringify === parse|stringify ===
data/canada.json          16.2ms    38.8ms    23.9ms    52.6ms
data/citm_catalog.json    11.0ms     3.6ms    15.7ms     2.9ms
data/twitter.json          6.2ms     1.8ms     8.6ms     1.7ms
```

- Intel(R) Core(TM) i7-6600U CPU @ 2.60GHz
- rustc 1.26.0-nightly (322d7f7b9 2018-02-25)

To update the numbers above, I run `./json-benchmark -n 256` twice on an
otherwise idle computer and take the least of the two results for each number.

For comparison, here are results from
[RapidJSON](https://github.com/miloyip/rapidjson) on the same hardware with the
nativejson-benchmark modified to run 256 times instead of 10.

```
                                DOM
==== rapidjson-clang ===== parse|stringify ===
data/canada.json           5.7ms    10.5ms
data/citm_catalog.json     2.5ms     1.7ms
data/twitter.json          1.8ms     1.2ms

===== rapidjson-gcc ====== parse|stringify ===
data/canada.json           4.7ms     8.6ms
data/citm_catalog.json     1.7ms     1.0ms
data/twitter.json          1.3ms     0.7ms
```

- clang version 3.8.0
- gcc version 5.4.0

# ham-codes

An educational collection of C implementations for Hamming and BCH error-correcting codes. The Hamming tools encode byte streams into codewords with configurable parity, and decode them again while detecting or correcting bit errors supported by the selected code. Separate command-line programs make it possible to try the encoders and decoders on files.

## Hamming code sizes

The project includes the following Hamming code configurations, written as `(n, k)` where `n` is the encoded word length and `k` is the number of data bits:

- `(3, 1)` and `(7, 4)`
- `(15, 11)` and `(31, 26)`
- `(63, 57)` and `(127, 120)`
- `(255, 247)` and `(511, 502)`

The implementation is organized around the Hamming code sources in `hamm/` and shared support routines in `std/`. BCH routines live in `bch/`, with C++ file encoder and decoder programs in `bch_cpp/`.

## Build the command-line tools

Each implementation directory has its own Makefile. From the repository root, build the Hamming utilities with:

```bash
make -C hamm
```

The resulting programs include an encoder (`file2hamm`) and decoder (`hamm2file`); the exact supported arguments are printed by the utilities or documented in their source. The BCH C++ tools can be built separately:

```bash
make -C bch_cpp
```

Use a compiler compatible with the flags configured in each Makefile. `make clean` in a component directory removes its generated output.

## File-based checks

The `test/` directory contains a Python runner that generates an input file, encodes it, can add simulated bit errors, decodes the result, and repeats the cycle. It can model randomly scattered flips or a contiguous damaged region. The parameters cover compiler selection, code sources, input size, parity configuration, output paths, and error pattern.

For example, from `test/`:

```bash
python3 test.py --gcc gcc --repeat 1 --file-size 512 --strategy random --flips-size 10
```

Run `python3 test.py --help` for the options supported by the checked-in runner. A separate test README gives a longer example and describes the runner's arguments.

## Scope

This repository focuses on the coding routines and simple file wrappers used to exercise them. It is not a general-purpose storage format or a network protocol. Keep the selected code parameters and decoder capabilities in mind when interpreting a result: error-correcting codes can only detect or correct error patterns within their mathematical limits.

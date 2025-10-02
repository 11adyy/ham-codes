# 11hamming-codes test tools

This runner generates an input file, encodes it, optionally introduces bit errors, decodes it, and repeats the process when requested.

Example:

```bash
python main.py \
    --gcc gcc-14 \
    --hamm-api ../ \
    --coder tools/file2hamm \
    --decoder tools/hamm2file \
    --file-gen tools/gen_file \
    --file-size 1024 \
    --parity-bits 3 \
    --strategy random \
    --flips-size 20
```

## General options

| Option | Default | Description |
| --- | --- | --- |
| `--gcc` | `gcc-14` | C compiler executable |
| `--hamm-api` | `..` | Directory containing the Hamming interface and sources |
| `--coder` | `tools/file2hamm` | Encoder source path |
| `--decoder` | `tools/hamm2file` | Decoder source path |
| `--file-gen` | `tools/gen_file` | Input-file generator source path |
| `--repeat` | `1` | Number of complete encode/decode runs |

## Input and output options

| Option | Default | Description |
| --- | --- | --- |
| `--file-size` | `512` | Generated input size in bytes |
| `--parity-bits` | `2` | Hamming parity-bit configuration |
| `--parity-help` | — | Print parity configuration details |
| `--src-file` | `image.img` | Generated input path |
| `--coded-file` | `image.hamm` | Encoded output path |
| `--decoded-file` | `decoded.img` | Decoded output path |

## Error simulation

| Option | Default | Description |
| --- | --- | --- |
| `--strategy` | `none` | Select `random` flips or a contiguous `scratch` region |
| `--scratch-length` | `1024` | Region length in bytes for `scratch` mode |
| `--width` | `1` | Number of affected bytes per step in `scratch` mode |
| `--intensity` | `0.7` | Flip probability from 0 to 1 in the selected region |
| `--flips-size` | `10` | Number of flips in `random` mode |

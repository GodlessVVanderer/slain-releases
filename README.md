# SLAIN

Compiled releases of SLAIN: cryptography, hashing and compression written from scratch in Rust,
one source for every CPU, no assembly. This repository holds release binaries only; the source is
not published.

## SLAIN evaluation kit 0.1.0

Download: [Releases](../../releases) -> `slain-eval-kit-0.1.0.zip` (Windows x64, Linux x64, Linux ARM64).

The kit finds the libraries already installed on your machine (OpenSSL 3, libsodium, libzstd) and
races them against SLAIN on one CPU core. Before anything is timed, both sides get the same input
and the outputs must match. It makes no network connection; it writes an HTML and a JSON report
on your machine. Run `windows-x64\slain-eval.exe` or `./linux-x64/slain-eval`; a full run takes
under a minute. The kit reports every operation it measures, slower ones included.

## Measured wins

AMD Ryzen 7 4800HS, one pinned core, best of 8 alternating rounds, 2026-10-30.
Speedup = installed library's time / SLAIN's time (above 1 = SLAIN is faster).

| Operation | vs OpenSSL 3.5.4 (Windows) | vs libsodium 1.0.18 (Linux) |
|---|---|---|
| AES-128-GCM | 3.50x at 64 B, 1.18x at 16 KiB, 1.14x at 1 MiB | |
| AES-256-GCM | 1.05-1.07x at 16 KiB-1 MiB | 1.87-2.23x |
| ChaCha20-Poly1305 | 2.29x at 64 B, 1.10-1.13x at 16 KiB-1 MiB | 1.41-1.76x |
| Ed25519 sign / verify | 3.35x / 3.55x | 1.88x / 1.96x |
| P-256 ECDSA sign / verify | 1.31x / 1.07x | |
| SHA-256 | 1.40x at 64 B, 1.00-1.01x at 16 KiB-1 MiB | 5.83-6.23x |
| SHA3-256 | 1.15x at 64 B, 1.01-1.02x at 16 KiB-1 MiB | |
| X25519 | | 1.24x |

| Operation | vs libzstd 1.5.7 (Windows) |
|---|---|
| zstd decompress, 4 MiB, levels 1 / 3 / 19 | 1.054x / 1.092x / 1.132x |

Run the kit on your own hardware; your numbers are the ones that count.

## License

The binaries are free to run for evaluation. All rights reserved. For a commercial license, open
an issue in this repository.

# ByteStore

A C++17 NoSQL key-value storage engine with a REST API layer.

## Architecture

- **Robin Hood Hash Map** — open-addressing index with linear probing
- **Bloom Filter** — probabilistic key-existence check per segment
- **Segmented Log** — append-only storage rotated by size
- **CRC-32 Checksums** — per-record integrity verification
- **Thread Pool** — concurrent task execution
- **Full-Text Search Index** — inverted index over stored JSON docs
- **Crow HTTP Server** — REST API exposing the engine

## Project Structure

```
ByteStore/
├── include/kv/       # All header files
├── src/              # All implementation files
│   └── conf/         # Configuration files
├── Makefile
└── README.md
```

## Build

```bash
make
```

## Configuration

Edit `src/conf/db.conf` to set data directory, segment size, and bloom filter parameters.

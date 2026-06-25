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

## REST API

The engine exposes a REST API via [Crow](https://crowcpp.org) on port **8008**.

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/` | List all models |
| POST | `/{model}` | Create model + insert data |
| GET | `/{model}` | Get all records (supports `?search=term`) |
| GET | `/{model}/{key}` | Get specific key |
| DELETE | `/{model}` | Delete entire model |
| DELETE | `/{model}/{key}` | Delete specific key |

## Performance

- ~500K+ ops/sec on local benchmarks
- Sub-millisecond lookups via Bloom filter + Robin Hood index
- CRC-32 integrity check on every read

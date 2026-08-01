# Kośa (कोश)

> A unified Rust platform for storage, file management, serialization, and cloud integrations.

---

## Vision

Kośa (कोश) is a modular Rust workspace that provides a common abstraction layer for storage providers, file systems, serialization formats, and cloud services.

Instead of applications directly interacting with Firebase, SQLite, Google Sheets, or Google Drive, they interact with a unified API defined by Kośa.

The underlying provider becomes an implementation detail.

Kośa is designed to compile to both native libraries and WebAssembly (WASM), enabling the same storage logic to be reused across:

- Desktop applications
- Web applications
- Electron
- Tauri
- Rust applications
- Future MCP runtimes

---

## Meaning

**Kośa (कोश)**

In Sanskrit, *Kośa* means:

- Treasury
- Repository
- Storehouse
- Collection
- Container

The name reflects the project's purpose of providing a unified repository for data and storage services.

---

# Philosophy

Applications should never depend directly on a storage implementation.

Instead:

```
Application
        │
        ▼
     Kośa API
        │
 ┌──────┼────────┐
 │      │        │
SQLite Firebase Google
```

Changing storage providers should require little or no application changes.

---

# Design Goals

- Provider-oriented architecture
- Storage abstraction
- Local-first support
- Cloud-native integrations
- WASM compatible
- Zero business logic
- Modular crates
- Cross-platform
- Strong typing
- Async-first APIs

---

# Workspace

```
kosa/

Cargo.toml

crates/

    kosa-core

    kosa-sqlite
    kosa-firebase

    kosa-google-sheet
    kosa-google-drive

    kosa-file
    kosa-zip

    kosa-json
    kosa-yaml
    kosa-toml
    kosa-csv

bindings/

    kosa-wasm
```

---

# Current Scope

Version 1 intentionally focuses on a small number of providers.

## Storage

- SQLite
- Firebase

## Google Workspace

- Google Sheets
- Google Drive

## Files

- Local File System
- ZIP Archives

## Serialization

- JSON
- YAML
- TOML
- CSV

---

# Future Scope

Future releases may add support for:

Storage

- PocketBase
- PostgreSQL
- MongoDB
- MySQL

Cloud Storage

- Amazon S3
- Azure Blob Storage
- Google Cloud Storage
- MinIO

Utilities

- Encryption
- Compression
- Synchronization
- Versioning
- Streaming
- Caching

---

# Architecture

```
                 Applications
                        │
                        ▼
                  Kośa Core
                        │
      ┌─────────────────┼──────────────────┐
      │                 │                  │
 Storage Providers   File Providers   Serializers
```

---

# Core Components

## kosa-core

Defines all common traits.

Responsible for:

- Storage abstractions
- File abstractions
- Serialization abstractions
- Shared types
- Error handling
- Common utilities

No provider-specific logic exists here.

---

## kosa-sqlite

SQLite implementation.

Features

- CRUD
- Transactions
- Migrations
- Local cache
- Prepared statements

---

## kosa-firebase

Firebase implementation.

Features

- Authentication
- Firestore / Realtime Database support (configurable)
- CRUD operations
- Batch operations

---

## kosa-google-sheet

Google Sheets provider.

Features

- Read Sheets
- Write Sheets
- Batch Updates
- Sheet Management

---

## kosa-google-drive

Google Drive provider.

Features

- Upload
- Download
- Search
- Folder Management

---

## kosa-file

Local filesystem abstraction.

Features

- Read
- Write
- Copy
- Move
- Delete
- Directory traversal

---

## kosa-zip

Archive support.

Features

- ZIP creation
- Extraction
- Streaming
- Directory compression

---

## Serialization

### kosa-json

JSON serialization

### kosa-yaml

YAML serialization

### kosa-toml

TOML serialization

### kosa-csv

CSV serialization

---

# Provider Model

```
Application

↓

Storage

↓

StorageProvider

↓

Firebase
SQLite
Google Sheets
```

Applications never directly depend on provider implementations.

---

# Example

```rust
let storage = Storage::firebase(config);

storage.insert("users", user);
```

Later

```rust
let storage = Storage::sqlite(config);

storage.insert("users", user);
```

Application logic remains unchanged.

---

# WebAssembly

Kośa is designed to compile into WASM.

```
Rust

↓

Kośa

↓

WebAssembly

↓

Electron
React
Browser
```

This allows one implementation to serve multiple frontends.

---

# Principles

- Trait-driven architecture
- Provider isolation
- Local-first
- Async by default
- Zero business logic
- Strong typing
- Minimal dependencies
- Cross-platform
- Testability

---

# Non Goals

Kośa is **not**

- An ORM
- A backend framework
- A web framework
- A database server
- An authentication platform
- A synchronization engine

Applications remain responsible for business logic.

Kośa provides infrastructure only.

---

# Roadmap

## Version 1

- Core abstractions
- SQLite
- Firebase
- Google Sheets
- Google Drive
- File API
- ZIP API
- JSON
- YAML
- TOML
- CSV

## Version 2

- PocketBase
- MongoDB
- PostgreSQL
- MinIO
- Encryption

## Version 3

- Synchronization Engine
- Caching
- Streaming
- Versioning
- Offline replication

---

# License

Apache-2.0

---

> **Kośa** provides a unified storage platform that enables applications to interact with diverse storage systems through a consistent, provider-oriented API, allowing storage implementations to evolve without impacting application logic.

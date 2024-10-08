## Storage Engine

This document describes the implementation of the `Opslag Storage Engine (OsE)`. This spans from disk storage to memory management using a
buffer pool manager. This document describes the following:

- [ ] The database structure
  - [ ] Each database instance is a folder
  - [ ] Each table is a file
  - [ ] Each index is a file too
- [ ] The storage model
  - [ ] Opslag is a Key/Value store
  - [ ] It uses the PAX storage model; a combination of row-oriented & column-oriented storage model
- [ ] The file organization structurev
  - [ ] Heap file organization
  - [ ] Tree file organization
  - [ ] Sequential/Sorted File organization
  - [ ] Hashing file organization
- [ ] The pages:
  - [ ] The page id
    - [ ] It's structure:
      - [ ] Database instance
      - [ ] Table
  - [ ] The page size
    - [ ] Read heavy vs write heavy
  - [ ] The page directory
  - [ ] The page header
  - [ ] Data pages
  - [ ] Index pages
  - [ ] Page Layout:
    - [ ] Tuple based:
      - [ ] Slotted pages
      - [ ] Record ID - used by the database not the user space
        - [ ] File ID, Page ID, Slot #
        - [ ] An offset page for variable length data
    - [ ] Layout
      - [ ] Convert types to bytes
      - [ ] Opslag us responsible to interpret bytes back to attributes & values
      - [ ] Tuples have a header describing their content
      - [ ] Tuple data
        - [ ] Determine bytes layout
          - [ ] Padding if needed
          - [ ] `C` or `Rust` like memory layout
    - [ ] Column based
    - [ ] Index based
  - [ ] Keep track of free space per page
    - [ ] Pages with free space
  - [ ] `Page Replacement Policy`:
    - [ ] LRU
    - [ ] Clock Algorithm
    - [ ] LRU-k
  - [ ] General page interface:
    - [ ] Create
    - [ ] Get
    - [ ] Delete
    - [ ] Iterate
  - [ ] Concurrency conntril:
    - [ ] Locks
    - [ ] Latches
- [ ] Durability:
  - [ ] Write Ahead Log
    - [ ] Journal files
- [ ] Compaction
  - [ ] Vacuuming
- [ ] Configuration file:
  - [ ] yaml
  - [ ] conf
- [ ] Page clearance
- [ ] Compression
- [ ] Encoding
- [ ] Versioning
- [ ] Data catalog
  - [ ] Schema definition and storage
  - [ ] Column limits
- [ ] Null support
  - [ ] Bitmaps
- [ ] Index support:
  - [ ] Hash indices
  - [ ] B+Tree
  - [ ] Geo Based Indixes
  - [ ] Vector Index
  - [ ] Radix index
  - [ ] Tries
- [ ] Types support:
  - [ ] Serial for sequences
  - [ ] All int bases
  - [ ] All float types
  - [ ] Booleans
  - [ ] Varchar
  - [ ] BigInt
  - [ ] BigFloat
  - [ ] UUID
  - [ ] Char
  - [ ] Proto
  - [ ] Date
  - [ ] Arrays
  - [ ] Geo type
  - [ ] Vector
  - [ ] Polygon type
  - [ ] Decimal
  - [ ] Money/Currency
  - [ ] Dates type
- [ ] Consider Object Storages
  - [ ] S3
  - [ ] SlateDB


#### Questions:
- [ ] Columnar vs Row oriented?
  - [ ] An engine per table?
    - [ ] The default enfine being row-oriented
      - [ ] Similar to InnoDB/Block/Row storage format
    - [ ] Support for column oriented structures too
      - [ ] SSTables come here
      - [ ] Think through how compaction works
  - [ ] Column storage choice?
    - [ ] On Disk
    - [ ] Fully on RAM
- [ ] Look into kdb.
- [ ] Support for special structures?
  - [ ] Time based indices
  - [ ] Graph Database structure
  - [ ] Vector indices
    - [ ] Approximate nearest neighbor


#### Storage implementation considerations:
- [ ] Separate the files:
    - [ ] Data file
    - [ ] Index file
- [ ] Consider using deletion markers - `tombstones`.
- [ ] Disks are accessed using system calls
- [ ] The file format must be easy to construct, modify and interpret
- [ ] Garbage collection & fragmentation
- [ ] Binary encoding
- [ ] Endianness:
  - [ ] Big Endian
  - [ ] Little Endian
  - [ ] `RocksDB` has platform-specific definitions that help identify target platform byte order
- [ ] Most numeric data types are represented as fixed-sized values
- [ ] Consider serialization and deserialization
- [ ] Come up with a binary format
- [ ] Consider the `IEEE` standard for the different primitive types.
  - [ ] Like `IEEE 754` for `Floats`
  - [ ] `32-bit` float represents a single-precision value
  - [ ] `Double` represents a double-precision float.
  - [ ] `Pascal` & `German` strings
- [ ] Bit-packed data:
  - [ ] Booleans
  - [ ] Enums
  - [ ] Flags
- [ ] [Bit packing](https://www.databass.dev/links/58)
- [ ] Bitmasks and bitwise operations
- [ ] How addressing is going to be done:
  - [ ] Split into same-size pages; for in-place updates
  - [ ] Single/multiple contiguous blocks
- [ ] File header & footer 
  - [ ] Fixed size
  - [ ] Quick to access 
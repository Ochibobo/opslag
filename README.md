#### Opslag Storage Engine
- [ ] Storage Manager
  - [ ] File structure
    - [ ] Proprietary
    - [ ] Apache Parquet - columnar
    - [ ] File per database object
  - [ ] Storage model
    - [ ] K/V store?
- [ ] Buffer Pool Manager
  - [ ] Pages
    - [ ] Architecture
      - [ ] Heap File Organization
      - [ ] Tree File Organization
      - [ ] Sequential/ Sorted File Organization (ISAM)
      - [ ] Hashing File Organization
    - [ ] Page ID
      - [ ] Uniqueness:
        - [ ] Per database instance
        - [ ] Per database
        - [ ] Per table
    - [ ] Page Size
      - [ ] Read Heavy vs Write Heavy
    - [ ] Page Directory
    - [ ] Page Header
    - [ ] Page
      - [ ] Data Pages
      - [ ] Index Pages
    - [ ] Page Layout
      - [ ] Tuple based
        - [ ] Slotted Pages
        - [ ] Record IDs
          - [ ] File Id, Page ID, Slot #
          - [ ] Most don't store this id with the tuple
        - [ ] Layout
          - [ ] Need not be contiguous
          - [ ] DBMS interprets bytes into attribute types & values
          - [ ] Tuple Header
          - [ ] Tuple Data
      - [ ] Column Based 
      - [ ] Index Based
    - [ ] Free Space
    - [ ] Page Replacement Policy
    - [ ] Page Interface
      - [ ] Create
      - [ ] Get
      - [ ] Write
      - [ ] Delete
      - [ ] Iterate
- [ ] Locks
- [ ] Latches
- [ ] WAL
  - [ ] Journal files
- [ ] Compaction
  - [ ] Vacuuming
- [ ] Conf file
  - [ ] yaml
  - [ ] conf
- [ ] Page Clearance
- [ ] Storage Engine as a service
- [ ] Compression
- [ ] Encoding
- [ ] Versioning
- [ ] Data Catalog
  - [ ] Schema definition
- [ ] ACID
- [ ] Recovery management
- [ ] Column limits
  - [ ] The number of limits

### Random Notes
- [ ] Database server has a network layer
- [ ] Databases usually have a separate server
- [ ] We have an OS interface layer for file handling
- [ ] The storage engine has:
  - [ ] Disk Storage Manager
  - [ ] Buffer Manager
  - [ ] Index Manager
- [ ] Shard management sits on top of the storage manager
- [ ] It sits together with the cluster manager 
￼

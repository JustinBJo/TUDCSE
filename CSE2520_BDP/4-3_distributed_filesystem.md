# 3. Distributed Filesystem

## 1. Filesystem
> File systems determine how data is stored and retrieved.

A file system keeps track of the following data items:
- Files: where the data we want to store are
- Directories: groups file together
- Metadata: file length, permissions, file types, etc

File systems make sure that the data is always accessible.<br>
Most modern filesystems use a *log* to maintain consistency.

Common filesystems are EXT4, NTFS, APFS, and ZFS

## 2. Distributed filesystems
> A filesystem which is shared by being simultaneously mounted on multiple servers.<br>

Data in a distributed filesystem is partitioned and replicated across the network.<br>
Read and Writes can occur at any node.

## 3. Large-scale DF: Google File System (GFS)
- A single file can contain many objects
- Files are divided into fixed size chunks with ids
- Files are replicated across chunk servers
- Master keeps all metadata
- Chunkservers keep chunks on local disk as linux files
  - Neither the client nor the chunkserver cache file data
- GFS is a journaled filesystem: all operations are added to a log first, then applied

## 4. Large-scale DF: Hadoop FileSystem (HDFS)
roots from GFS<br>
- NameNode: same as Master in GFS
- DataNode: same as Chunkserver in GFS
- journal: same as the operation log in GFS
- block: same as chunk

Differences from GFS
- HDFS is append-only, where in GFS write is random
- HDFS has one writer and multiple readers, but GFS has multiple writers and readers
- HDFS block is 128MB, whereas HDFS chunk is 64MB
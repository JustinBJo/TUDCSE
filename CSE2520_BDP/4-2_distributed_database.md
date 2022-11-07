# 2. Distributed Databases
> A distributed database is a distributed system designed to provide read/write access to data,
> using the relational or other format.

We will examine 3 topics in DD:
1. Replication
    - Keep a copy of the same data on several nodes
2. Partitioning
    - Split the database and distribute the partitions to different nodes
3. Transactions
    - Units of work that group several reads/writes to be performed together in the DB

## 1. Replication
### Why replicate?
- Data scalability
    - to increase read throughput by allowing more machines to serve read-only requests
- Geo-scalability
    - to have the data close to clients
- Fault tolerance

### How to replicate?
We have several replication design choices:
- Replication architecture
    - Leader-based replication
    - Multi-leader replication
    - Leaderless replication
- Implementation of replication logs
    - Statement based
    - Write-ahead log based
    - Logical-based
- Distribution of updates
    - Synchronous
    - Asynchronous

<br>

**Replication Architectures**<br>
> How is a replicated dataset accessed and updates?

In a replicated system, we have two node roles:
- Leaders: nodes that accept write queries from clients
- Followers: nodes that provide read-only access to data

Therefore we can have different architectures:
- Single leader (master-slave)
    - a single leader accepts writes, which are distributed to followers
- Multi-leader (master-master)
    - multiple leaders accept writes, keep themselves in sync, then update followers
- Leaderless replication
    - all nodes are peers in the replication network

<br>

**Implementations of replication logs**<br>
1. Statement based replication
    - The leader ships all write requests (e.g. INSERT, UPDATE) to the followers
    - However it is non-deterministic and mostly abandoned
2. Write-ahead log based replication
    - Before writing data to data structures, databases write the intended change to an append-only write-ahead log (WAL)
    - WAL-based replication writes all changes to the leader WAL and all the follower WALs. The followers apply the WAL entries to get consistent data.
    - The problem is that if the data structure changes in the leader, the followers stop working
    - Postgres and Oracle use this replication
3. Logical-based replication
    - The database generates a stream of logical updates for each update to the WAL.
    - Logical updates can be:
        - for new records, the values that were inserted
        - for deleted records, their id
        - for updated records, their id and the new values
    - MongoDB and MySQL use this replication

<br>

**Distribution of updates (How does replication work?)**<br>
When a write occurs in a node, this write is distributed to other nodes in synchronously or asynchronously.

1. Synchronous replication
    - the leader waits until the followers receive the update before reporting success
    - followers are guaranteed to have a copy, so durable even if the leader fails
    - impractical
2. Asynchronous replication
    - the leader reports success and asynchronously updates the followers
    - higher availability but followers are not guaranteed to have an up-to-date copy

<br>

### Consistency models
> Contract between programmer and replicated system<br>
> It specifies the consistency between replicas and what can be observed as possible results of operations.

CAP theorem states that it is impossible to get all three of consistency, availability, and partition tolerance

For example, synchronous replication is consistent but not always available (in case of failure of any follower)<br>
Asynchronous replication is inconsistent but available in the existence of failure

Consistency models can answer questions such as:
- what are the possible results of a read query?
- can a client see its own updates?
- is the causal order of queries preserved at all copies of data?
- is there a total order of operations preserved at all replicas?

Spectrum of consistency models:
- Strong consistency models (illusion of maintaining a copy)
  - Linearizable consistency
  - Sequential consistency
- Weak consistency models
  - Client-centric consistency models
  - Causal consistency
  - Eventual consistency

Strong consistency models have stronger consistency.<br>
Weak consistency models have better performance.

- Eventual consistency
  - All updates are eventually delivered to all replicas.
  - Examples
    - search engines: not always consistent with the current state of the web
    - cloud file systems: may be out-of-sync with their latest versions
    - social media apps: number of likes for a video may need refreshing
- Causal consistency
  - Causally related operations are delivered to other replicas in the correct order.
  -  maintains a partial order based on causality
- Client-centric consistency
  - Monotonic reads: if a process reads x, return x or more recent value
  - Monotonic writes: if a process writes to x, reflect previous write
  - Read your writes: the effect of a write on x will always be seen by a successive read on x by the same process
  - Writes follow reads: if write is followed by a read on x, it is guaranteed to be on the same or more recent value
<br>
<br>

- Sequential consistency
  - The operations appear to take place in some total order that is consistent with the order of operations on each replica
- Linearizability
  - As soon as write is complete, the result is immediately replicated to all nodes and is made available
  - Concurrent reads from any node returns the same values at any time


## 2. Partitioning
> Partitioning is done for more scalability

Due to partitioning, queries can be run in parallel, and read/writes can be spread on multiple machines.

Partitioning is always combined with replication because with partitioning, a node failure leads to irreversible data corruption.

### How to partition
1. Range partitioning
    - takes into account the natural order of keys to split the dataset in the required number of partitions
    - requires keys to be naturally ordered and keys to be equally distributed
2. Hash partitioning
    - calculates a hash over each item key and then produces the modulo of this has to determine new partition
3. Custom partitioning
    - exploits locality or uniqueness properties of the data to calculate the appropriate partition to store the data
    - example: pre-hashed data (e.g. git commits) or location specific data

## 3. Transactions
not part of the exam material

<br>
BDP - The Ultimate Cheat Sheet
===

# 0. Introduction to Big Data
> Big data are data too large to be efficiently processed on a single computer,<br>
> or massive amounts of diverse, unstructured data produced by high-performance applications

## Many V's
- Volume: large amount of data
- Variety: data comes in various forms and sources
- Velocity: the content is changing quickly

## Processing
The ETL cycle:
- Extract: convert raw or semi-structured data into structured data
- Transform: covert units, join data sources, cleanup etc
- Load: load the data into another system for further processing

Big data engineering: concerned with building pipelines
Big data analysis: concerned with discovering patterns

Types of processing:
- Batch processing
- Stream processing


# 1. Programming for Big Data

## 1. Data types
- Unstructured: data formats not known (txt, html)
- Semi-structured: known format (json, csv, xml)
- Structured: known format, linked together in graphs or tables (SQL or Graph DBs)


1. Sequences/Lists
2. Sets
3. Maps or Dictionaries
4. Nested data type: Graph
   - Nodes and Edges
   - Represented as Map[Node, List[Edge]]
5. nested data type: Tree
6. Tuples
7. Relations
8. K/V pairs

## 2. Functional programming
1. No side effects
2. Immutable data structures
3. Higher order functions
4. Laziness

[Function signatures](2.programming_for_bd.md#Functions and signatures)


# 3. Unix
> A true multiuser operating system<br>
> Users have their own private space on the machine's hard disk and are identified by an id number

## 1. Filesystem
Permissions: Owner - Group - Other
- r: read(4)
- w: write(2)
- x: execute(1)

## 2. Pipe
> Pipes combine commands<br>
> Pipes forward a program's STDOUT line-by-line to the input of another program<br>

## 3. Commands
[link](3.unix.md#3-commands)


# 4. Distributed Systems
## 1. Introduction to DS
> Distributed system is a software system in which components located on networked computers communicate and coordinate their actions by passing messages

Main problems in DS
1. Partial failures
2. Unreliable networks
3. Unreliable time
4. No single source of truth, different options

### 1. Partial failures
If one part of the system fails but the system as a whole works, it can cause outages.<br>
It is hard to detect whether something has failed or not because it takes time to deliver the message

### 2. Unreliable networks
Two types:
- Synchronous system
  - Process execution speeds or message delivery times are bounded
  - Pure synchronous system only exists in theory
- Asynchronous system
  - No assumptions about process execution speeds or msg delivery times
  - Used by most DS's

When an asynchronous system fails, it is hard to tell where the failure happened.<br>
Common solution is using message timeouts.

Partially-synchronous systems: upper bounds on the network delay

### 3. Unreliable time
We cannot rely on RTC because our message rated might be more fine-grained that the clock accuracy.

Ordering problems:
- For a single sender, use FIFO
- For multiple sender and receiver,
  - Total order: use RTCs if our message rate is globally bounded and less fine-grained
  - Causal order: use happens-before otherwise

#### Lamport Timestamps
- Each individual process p maintains a counter: LT(p)
- A process performing an action increments its counter LT(p)
- A process includes its counter when sending a message
- A process updates its counter when it receives a message (it chooses a larger counter)

if a -> b then LT(a) < LT(b), but not the other way around.

#### Vector clocks
Similar to Lamport timestamps, but each node has N counters where N is the total number of nodes in the system.

if a->b then VC(a) < VC(b), and also the other way around.

Vector clocks are expensive to maintain (O(n) per communication).

They maintain partial causal order

### 4. Distributed decision making
#### Byzantine fault tolerance
Tolerance against malicious nodes/suboptimal voting.

There must be at least 3f+1 nodes, where f = malicious nodes

#### Consensus algorithms
Algorithms that provide agreement in the presence of faulty nodes.<br>
Agreements in:
- resource allocation
- committing a transaction
- synchronising state machines
- leader election
- atomic broadcasts

We are looking at two algorithms: Paxos and Raft. They tolerate crash faults with 2f+1 nodes, but not Byzantine fault.

##### 1. Paxos
Three roles:
- Proposer: chooses a value and sends it to a set of acceptors to collect votes
- Acceptor: vote to accept or reject the values proposed by the proposer
- Learner: adopt the value when a large enough number of acceptors have accepted it

Steps:
1. Voting
   - Prepare
     - proposer sends Prepare(n) to acceptors (n = proposal number)
   - Promise
     - acceptor sends Promise to proposer if n is higher than every previous proposal number received
2. Replication
   - Accept
     - if proposer receives promise from the majority, it sends Accept(n)
     - proposers accept the proposal unless they already have responded to a prepare request with higher n

##### 2. Raft
1. Leader election
   - Raft defines the following server states:
     - Candidate
     - Leader: accepts log entries from clients, replicates them on other servers
     - Follower: replicate the leader's state machine
   - If the leader server crashes, a new leader is voted
   - Only up-to-date nodes are elected as leaders
2. Log replication
   - The leader accepts log entries from clients and replicates them across the servers


## 2. Distributed database
Three main topics:
1. Replication: keep a copy of the same data on several nodes
2. Partitioning: split the database and distribute the partitions to different nodes
3. Transactions (not part of this course)

### 1. Replication
Replication is done for:
- data scalability (increase read throughput)
- geo-scalability (to have the data close to clients)
- fault tolerance

Replication is done by choosing several different replication design choices:
1. Replication architecture
   - Leader-based
   - Multi-leader
   - Leaderless
2. Implementation of replication logs
   - Statement based
   - Write-ahead log based
   - Logical-based
3. Distribution of updates
   - Synchronous
   - Asynchronous

#### Replication architecture
> How is a replicated dataset accessed and updated?

1. Single-leader: a single leader accepts writes, which are distributed to followers
2. Multi-leader: multiple leaders accept writes, keep themselves in sync, the update followers
3. Leaderless replication: all nodes are peers in the replication methods

#### Implementations of replication logs
1. Statement-based replication
   - The leader ships all write requests to the followers
   - Non-deterministic and is mostly abandoned
2. Write-ahead log based replication
   - Before writing data to structures, databases write the intended change to an append-only write-ahead log (WAL)
   - WAL-based replication writes all changes to the leader WAL and all the follower WALs. The followers apply WAL entries
   - Problem: if the data structure changes in the leader, the followers stop working
   - Example: Postgres, Oracle
3. Logical-based replication
   - The database generates a stream of logical updates for each update to the WAL:
     - for new records: the values that were inserted
     - for deleted records: their id
     - for updated records: their id and new values

#### Distribution of updates
1. Synchronous replication
   - The leader waits until a configurable number of followers report success
   - impractical
   - High consistency, low availability
2. Asynchronous replication
   - The leader reports success and asynchronously updates the followers
   - High availability, low consistency

#### Problems of replication methods
1. Multi-leader replication
   - Write conflicts can happen
   - Resolve by:
     - one leader per session
     - converge to consistent state
       - last-write-wins
       - let an application solve it
       - use conflict-free data types
2. Asynchronous replication
   - Read-after-writes: clients might not see their own updates
   - (non-)Monotonic reads: when reading from multiple replicas concurrently, a stale replica might not return records that the client read from an up to date one.
   - Causality violations: updates might be visible in different orders at different replicas.

#### Consistency models
In distributed database, there is a tradeoff between Availability and Consistency(CAP theorem).
<br>Consistency model is a contract between programmer and replicated system.

There are two types of consistency models:
- Strong consistency models (linearizable consistency, sequential consistency)
- Weak consistency models (client-centric, causal, eventual consistency)

1. Eventual consistency 
   - all updates eventually delivered to all replicas 
   - all replicas reach a consistent state if no more user updates arrive
2. Causal consistency 
   - Causally related operations are delivered to other replicas in the correct order
3. Client-centric consistency models
   - provides guarantees about ordering of operations only for a single client process
4. Sequential consistency
   - The operations appear to take place in some total order that is consistent with the order of operations on each replica
5. Linearizability
   - As soon as writes complete successfully, the result is immediately replicated to all nodes atomically and is made available to reads
   - At any time, concurrent reads from any node return the same values

### 2. Partitioning
Partitioning is done for scalability (running queries, reads, and writes in parallel)

3 partitioning strategies
- Range partitioning: natural order of keys to split the dataset into required number of partitions
- Hash partitioning: modulo of hash
- Custom partitioning

Request routing: a query router directs the clients to appropriate partitions.
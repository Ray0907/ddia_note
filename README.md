# Designing Data-Intensive Applidations

- Reliable
- Scalable
- Maintainable

# Data model

- Relational
- Document
- Graph
  - Vertices(Nodes or Entities)
  - Edges(Relationships 或 Arcs)
  - Ex
    Graph:
    Vertices 就是人，Edges 就是人之間的關係

## SSTables and LSM-Trees

- SSTables(Sorted String Table)
  - SSTable requires that the writes be sorted by key.
  - This means we cannot append the new key/value pairs to the segment immediately because we need to make sure the data is sorted by key first.
- LSM-Trees ( Log Structured-Merge Trees)
  - heavy write throughput
  - worst case is thiat the key is not exist.

## B-Tree v.s. LSM-Trees

- LSM-Trees 的寫入較 B-Tree 快
- B-Tree 讀取比 LSM-Trees 快

## OLAP and OLDP

- Online analytical processing (OLAP) is a system for performing multi-dimensional analysis at high speeds on large volumes of data.
  - for user
- Online transactional processing (OLTP) enables the real-time execution of large numbers of database transactions by large numbers of people, typically over the Internet.
  - for analyzer

## Encoding and Evolution

- Backward compatibility
- Forward compatibility

- binary encoding

  - Programming language–specific encoding
  - Textual encoding
    - JSON, XML, and CSV
  - Binary schema–driven
    - Thrift, Protocol Buffers, and Avro

- dataflow
  - database
  - RPC and REST APIs
  - Asynchronous message passing

## Three popular algorithms for replicating changes between nodes

- Single-leader replication
- Multi-leader replication
  - Multi-Leader Replication Topologies
    - Circular topology(MySQL)
    - Star topology
    - All-to-all topology
- Leadless replication

  - Quorum

    - A quorum is the minimum number of votes that a distributed transaction has to obtain in order to be allowed to perform an operation in a distributed system.
    - A quorum-based technique is implemented to enforce consistent operation in a distributed system.
    - The quorum-based voting for replica control is due to [Gifford, 1979].[3] Each copy of a replicated data item is assigned a vote. Each operation then has to obtain a read quorum (Vr) or a write quorum (Vw) to read or write a data item, respectively. If a given data item has a total of V votes, the quorums have to obey the following rules:

      1. Vr + Vw > V
      2. Vw > V/2

## Partitioning and Secondary Indexes

- The situation becomes more complicated if secondary indexes are involved
- Secondary indexes are common in both relational and document DBs, and is the most important part of search servers (Solr, Elasticsearch)
- Main problem: secondary indexes don't map neatly to partitions
- Two main approaches

  - document-based partitioning
  - term-based partitioning

- ACID Definition

  - Atomicity
  - Consistency
  - Isolation
  - Durability

- Read phenomena
  - Dirty reads
    - A dirty read (aka uncommitted dependency) occurs when a transaction is allowed to read data from a row that has been modified by another running transaction and not yet committed.
  - Non-repeatable reads
    - A non-repeatable read occurs when, during the course of a transaction, a row is retrieved twice and the values within the row differ between reads.
  - Phantom reads
    - A phantom read occurs when, in the course of a transaction, new rows are added or removed by another transaction to the records being read.

## transaction isolation level

| transaction isolation level | Dirty Read | Unrepeatable Read | Phantom Read |
| --------------------------- | ---------- | ----------------- | ------------ |
| Read uncommitted            | YES        | YES               | YES          |
| Read committed              | NO         | YES               | YES          |
| Repreatable read            | NO         | NO                | YES          |
| Serializable                | NO         | NO                | NO           |

- Two-phase locking

  - In databases and transaction processing, two-phase locking (2PL) is a concurrency control method that guarantees serializability.

- Snapshot isolation

  - In databases, and transaction processing (transaction management), snapshot isolation is a guarantee that all reads made in a transaction will see a consistent snapshot of the database (in practice it reads the last committed values that existed at the time it started), and the transaction itself will successfully commit only if no updates it has made conflict with any concurrent updates made since that snapshot.

- Consensus algorithms
  - A fundamental problem in distributed computing and multi-agent systems is to achieve overall system reliability in the presence of a number of faulty processes.
- fencing token(ZooKeeper ID zxid or cversion)
  - simply a number that increases (e.g. incremented by the lock service) every time a client acquires the lock.
    - Uniqueness
    - Monotonic sequence
    - Availability
- Byzantine generals problem

  - a condition of a computer system, particularly distributed computing systems, where components may fail and there is imperfect information on whether a component has failed. The term takes its name from an allegory, the "Byzantine generals problem",[2] developed to describe a situation in which, in order to avoid catastrophic failure of the system, the system's actors must agree on a concerted strategy, but some of these actors are unreliable.

- Atomic broadcast

  - a broadcast where all correct processes in a system of multiple processes receive the same set of messages in the same order; that is, the same sequence of messages.[1][2] The broadcast is termed "atomic" because it either eventually completes correctly at all participants, or all participants abort without side effects. Atomic broadcasts are an important distributed computing primitive.

- Two-phase commit protocol

  - In transaction processing, databases, and computer networking, the two-phase commit protocol (2PC) is a type of atomic commitment protocol (ACP). It is a distributed algorithm that coordinates all the processes that participate in a distributed atomic transaction on whether to commit or abort (roll back) the transaction.

- Three-phase commit protocol
  - In computer networking and databases, the three-phase commit protocol (3PC) is a distributed algorithm which lets all nodes in a distributed system agree to commit a transaction. It is a more failure-resilient refinement of the two-phase commit protocol (2PC).

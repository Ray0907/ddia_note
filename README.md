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

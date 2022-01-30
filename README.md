Designing Data-Intensive Applidations
===
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
- Online transactional processing (OLTP) enables the real-time execution of large numbers of database transactions by large numbers of people, typically over the Internet.

# Shared-Disk Cluster

A **Shared-Disk Cluster** is a high-availability cluster configuration where all nodes have simultaneous access to a common storage system. Unlike shared-nothing clusters—where each node uses its own independent storage—in a shared-disk cluster, all nodes directly access the same disk subsystem (typically via a Storage Area Network or SAN).

## Key Characteristics

- **Common Storage Resource:**  
  All nodes share a single storage system, which allows for data consistency since every node reads from and writes to the same disk.

- **Cluster File Systems:**  
  To prevent data corruption, shared-disk clusters use specialized cluster file systems (such as GFS2, OCFS2, or Veritas Cluster File System) that coordinate access and implement locking mechanisms across nodes.

- **High Availability:**  
  If one node fails, other nodes in the cluster can continue to access the shared storage, ensuring continuous service availability.

- **Synchronized Data Access:**  
  Since all nodes share the same disk, data synchronization between nodes is inherently maintained, reducing the need for complex data replication strategies.

## Advantages

- **Data Consistency:**  
  With a single copy of the data accessible by all nodes, consistency is easier to maintain.
  
- **Simplified Data Management:**  
  There’s no need to replicate data between nodes because all nodes access the same physical storage.

- **High Availability:**  
  In the event of a node failure, other nodes can immediately take over without requiring data recovery from a separate source.

## Challenges

- **Scalability:**  
  The shared storage can become a bottleneck if many nodes attempt to access it simultaneously, limiting the cluster’s scalability.
  
- **Complexity in File System Management:**  
  A cluster file system must be used to coordinate disk access, which can be more complex to configure and maintain compared to standard file systems.
  
- **Single Point of Failure:**  
  The shared storage system itself must be highly available and redundant, as its failure could impact the entire cluster.

## Use Cases

- **Database Clusters:**  
  Shared-disk clusters are often used for database systems where consistent, concurrent access to data is critical.
  
- **File Servers:**  
  They are well-suited for file server clusters where multiple nodes need to access and update the same files.
  
- **Enterprise Applications:**  
  Applications requiring strong consistency and high availability, such as ERP systems, often leverage shared-disk clustering.

## Conclusion

A **Shared-Disk Cluster** enables multiple nodes to access the same storage directly, which simplifies data consistency and management. However, it requires a robust, highly available shared storage solution and a sophisticated cluster file system to manage concurrent access effectively. This architecture is particularly valuable in environments where data integrity is paramount and where the shared storage can be engineered to scale alongside the cluster.

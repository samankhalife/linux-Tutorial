# Quorum
**Quorum** is a fundamental concept in cluster computing and distributed systems that ensures data consistency and system reliability by making decisions based on the majority agreement (or "quorum") of nodes or members in a cluster. It is critical for preventing split-brain scenarios, ensuring data integrity, and maintaining the overall health of the cluster.

## Key Concepts of Quorum in Clusters:

1. **Definition of Quorum:**  
   Quorum refers to the minimum number of nodes (or votes) that must be active and in communication with each other to perform certain operations or make decisions. Quorum helps ensure that the cluster can continue to operate safely and that no two parts of the cluster can function independently in case of a network partition.

2. **Purpose of Quorum:**
   - Prevent **split-brain scenarios** (where two parts of the cluster operate independently without knowing the status of the other).
   - Ensure **data consistency** across nodes.
   - Allow safe **failover** and automatic recovery of services.

3. **Types of Quorum:**
   - **Simple Majority Quorum:**  
     More than half the nodes must be active for the cluster to remain operational. For example, in a 5-node cluster, at least 3 nodes must be active for quorum to be achieved.
   
   - **Weighted Quorum:**  
     Each node is assigned a vote count, and a certain number of votes are needed to achieve quorum. This allows for more flexible quorum management, such as giving higher-weighted votes to critical nodes.
   
   - **Tie-breaker Quorum:**  
     In a scenario where an even number of nodes are present, an additional "tie-breaker" mechanism (such as an external witness node) is used to break potential ties and prevent split-brain.
   
   - **Disk Quorum/Shared Disk Quorum:**  
     In certain setups, a shared storage device (such as a quorum disk) is used to hold the quorum vote. This ensures that the cluster nodes can check a common storage device to achieve quorum.

4. **Quorum in High-Availability Clusters:**
   In **high-availability (HA) clusters**, quorum ensures that the cluster only operates when a majority of nodes are online, thus avoiding data corruption or operational conflicts. Quorum is typically used to:
   - Allow **failover** of services in a multi-node cluster.
   - Decide which part of the cluster will continue operations during a network partition.
   - Trigger **fencing (STONITH)** to isolate or power down nodes that may cause inconsistencies.

5. **Quorum in Distributed Systems:**
   In distributed databases and systems (like Apache Cassandra, etcd, or Ceph), quorum-based mechanisms ensure that **replication** and **reads/writes** are consistent across multiple replicas. A certain number of nodes (quorum) must agree on updates before they are considered committed.

## Quorum Voting and Configuration:
   Many clustering software solutions (like **Pacemaker**, **Corosync**, **Microsoft Failover Clusters**) offer customizable quorum policies, including:
   - **Auto-quorum adjustment:** Automatically recalculates quorum when nodes are added or removed from the cluster.
   - **Quorum policy:** Configures what actions to take if quorum is lost (e.g., shutdown the cluster, continue in a degraded state).
   
   Configuration of quorum often involves setting:
   - **Quorum vote weights** to specific nodes.
   - Designating a **quorum witness** or tie-breaker.
   - Enabling **quorum disk** in clusters with shared storage.

## Conclusion:
Quorum is an essential mechanism for ensuring the safe and consistent operation of clusters and distributed systems. It avoids the split-brain issue, helps maintain high availability, and supports automatic failover and data replication consistency. Proper quorum configuration and monitoring are necessary to ensure the reliability of clustered environments.

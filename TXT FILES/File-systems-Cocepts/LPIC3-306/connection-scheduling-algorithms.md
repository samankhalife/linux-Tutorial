Linux Virtual Server (LVS) supports various connection scheduling algorithms to determine how client requests are distributed across real servers. These algorithms are essential for load balancing to ensure fair and efficient use of server resources. Below is an overview of the most common scheduling algorithms used by LVS:


## 1. **Round Robin (rr)**

- **Description:**  
  Distributes incoming requests to each real server in turn, without considering the server's load or current connections.
  
- **Advantages:**  
  - Simple to implement.
  - Provides even distribution if all servers have equal processing power.

- **Disadvantages:**  
  - Does not account for the current load or capacity of the servers, which can lead to imbalanced traffic distribution.

## 2. **Weighted Round Robin (wrr)**

- **Description:**  
  Similar to Round Robin but assigns a weight to each real server. Servers with higher weights receive more requests.
  
- **Advantages:**  
  - Allows for more powerful servers to handle a larger share of the load.
  
- **Disadvantages:**  
  - Static weights may not reflect changes in server load over time.

## 3. **Least Connection (lc)**

- **Description:**  
  Directs new requests to the server with the fewest active connections. This is useful when servers have similar processing power but varying levels of connection load.
  
- **Advantages:**  
  - Dynamically balances load based on the number of active connections.
  
- **Disadvantages:**  
  - May not always account for connection complexity or server performance differences.

## 4. **Weighted Least Connection (wlc)**

- **Description:**  
  A variant of Least Connection that also considers the weight of each server. Servers with higher weights can handle more connections.
  
- **Advantages:**  
  - Provides better balancing when servers have different capacities.
  
- **Disadvantages:**  
  - Weights are static, which may not adapt well to changing loads or server conditions.

## 5. **Locality-Based Least Connection (lblc)**

- **Description:**  
  Used in proxy-based setups (e.g., cache servers). Requests from the same client are sent to the same real server unless that server is overloaded.
  
- **Advantages:**  
  - Optimizes for locality, improving cache efficiency by keeping related requests on the same server.
  
- **Disadvantages:**  
  - Does not evenly distribute traffic in environments without proxy or cache considerations.

## 6. **Locality-Based Least Connection with Replication (lblcr)**

- **Description:**  
  Like `lblc`, but replicates connections across multiple servers to avoid overloading any single server. Used for heavy-load proxy services.
  
- **Advantages:**  
  - Offers better load distribution for proxy services while preserving locality.
  
- **Disadvantages:**  
  - Increased overhead for connection replication.

## 7. **Destination Hashing (dh)**

- **Description:**  
  Uses a hash of the destination IP address to determine the server. This ensures that requests for the same destination IP always go to the same real server, ideal for services where session persistence is needed.
  
- **Advantages:**  
  - Maintains session persistence by directing traffic to the same server based on the destination IP.
  
- **Disadvantages:**  
  - Does not adapt to changes in server load or performance.

## 8. **Source Hashing (sh)**

- **Description:**  
  Uses a hash of the source IP address to assign requests to real servers. Similar to `dh`, this algorithm is useful for maintaining session persistence.
  
- **Advantages:**  
  - Maintains session persistence by directing all requests from the same client to the same server.
  
- **Disadvantages:**  
  - Does not balance load based on server performance or connection count.

## 9. **Shortest Expected Delay (sed)**

- **Description:**  
  A dynamic algorithm that selects the server with the lowest expected delay based on the number of active connections and the server’s weight.
  
- **Advantages:**  
  - More efficient than Least Connection for balancing servers with different capacities.
  
- **Disadvantages:**  
  - Requires more overhead for calculating expected delays.

## 10. **Never Queue (nq)**

- **Description:**  
  Forwards requests only to servers that are not currently queued, ensuring requests are handled as quickly as possible. If all servers are queued, it reverts to a least connection approach.
  
- **Advantages:**  
  - Minimizes request latency by avoiding busy servers.
  
- **Disadvantages:**  
  - Not ideal for environments with significant load or where all servers are equally busy.

---

### Summary Table:

| **Algorithm**                          | **Advantages**                                                                 | **Disadvantages**                                                       |
|----------------------------------------|-------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Round Robin (rr)**                   | Simple, even distribution.                                                   | Does not account for server load.                                       |
| **Weighted Round Robin (wrr)**         | Better for servers with unequal capacities.                                  | Static weights; does not adapt to changing loads.                       |
| **Least Connection (lc)**              | Dynamically balances based on active connections.                            | Does not account for server performance differences.                    |
| **Weighted Least Connection (wlc)**    | Considers both connection count and server capacity.                         | Static weights may not reflect current load.                            |
| **Locality-Based Least Connection (lblc)** | Optimizes for locality, improving cache hit rates.                           | Imbalanced traffic in non-proxy setups.                                 |
| **Locality-Based Least Connection Replication (lblcr)** | Better distribution for proxy services.                                     | Connection replication overhead.                                        |
| **Destination Hashing (dh)**           | Ensures session persistence based on destination IP.                         | Does not adapt to changing server conditions.                           |
| **Source Hashing (sh)**                | Maintains session persistence based on client IP.                           | Does not balance load or connection count.                              |
| **Shortest Expected Delay (sed)**      | Selects server with the lowest expected delay.                               | Higher overhead for delay calculation.                                  |
| **Never Queue (nq)**                   | Avoids servers with queued requests, reducing response time.                 | Falls back to least connection if all servers are busy.                 |


### Conclusion:

The selection of a connection scheduling algorithm depends on the specific use case and environment:

- **Round Robin** is best for simple setups with similar-capacity servers.
- **Least Connection** is ideal for dynamic environments with varying connection loads.
- **Locality-based algorithms** (LBLCR, LBLC) optimize caching systems.
- **Hash-based algorithms** (DH, SH) work well in environments that require session persistence.
- **Shortest Expected Delay** is beneficial for balancing servers with different capacities and connection handling speeds.

Selecting the right algorithm can significantly enhance load balancing efficiency, ensuring a more reliable and scalable network infrastructure.

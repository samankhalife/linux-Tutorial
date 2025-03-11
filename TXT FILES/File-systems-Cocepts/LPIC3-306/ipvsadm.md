# ipvsadm

**ipvsadm** is a command-line administration tool used to manage IP Virtual Server (IPVS) functionality in the Linux kernel. IPVS is a load balancing technology that directs network traffic to various backend servers, enabling efficient distribution of requests and ensuring high availability.

## Key Features and Uses

- **Load Balancing:**  
  IPVS acts as a transport layer load balancer, distributing incoming network connections (typically for TCP and UDP services) across multiple real servers (backend nodes).

- **Connection Tracking:**  
  It keeps track of connections, ensuring that subsequent packets from the same client are directed to the same server (session persistence).

- **High Availability:**  
  When combined with tools like keepalived, ipvsadm helps build highly available and scalable service clusters.

## Basic Operations

**ipvsadm** supports several key operations:

- **Listing IPVS Table:**  
  To display the current IPVS table (virtual services and real servers):
  ```bash
  ipvsadm -L -n
  ```
  The `-L` flag lists the table, and `-n` shows numeric addresses (faster and avoids DNS lookups).

- **Adding a Virtual Service:**  
  You can add a virtual service (VIP) and configure it to forward connections to a set of real servers:
  ```bash
  ipvsadm -A -t 192.168.1.100:80 -s rr
  ```
  Here, `-A` adds a TCP service on port 80 with a round-robin scheduling algorithm (`-s rr`).

- **Adding Real Servers:**  
  Once a virtual service is defined, you can add real servers to it:
  ```bash
  ipvsadm -a -t 192.168.1.100:80 -r 192.168.1.101:80 -m
  ```
  The `-a` flag adds a real server; `-r` specifies the real server’s IP and port; `-m` indicates direct routing (masq and tunnel options are also available).

- **Deleting a Service or Server:**  
  To remove a service or a real server from the IPVS table:
  ```bash
  ipvsadm -D -t 192.168.1.100:80
  ```
  The `-D` flag deletes the specified virtual service or real server.

## Scheduling Algorithms

**ipvsadm** supports multiple scheduling algorithms, such as:
- **rr (Round Robin):** Distributes requests evenly.
- **wrr (Weighted Round Robin):** Distributes requests based on server weight.
- **lc (Least Connection):** Directs traffic to the server with the fewest active connections.
- **wlc (Weighted Least Connection):** Similar to lc but considers weights.
- **sh (Source Hashing):** Ensures the same client IP always maps to the same server.

## Integration and Usage

- **Keepalived:**  
  **ipvsadm** is often used in conjunction with keepalived to manage virtual IP addresses and provide failover capabilities.
  
- **High-Performance Environments:**  
  IPVS is designed to handle high volumes of traffic with minimal overhead, making it suitable for high-performance web services and large-scale applications.



## Conclusion

**ipvsadm** is a powerful and versatile tool for administering the IP Virtual Server in Linux. It enables administrators to set up and manage load balancing configurations efficiently, ensuring that network traffic is distributed across multiple backend servers. This contributes to both performance and high availability in distributed systems.

For more details and advanced options, you can refer to the official man page or relevant documentation online.

citeipvsadm-manpage

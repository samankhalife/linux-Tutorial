# ldirectord Configuration File

**ldirectord** is a daemon from the Linux Virtual Server (LVS) project used to monitor the health of real servers behind a load-balanced virtual IP (VIP) and to update the IPVS (IP Virtual Server) table accordingly. Its configuration file, typically located at `/etc/ldirectord.conf`, defines global settings, health check parameters, virtual server definitions, and real server details.

## Key Sections and Directives

### 1. **Global Settings**

Global parameters control the overall behavior of ldirectord. Common directives include:

- **checkinterval:**  
  Specifies how often (in seconds) ldirectord performs health checks on the real servers.
  ```conf
  checkinterval=2
  ```
  
- **autorestart:**  
  Enables automatic restart of the service if ldirectord detects issues.
  ```conf
  autorestart=yes
  ```
  
- **configfile:**  
  Indicates the location of the configuration file. This is often implicit.
  
- **debug:**  
  Enables debug logging for troubleshooting.
  ```conf
  debug=yes
  ```

### 2. **Virtual Server Definition**

This section defines the VIP and associated service parameters that ldirectord will manage. Key directives include:

- **virtual=VIP:port:**  
  The virtual server's IP address and port that clients connect to.
  ```conf
  virtual=192.168.1.100:80
  ```

- **scheduler:**  
  Specifies the load balancing algorithm used by IPVS (e.g., round-robin, least-connection).
  ```conf
  scheduler=rr
  ```

- **protocol:**  
  The protocol for the virtual service (usually TCP or UDP).
  ```conf
  protocol=tcp
  ```

- **service:**  
  Defines the type of service being monitored. This is sometimes used in conjunction with health checks.

### 3. **Real Server Definition**

Within the virtual server block, real servers (the actual backend servers) are defined. For each real server, you specify:

- **real=IP:port:**  
  The IP address and port of a real server that will receive traffic.
  ```conf
  real=192.168.1.101:80
  real=192.168.1.102:80
  ```

- **weight:**  
  (Optional) The weight assigned to a real server to influence load distribution.
  ```conf
  weight=1
  ```

### 4. **Health Check Configuration**

ldirectord uses health check methods to determine the availability of real servers. Common directives include:

- **method:**  
  The method used for health checking, such as HTTP, TCP, or ICMP.
  ```conf
  method=http
  ```

- **request:**  
  The HTTP request to be sent for an HTTP check.
  ```conf
  request="GET / HTTP/1.0\r\n\r\n"
  ```

- **expect:**  
  A string or regular expression that must be present in the response for the check to pass.
  ```conf
  expect="200 OK"
  ```

- **fall:**  
  The number of consecutive failed checks before marking a real server as down.
  ```conf
  fall=3
  ```

- **rise:**  
  The number of consecutive successful checks required to mark a real server as up.
  ```conf
  rise=2
  ```

### Sample Configuration

Below is an example of a typical `ldirectord.conf` file:

```conf
# Global settings
checkinterval=2
autorestart=yes
debug=yes

# Virtual server configuration
virtual=192.168.1.100:80
scheduler=rr
protocol=tcp

# Health check configuration for HTTP service
method=http
request="GET / HTTP/1.0\r\n\r\n"
expect="200 OK"
fall=3
rise=2

# Real server definitions
real=192.168.1.101:80
weight=1

real=192.168.1.102:80
weight=1
```

## Best Practices

- **Consistency:**  
  Ensure that all parameters, especially health check directives, are consistently defined to avoid false positives or negatives in server availability.

- **Testing:**  
  Test configuration changes in a staging environment before applying them to production. Use the debug mode (`debug=yes`) for detailed logs during testing.

- **Backup:**  
  Always back up your configuration file before making changes.

- **Monitoring:**  
  Regularly monitor the ldirectord logs to ensure that health checks are performing as expected and that real server status changes are correctly reflected in the IPVS table.


## Conclusion

The **ldirectord** configuration file is central to how LVS implements load balancing and high availability. By defining global settings, virtual server parameters, real server details, and health check criteria, administrators can control traffic distribution and maintain service reliability. With careful configuration and adherence to best practices, ldirectord helps ensure that client requests are efficiently routed to healthy real servers, contributing to a robust and responsive network service environment.

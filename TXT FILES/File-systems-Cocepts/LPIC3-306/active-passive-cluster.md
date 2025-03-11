In an **active-passive cluster** configuration, one node (the active node) handles all incoming traffic, while the other node (the passive node) remains on standby, ready to take over if the active node fails. This setup ensures high availability and fault tolerance for critical services.

**Implementing Active-Passive Clustering with HAProxy**

HAProxy can be configured to support active-passive clustering, often in conjunction with tools like Keepalived or Pacemaker to manage failover and virtual IP addresses. Here's how you can set up such a configuration:

1. **Install HAProxy on Both Nodes:**
   Ensure that HAProxy is installed on both the active and passive nodes.

2. **Configure HAProxy:**
   Set up HAProxy on both nodes to listen on the same virtual IP address. On the active node, configure HAProxy to bind to the virtual IP:

   ```haproxy
   frontend http_front
       bind 192.168.1.100:80
       default_backend http_back
   ```


   On the passive node, configure HAProxy similarly:

   ```haproxy
   frontend http_front
       bind 192.168.1.100:80
       default_backend http_back
   ```


3. **Set Up Keepalived for Virtual IP Management:**
   Use Keepalived to manage the virtual IP address and handle failover between the active and passive nodes. Keepalived uses the Virtual Router Redundancy Protocol (VRRP) to assign a virtual IP to one node at a time.

   On the active node, configure Keepalived with a higher priority:

   ```bash
   vrrp_instance VI_1 {
       state MASTER
       interface eth0
       virtual_router_id 51
       priority 101
       virtual_ipaddress {
           192.168.1.100
       }
   }
   ```


   On the passive node, configure Keepalived with a lower priority:

   ```bash
   vrrp_instance VI_1 {
       state BACKUP
       interface eth0
       virtual_router_id 51
       priority 100
       virtual_ipaddress {
           192.168.1.100
       }
   }
   ```


4. **Enable and Start Services:**
   Enable and start both HAProxy and Keepalived on both nodes:

   ```bash
   sudo systemctl enable haproxy keepalived
   sudo systemctl start haproxy keepalived
   ```


In this setup, Keepalived ensures that only one node holds the virtual IP at any time. If the active node fails, Keepalived promotes the passive node to active status, allowing HAProxy on that node to start handling traffic. citeturn0search5

**Alternative with Pacemaker and Corosync**

Alternatively, you can use Pacemaker and Corosync to manage the cluster's resources and failover:

1. **Install Pacemaker and Corosync:**
   Install these tools on both nodes to handle cluster management and communication.

2. **Configure Cluster Resources:**
   Define resources for HAProxy and the virtual IP address in Pacemaker. Pacemaker will monitor these resources and manage failover between nodes. citeturn0search6

**Considerations**

- **Health Checks:** Configure HAProxy to perform health checks on backend servers to ensure traffic is only directed to healthy servers.

- **Session Persistence:** If your application requires session persistence, ensure that HAProxy is configured to handle sticky sessions appropriately.

- **Testing Failover:** Regularly test failover scenarios to ensure that the passive node can successfully take over in case of an active node failure.

By implementing an active-passive cluster with HAProxy and appropriate failover management tools, you can achieve high availability and reliability for your services. 

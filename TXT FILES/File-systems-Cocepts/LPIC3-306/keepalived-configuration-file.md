# Keepalived Configuration File

The keepalived configuration file, typically located at **`/etc/keepalived/keepalived.conf`**, is used to configure keepalived for load balancing and high availability. The configuration is written in plain text and is divided into several sections, each with its specific purpose.

## Main Sections

### 1. **global_defs**

This section sets global parameters that affect the overall behavior of keepalived.

- **notification_email:**  
  Email address to which notifications should be sent.
- **notification_email_from:**  
  The sender’s email address for notifications.
- **smtp_server:**  
  The SMTP server used to send notification emails.
- **smtp_connect_timeout:**  
  Timeout for connecting to the SMTP server.
- **router_id:**  
  A unique identifier for the router or the keepalived instance.

*Example:*
```conf
global_defs {
    notification_email {
        to      admin@example.com
        from    keepalived@example.com
        smtp_server 192.168.1.1
        smtp_connect_timeout 30
    }
    router_id LVS_DEVEL
}
```

### 2. **vrrp_instance**

This section is used to define VRRP (Virtual Router Redundancy Protocol) instances, which are essential for managing virtual IP addresses (VIPs) for high availability.

- **state:**  
  Indicates whether the instance starts in MASTER or BACKUP state.
- **interface:**  
  The network interface used for VRRP communication.
- **virtual_router_id:**  
  A unique identifier for the VRRP instance.
- **priority:**  
  Determines the master in the VRRP group (higher priority wins).
- **advert_int:**  
  The interval (in seconds) at which VRRP advertisements are sent.
- **virtual_ipaddress:**  
  List of VIPs managed by this instance.

*Example:*
```conf
vrrp_instance VI_1 {
    state MASTER
    interface eth0
    virtual_router_id 51
    priority 101
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass mypassword
    }
    virtual_ipaddress {
        192.168.1.100
    }
}
```

### 3. **virtual_server**

This section configures virtual servers for load balancing. It directs client requests from the virtual IP to a group of real servers.

- **virtual_ipaddress:**  
  The VIP that clients connect to.
- **delay_loop:**  
  Interval in seconds between health check loops.
- **lb_algo:**  
  Load balancing algorithm (e.g., rr for round-robin, wrr for weighted round-robin, lc for least-connection).
- **lb_kind:**  
  The load balancing method (e.g., NAT, DR, TUN).
- **protocol:**  
  The protocol (usually TCP or UDP).
- **real_server:**  
  Blocks that define real servers that will handle the traffic.

*Example:*
```conf
virtual_server 192.168.1.100 80 {
    delay_loop 6
    lb_algo rr
    lb_kind NAT
    protocol TCP

    real_server 192.168.1.101 80 {
        weight 1
        TCP_CHECK {
            connect_timeout 3
            nb_get_retry 3
            delay_before_retry 3
            connect_port 80
        }
    }
    real_server 192.168.1.102 80 {
        weight 1
        TCP_CHECK {
            connect_timeout 3
            nb_get_retry 3
            delay_before_retry 3
            connect_port 80
        }
    }
}
```

## Additional Sections

- **track_script:**  
  Allows keepalived to monitor custom scripts and use their exit status to adjust resource priority or trigger notifications.
  
*Example:*
```conf
track_script {
    script "pidof my_app"
    interval 2
    weight -20
}
```

- **smtp_alert:**  
  Can be configured for sending alerts via email when a VRRP instance changes state.

## Best Practices

- **Consistent Configuration:**  
  Ensure that all nodes in the cluster share the same keepalived configuration, especially the VRRP settings, to avoid conflicts.
- **Security:**  
  Use strong authentication for VRRP (e.g., a strong password with `auth_type PASS`) to prevent unauthorized takeovers.
- **Testing:**  
  Test configuration changes in a controlled environment before deploying to production.
- **Backup:**  
  Always keep a backup of the configuration file before making any modifications.



## Conclusion

The keepalived configuration file is central to setting up high availability and load balancing on Linux systems. It combines VRRP for managing virtual IP addresses with load balancing configurations to distribute client requests among real servers effectively. With careful planning and adherence to best practices, keepalived helps ensure that your network services remain resilient and available.

For more details and examples, you can refer to the official documentation and community guides on keepalived configuration.


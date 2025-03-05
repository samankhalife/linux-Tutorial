# ipactl
The `ipactl` command is used in FreeIPA to manage the IPA services on the server. It provides a convenient way to start, stop, restart, and check the status of all IPA services at once.

### **Common `ipactl` Commands**

1. **Check IPA Services Status**:
   ```bash
   ipactl status
   ```
   This command shows the status of all the IPA-related services, such as Directory Server (LDAP), Kerberos, DNS, and HTTP services, among others.

   Example:
   ```bash
   # ipactl status
   ```

   **Output** (example):
   ```
   Directory Service: RUNNING
   KDC Service: RUNNING
   KPASSWD Service: RUNNING
   HTTP Service: RUNNING
   DNS Service: RUNNING
   ```

2. **Start IPA Services**:
   ```bash
   ipactl start
   ```
   Starts all the IPA services on the system. This is useful after system reboots or maintenance.

   Example:
   ```bash
   # ipactl start
   ```

3. **Stop IPA Services**:
   ```bash
   ipactl stop
   ```
   Stops all the IPA services on the system. This can be useful for troubleshooting, planned maintenance, or shutting down the server gracefully.

   Example:
   ```bash
   # ipactl stop
   ```

4. **Restart IPA Services**:
   ```bash
   ipactl restart
   ```
   Restarts all IPA services. Useful after configuration changes or to recover from certain types of issues.

   Example:
   ```bash
   # ipactl restart
   ```

5. **Enable IPA Services on Boot**:
   By default, `ipactl` ensures that all IPA-related services start automatically during system boot. However, if required, you can use the system’s service manager (like `systemctl` in RHEL/CentOS 7 and above) to ensure the FreeIPA services start on boot.

   Example:
   ```bash
   systemctl enable ipa.service
   ```

### **Services Managed by `ipactl`**

`ipactl` manages multiple services critical to FreeIPA, including:

- **Directory Server (LDAP)** – Manages the LDAP directory services.
- **KDC (Kerberos Key Distribution Center)** – Manages Kerberos authentication.
- **KPASSWD** – Manages password changes via Kerberos.
- **HTTPD (Apache)** – Manages the web interface and HTTP services for IPA.
- **DNS (if configured)** – Manages DNS services, including DNSSEC.
- **Certmonger** – Manages certificate renewal.

### **Use Case: Restarting IPA Services After a Change**

If you’ve made configuration changes to the FreeIPA setup or encountered issues with services not responding, you can restart all IPA-related services with:
```bash
ipactl restart
```
This ensures that the changes are applied across all relevant services.

---

### **Conclusion**

The `ipactl` command is a simple and powerful utility to manage all services related to FreeIPA. It provides system administrators with the ability to control, monitor, and maintain the health of IPA services from a single interface, making it an essential tool for managing FreeIPA servers.

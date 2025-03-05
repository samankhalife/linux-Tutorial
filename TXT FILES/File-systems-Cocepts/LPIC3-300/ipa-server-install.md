# ipa-server-install
`ipa-server-install` is the command used to set up a new FreeIPA server. FreeIPA (Identity, Policy, and Audit) is an integrated solution for centralized identity management, authentication, and authorization in Linux and Unix environments. The `ipa-server-install` command is crucial for initializing and configuring an IPA server, which will act as the primary server for managing users, groups, hosts, and services.

### **Purpose**
This command installs and configures an IPA server with various services like:
- 389 Directory Server (LDAP)
- Kerberos (KDC)
- DNS (optional)
- NTP or Chrony (optional)
- PKI (Dogtag Certificate System)
- HTTP server

The installation includes setting up an LDAP directory, configuring Kerberos authentication, and other optional services such as DNS and certificate authorities.

### **Basic Usage**

```bash
ipa-server-install [options]
```

### **Key Options**

- **`--hostname`**: Specifies the fully qualified domain name (FQDN) of the server.
  
  Example:
  ```bash
  ipa-server-install --hostname=ipa.example.com
  ```

- **`--realm`**: Specifies the Kerberos realm. It is usually the domain name in uppercase.
  
  Example:
  ```bash
  ipa-server-install --realm=EXAMPLE.COM
  ```

- **`--domain`**: Specifies the domain name for the IPA server.
  
  Example:
  ```bash
  ipa-server-install --domain=example.com
  ```

- **`--ds-password`**: The password for the Directory Server's admin user (`cn=Directory Manager`).

  Example:
  ```bash
  ipa-server-install --ds-password=supersecretpassword
  ```

- **`--admin-password`**: The password for the FreeIPA admin account (`admin` user).
  
  Example:
  ```bash
  ipa-server-install --admin-password=adminpassword
  ```

- **`--setup-dns`**: Installs and configures the DNS server as part of the FreeIPA setup. This option is used if you want FreeIPA to manage DNS.
  
  Example:
  ```bash
  ipa-server-install --setup-dns
  ```

- **`--no-host-dns`**: Skips the creation of DNS records for the host in the DNS server.
  
  Example:
  ```bash
  ipa-server-install --no-host-dns
  ```

- **`--no-ntp` or `--no-chrony`**: Skips the installation of NTP or Chrony for time synchronization. By default, `ipa-server-install` installs either NTP or Chrony, but you can opt out with these flags.
  
  Example:
  ```bash
  ipa-server-install --no-ntp
  ```

- **`--idstart` and `--idmax`**: Define the range of UID/GID values to be used by FreeIPA for user and group IDs.

  Example:
  ```bash
  ipa-server-install --idstart=1000 --idmax=2000
  ```

- **`--no-pkinit`**: Disables PKINIT (Public Key Cryptography for Initial Authentication in Kerberos).

  Example:
  ```bash
  ipa-server-install --no-pkinit
  ```

- **`--external-ca`**: Use this option if you're integrating FreeIPA with an external certificate authority. This will generate a Certificate Signing Request (CSR) for submission to the external CA.

  Example:
  ```bash
  ipa-server-install --external-ca
  ```

- **`--unattended`**: Use this for unattended installations, where the system does not prompt for input, and all required data is provided via command-line options.

  Example:
  ```bash
  ipa-server-install --unattended
  ```

### **Installation Process**
1. **Prepare the Environment**:
   Ensure that DNS is properly configured and the FQDN of the server resolves correctly.

2. **Run `ipa-server-install`**:
   Execute the `ipa-server-install` command with the necessary options.

   Example:
   ```bash
   ipa-server-install --hostname=ipa.example.com --realm=EXAMPLE.COM --domain=example.com --admin-password=adminpassword --ds-password=supersecretpassword
   ```

3. **Set up DNS (Optional)**:
   If you're setting up DNS with FreeIPA, make sure to provide the DNS-related options (`--setup-dns`, `--no-host-dns`, etc.).

4. **Provide Passwords**:
   During the installation, you'll be asked to provide passwords for the Directory Manager and the admin user unless provided as command-line options.

5. **Verify Time Synchronization**:
   Make sure that time is synchronized across all systems, as FreeIPA relies on Kerberos, which requires accurate time settings.

6. **Complete the Setup**:
   Once the installation is complete, the server will be fully set up and ready to manage identity services.

### **Post-Installation Steps**
After installation, you can verify the status of the FreeIPA server using:

```bash
ipactl status
```

To add users, groups, and manage the FreeIPA server, you can use the `ipa` command-line tools.

For example:
- To add a user:
  ```bash
  ipa user-add johndoe --first=John --last=Doe
  ```

- To add a group:
  ```bash
  ipa group-add engineers --desc="Engineering Team"
  ```

### **Common Issues and Troubleshooting**

- **DNS Resolution**: Ensure the FQDN resolves properly, as DNS issues can cause the installation to fail.
- **Ports**: Ensure that the necessary ports (e.g., 389 for LDAP, 88 for Kerberos, 53 for DNS if configured) are open and accessible.
- **Time Sync**: Kerberos relies on synchronized clocks, so ensure that NTP or Chrony is configured correctly.
- **Firewall**: Ensure that your firewall settings allow the necessary communication (e.g., LDAP, Kerberos, HTTP).

### **Conclusion**
The `ipa-server-install` command sets up a new FreeIPA server with services like LDAP, Kerberos, and DNS. By configuring these services, it centralizes authentication and policy management across Linux/Unix systems, reducing administrative overhead. The installation process is flexible, allowing options for DNS management, certificate authorities, and unattended installs for automated environments.

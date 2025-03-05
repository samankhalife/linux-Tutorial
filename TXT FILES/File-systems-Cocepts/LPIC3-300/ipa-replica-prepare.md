# ipa-replica-prepare
The `ipa-replica-prepare` command is used in FreeIPA to prepare a replica server for installation. It generates the necessary data files required to configure a new replica, including replication agreements and the necessary configuration for the new server. These files are transferred to the system where the replica will be installed and used with the `ipa-replica-install` command.

### **Purpose**
The command creates a GPG-encrypted file that contains all the required information for the replica installation, which includes data like Kerberos configuration, CA certificates, and LDAP replication information.

### **Usage**

```bash
ipa-replica-prepare [options] replica-fqdn
```

Where:
- `replica-fqdn` is the fully qualified domain name (FQDN) of the replica you want to install.

### **Steps to Prepare for Replica Installation**

1. **Prepare the Master IPA Server**:
   Run the `ipa-replica-prepare` command on the existing master FreeIPA server.

   Example:
   ```bash
   sudo ipa-replica-prepare replica.example.com
   ```

   This generates a GPG file, typically located in `/var/lib/ipa/` directory, with a name like `replica-info-replica.example.com.gpg`.

2. **Copy the Replica File to the Replica Machine**:
   You need to transfer the generated GPG file to the system where you intend to install the replica. This can be done using `scp` or any other secure file transfer method.

   Example:
   ```bash
   scp /var/lib/ipa/replica-info-replica.example.com.gpg root@replica.example.com:/tmp
   ```

3. **Run ipa-replica-install on the Replica**:
   On the new system (replica server), use the `ipa-replica-install` command along with the replica information file.

   Example:
   ```bash
   sudo ipa-replica-install /tmp/replica-info-replica.example.com.gpg
   ```

### **Key Options for ipa-replica-prepare**

- **`--ip-address`**: 
   This option allows you to specify the IP address of the replica.

   Example:
   ```bash
   ipa-replica-prepare replica.example.com --ip-address=192.168.1.100
   ```

- **`--no-reverse`**: 
   Disables the creation of a reverse DNS zone. This is useful if you don’t want the installation process to create a reverse DNS record for the replica server.

   Example:
   ```bash
   ipa-replica-prepare replica.example.com --no-reverse
   ```

- **`--no-pkinit`**: 
   Disables PKINIT (Public Key Cryptography for Initial Authentication in Kerberos) on the replica.

   Example:
   ```bash
   ipa-replica-prepare replica.example.com --no-pkinit
   ```

- **`--dirsrv-cert-file`**: 
   Specifies the directory server’s certificate for the replica, useful when the certificate already exists or is pre-configured.

   Example:
   ```bash
   ipa-replica-prepare replica.example.com --dirsrv-cert-file=/path/to/cert.pem
   ```

- **`--http-cert-file`**: 
   Similar to the above but for the HTTP server.

   Example:
   ```bash
   ipa-replica-prepare replica.example.com --http-cert-file=/path/to/cert.pem
   ```

- **`--skip-schema-check`**: 
   Skips the schema check on the master during preparation. This option is rarely used but may be necessary in specific scenarios where schema conflicts might exist.

   Example:
   ```bash
   ipa-replica-prepare replica.example.com --skip-schema-check
   ```

### **Post-Preparation Steps**

Once the replica preparation is done and the replica information file has been generated:

1. **Transfer the File**: Copy the `.gpg` file to the replica machine.
2. **Run `ipa-replica-install`**: Use the file to complete the replica installation on the replica server.
3. **Verify Replica**: Once the installation is done, ensure that replication is working correctly by using commands like `ipa-replica-manage list` or checking the status of FreeIPA services using `ipactl status`.

### **Common Issues and Troubleshooting**

- **DNS and Hostname**: Make sure that DNS and hostname resolution work correctly between the master and replica servers.
- **Network Connectivity**: Ensure that all necessary ports (e.g., 389 for LDAP, 88 for Kerberos, etc.) are open between the master and replica systems.
- **Time Synchronization**: Ensure both the master and replica servers have synchronized system clocks (e.g., through NTP), as time discrepancies can cause issues with Kerberos authentication.
- **Certificates**: If using custom certificates for the replica, make sure they are valid and properly configured.

### **Conclusion**

The `ipa-replica-prepare` command is an essential step in setting up a replica FreeIPA server. It creates the necessary configuration and replication information for the replica to be installed. By preparing the replica on the master server and then installing it using `ipa-replica-install`, you ensure redundancy, load balancing, and increased availability in your FreeIPA domain.

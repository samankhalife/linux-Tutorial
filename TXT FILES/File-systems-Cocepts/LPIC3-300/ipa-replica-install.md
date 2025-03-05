# ipa-replica-install
The `ipa-replica-install` command is used to install a FreeIPA replica server. A replica server acts as a redundant IPA server, allowing load balancing, failover, and increased availability for the FreeIPA infrastructure. Installing a replica ensures that essential services such as Kerberos authentication, DNS, LDAP directory services, and other IPA services continue to operate even if the primary IPA server goes down.

### **Basic Usage**

```bash
ipa-replica-install [options]
```

### **Requirements for a Replica**

- The FreeIPA master server should already be installed and running.
- The system should meet the required dependencies, like DNS, Kerberos, etc.
- You should have administrative credentials to the IPA master.
- The replica system should have its hostname and domain set up properly.

### **Replica Installation Process**

1. **Install FreeIPA Packages**: 
   Ensure the FreeIPA server packages are installed on the replica machine. 

   Example:
   ```bash
   sudo yum install ipa-server
   ```

2. **Prepare Replica on Master**:
   On the primary IPA master, generate the replica file that will be used during the installation. This can be done using `ipa-replica-prepare`.

   Example:
   ```bash
   sudo ipa-replica-prepare replica.example.com
   ```

   This command will generate a file (typically `.gpg` file) that contains configuration data for the replica.

3. **Copy Replica File**:
   Copy the replica file to the machine where you want to set up the replica (e.g., using `scp`).

   Example:
   ```bash
   scp /var/lib/ipa/replica-info-replica.example.com.gpg replica.example.com:/tmp
   ```

4. **Run ipa-replica-install**:
   Once the replica file is on the replica server, run `ipa-replica-install` to install the replica.

   Example:
   ```bash
   sudo ipa-replica-install /tmp/replica-info-replica.example.com.gpg
   ```

### **Key Options**

- **`--setup-ca`**: 
   This option installs a Certificate Authority (CA) on the replica. It’s useful if you want to distribute CA services across multiple IPA servers.

   Example:
   ```bash
   --setup-ca
   ```

- **`--setup-dns`**: 
   This option installs DNS services on the replica. This allows DNS records to be updated on the replica as well, rather than relying solely on the master.

   Example:
   ```bash
   --setup-dns
   ```

- **`--no-pkinit`**: 
   Disables PKINIT (Public Key Cryptography for Initial Authentication in Kerberos) on the replica.

   Example:
   ```bash
   --no-pkinit
   ```

- **`--unattended`**: 
   Run the installation without user interaction. This is useful when automating the process with scripts.

   Example:
   ```bash
   --unattended
   ```

- **`--force`**: 
   Forces the reinstallation of a replica if it's already configured.

   Example:
   ```bash
   --force
   ```

### **Example Commands**

1. **Install Replica with CA and DNS**:
   If you want to install a replica with both CA and DNS services, use:

   ```bash
   sudo ipa-replica-install /tmp/replica-info-replica.example.com.gpg --setup-ca --setup-dns
   ```

2. **Install Replica in Unattended Mode**:
   This command will install the replica non-interactively:

   ```bash
   sudo ipa-replica-install /tmp/replica-info-replica.example.com.gpg --unattended
   ```

3. **Install Replica Without Setting up CA**:
   To install a replica without a Certificate Authority:

   ```bash
   sudo ipa-replica-install /tmp/replica-info-replica.example.com.gpg --no-pkinit
   ```

### **Post-Installation**

After the installation, the replica server should be synchronized with the primary IPA server and function as a full IPA server in the FreeIPA domain. You can verify the replica by:

1. **Check IPA Status**:
   ```bash
   sudo ipactl status
   ```
   This command will show the status of various IPA-related services (e.g., Kerberos, LDAP, DNS).

2. **Replica Management**:
   The replica should automatically synchronize data such as user information and policies from the master. You can use standard IPA commands like `ipa-replica-manage` to manage replication between servers.

3. **Testing Failover**:
   Shut down the master server temporarily and verify if authentication services like Kerberos still work, to ensure the replica is operating correctly.

### **Uninstalling a Replica**

To remove a replica from the domain, you can use:

```bash
ipa-replica-manage del replica.example.com
```

And then:

```bash
sudo ipa-server-install --uninstall
```

This will clean up the replica and remove it from the IPA domain.

---

### **Conclusion**

The `ipa-replica-install` command is crucial for ensuring high availability and redundancy in a FreeIPA domain. By configuring multiple replicas, you can distribute the load across servers, provide failover capabilities, and increase the resilience of your authentication and identity management infrastructure. The process involves preparing the replica on the master, copying necessary configuration files, and running the `ipa-replica-install` command on the replica machine.

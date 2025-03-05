# ipa-client-install
The `ipa-client-install` command is used to configure a Linux machine as a FreeIPA client, allowing it to authenticate users, manage host information, and use Kerberos services provided by an IPA server. This tool helps in integrating the client machine into the FreeIPA domain, managing users and services centrally.

### **Basic Usage**

```bash
ipa-client-install [options]
```

### **Steps for Client Installation**

1. **Install FreeIPA Client Package**: 
   If not installed, you'll need to first install the FreeIPA client package on the machine.
   ```bash
   sudo yum install ipa-client
   # or on Debian/Ubuntu systems:
   sudo apt-get install freeipa-client
   ```

2. **Run the Installation Command**:
   Once the package is installed, run the `ipa-client-install` command with appropriate options to join the machine to the IPA domain.

   Example:
   ```bash
   sudo ipa-client-install --domain=example.com --server=ipa.example.com --realm=EXAMPLE.COM
   ```

3. **Interactive Installation**: 
   If you don’t specify all options, the command will prompt you interactively for the required information, such as the IPA server’s FQDN, realm, and admin credentials.

### **Key Options**

- **`--domain=DOMAIN`**: 
   Specifies the DNS domain name of the IPA server.
   
   Example:
   ```bash
   --domain=example.com
   ```

- **`--server=SERVER`**: 
   The fully qualified domain name (FQDN) of the IPA server.
   
   Example:
   ```bash
   --server=ipa.example.com
   ```

- **`--realm=REALM`**: 
   The Kerberos realm for the IPA server (usually the uppercase version of the domain).
   
   Example:
   ```bash
   --realm=EXAMPLE.COM
   ```

- **`--mkhomedir`**: 
   Automatically creates home directories for users when they log in for the first time.
   
   Example:
   ```bash
   --mkhomedir
   ```

- **`--no-ntp`**: 
   Disable configuration of NTP (Network Time Protocol) for time synchronization. This can be useful if you already have another time sync solution in place.
   
   Example:
   ```bash
   --no-ntp
   ```

- **`--hostname`**: 
   Set the hostname for the client.
   
   Example:
   ```bash
   --hostname=client.example.com
   ```

- **`--no-sudo`**: 
   Prevents the installation from modifying the sudoers file. By default, IPA client installation configures sudo to work with IPA.
   
   Example:
   ```bash
   --no-sudo
   ```

- **`--unattended`**: 
   Run the installation in non-interactive mode. Useful for automation or scripting.
   
   Example:
   ```bash
   --unattended
   ```

- **`--force`**: 
   Forces reinstallation if the client is already enrolled.

   Example:
   ```bash
   --force
   ```

### **Example Commands**

1. **Simple Client Installation**:
   ```bash
   sudo ipa-client-install --domain=example.com --server=ipa.example.com --realm=EXAMPLE.COM
   ```

2. **Non-interactive Client Installation with Home Directory Creation**:
   ```bash
   sudo ipa-client-install --domain=example.com --server=ipa.example.com --realm=EXAMPLE.COM --mkhomedir --unattended
   ```

3. **Installation Without NTP Configuration**:
   ```bash
   sudo ipa-client-install --domain=example.com --server=ipa.example.com --realm=EXAMPLE.COM --no-ntp
   ```

4. **Reinstalling a Client with Force Option**:
   ```bash
   sudo ipa-client-install --force --domain=example.com --server=ipa.example.com --realm=EXAMPLE.COM
   ```

### **Post-Installation**

After installing the FreeIPA client, you should verify that the machine has joined the domain successfully:

1. **Check the Kerberos Ticket**:
   ```bash
   kinit admin
   klist
   ```
   This command should list a valid Kerberos ticket for the user.

2. **Check IPA Services**:
   You can test IPA-related services like LDAP, Kerberos authentication, or sudo access to ensure the client is properly integrated.

### **Uninstalling the FreeIPA Client**

If you need to remove a client from the IPA domain:
```bash
sudo ipa-client-install --uninstall
```

This will remove the FreeIPA client configuration, undo any changes made by the installation, and remove the client from the FreeIPA domain.

---

### **Conclusion**

The `ipa-client-install` tool simplifies the process of integrating Linux machines with FreeIPA for centralized user management and authentication. It allows you to specify domain details, customize sudo settings, automate the installation, and more. By following the installation process and using appropriate options, you can effectively join your machines to the FreeIPA domain and benefit from centralized identity and authentication management.

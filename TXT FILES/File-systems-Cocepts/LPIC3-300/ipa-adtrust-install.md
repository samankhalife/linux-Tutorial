# ipa-adtrust-install

The `ipa-adtrust-install` command is used in FreeIPA to configure the FreeIPA server to work with **Active Directory (AD)** domains by enabling the **Cross-Realm Trust** feature. This tool installs the necessary components and sets up the required configurations so that **FreeIPA can establish a trust relationship with an Active Directory domain**. This allows Active Directory users to authenticate to FreeIPA resources and vice versa.

### Key Features of `ipa-adtrust-install`:

- **Configures Samba Services**: Installs and configures the Samba services required for cross-realm trusts with Active Directory.
- **Enables Trust with Active Directory**: Prepares the FreeIPA server to create trust relationships with AD domains.
- **Sets up ID Ranges**: Helps define ID ranges for users and groups from Active Directory.
- **Creates Services**: Registers necessary Kerberos principals for the trust relationship.
- **Optional DNS Management**: Can manage DNS zones if needed for the trust setup.

### When to Use `ipa-adtrust-install`:

- When you want FreeIPA and Active Directory to establish a trust relationship.
- When you need users from AD domains to authenticate to FreeIPA and access resources managed by FreeIPA.
- When you need to configure user/group mapping between FreeIPA and Active Directory.

### Basic Syntax:

```bash
ipa-adtrust-install [OPTIONS]
```

### Common Options:

- **`--add-sids`**: Generates **Security Identifiers (SIDs)** for users and groups in FreeIPA.
- **`--netbios-name=<name>`**: Specify the **NetBIOS** name of the FreeIPA domain. If not provided, the default NetBIOS name is derived from the FreeIPA realm.
- **`--netbios-domain-name=<name>`**: Specify the **NetBIOS domain** name. Defaults to the first component of the FreeIPA realm name.
- **`--no-msdcs`**: Disables the automatic creation of the `_msdcs` DNS zone, which is used for locating domain controllers in AD.
- **`--no-ntp`**: Skip NTP configuration.
- **`--setup-dns`**: Configures FreeIPA DNS to manage the DNS zones necessary for the AD trust relationship.
- **`--no-ui-redirect`**: Disables the user interface redirection to the Active Directory domain.
- **`--enable-compat`**: Enables the compatibility plugin for legacy clients, allowing older clients to resolve user and group names.
- **`--no-sssd`**: Disables the configuration of the **System Security Services Daemon (SSSD)**, though this is generally required for trust relationships.
- **`--force-ntpd`**: Forces the configuration of **NTP** to ensure time synchronization between FreeIPA and AD.

### Example: Basic Installation with Trust Setup

To install the required components for establishing a trust relationship between FreeIPA and Active Directory, run:

```bash
ipa-adtrust-install
```

This command will prompt you to provide necessary information, such as DNS configuration and the desired ID range for the Active Directory users.

### Example: Installation with a Custom NetBIOS Name

If you need to specify a custom NetBIOS name for the FreeIPA domain, use the `--netbios-name` option:

```bash
ipa-adtrust-install --netbios-name=MYNETBIOS
```

### Example: Installing with DNS Setup

If you want FreeIPA to manage DNS zones for the trust relationship with AD, use:

```bash
ipa-adtrust-install --setup-dns
```

This will configure the necessary DNS zones for trust discovery between FreeIPA and AD.

### Example: Enabling Compatibility Mode

For legacy client compatibility, run the following with the `--enable-compat` option:

```bash
ipa-adtrust-install --enable-compat
```

This enables the plugin that allows legacy clients to query and resolve user and group information from FreeIPA.

### Post-Installation:

After `ipa-adtrust-install` completes, you can create a trust with an Active Directory domain using the `ipa trust-add` command, which enables the actual trust relationship.

For example:

```bash
ipa trust-add --type=ad ad.example.com --admin administrator --password
```

This command establishes a trust relationship between FreeIPA and `ad.example.com`, allowing AD users to authenticate and access FreeIPA resources.

### Troubleshooting:

- **Time synchronization** is critical when establishing trusts between FreeIPA and AD. Ensure that NTP is correctly configured on both sides.
- Ensure that DNS resolution is working correctly, especially if you're setting up trust relationships without the `--setup-dns` option.
- If you encounter issues, check the Samba logs (`/var/log/samba/`) and Kerberos logs (`/var/log/krb5kdc.log`).

### Conclusion:

`ipa-adtrust-install` is essential for enabling trust relationships between FreeIPA and Active Directory. It sets up the necessary components (Samba, DNS, Kerberos) and prepares FreeIPA to handle cross-realm authentication. After installation, you can configure trust relationships to allow seamless authentication between users from both environments.

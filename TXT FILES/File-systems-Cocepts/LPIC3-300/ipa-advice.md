# ipa-advice

The `ipa-advice` command in FreeIPA provides guidance and recommendations on various administrative tasks, configurations, and security settings. It is used to receive actionable instructions or tips that can help improve system security, configuration, or solve specific tasks related to **Kerberos**, **LDAP**, **Certificates**, and more.

The `ipa-advice` tool suggests best practices based on common operational tasks in a FreeIPA environment and can help simplify complicated setup steps or security hardening processes.

### Key Features of `ipa-advice`:

- Provides **pre-configured templates** for specific use cases and best practices.
- Offers **customized advice** based on the current state of the FreeIPA environment.
- Helps administrators apply configurations that align with best practices for security and management.
- Covers areas such as **Kerberos**, **LDAP**, **Trusts**, **DNS**, **Certificate Management**, and more.

### Basic Syntax:

```bash
ipa-advice [OPTIONS] [TOPIC]
```

Where `TOPIC` refers to a specific category of advice that the command can offer.

### Commonly Available Topics:

Some typical topics for which `ipa-advice` can provide advice include:

- **Kerberos configuration**: Helps administrators harden and configure Kerberos-based authentication.
- **Trust configuration**: Offers advice on setting up and managing trusts between FreeIPA and Active Directory.
- **Security**: Provides recommendations on strengthening the security of the FreeIPA environment.
- **ID Range Management**: Guidance on how to handle ID range allocations when dealing with cross-realm trusts or external users.

To get a list of all available topics, you can run:

```bash
ipa-advice
```

This will show all available advice that can be queried for guidance.

### Examples of Usage:

#### 1. Getting advice for establishing a Kerberos cross-realm trust:
This topic offers advice on how to configure **cross-realm Kerberos trust** between FreeIPA and another Kerberos realm.

```bash
ipa-advice realm-crossover
```

This will output instructions on how to set up Kerberos cross-realm trust, including details on configuring the `/etc/krb5.conf` file and ensuring correct DNS records are in place.

#### 2. Getting advice for Kerberos client configuration:
To get advice on configuring **Kerberos clients** to authenticate against the FreeIPA domain, you can run:

```bash
ipa-advice configure-kerberos-client
```

This will give instructions on how to configure the Kerberos client, including editing configuration files and installing the required packages.

#### 3. Obtaining security-related advice:
For improving the security of the FreeIPA server, the following command can provide suggestions:

```bash
ipa-advice harden-security
```

This will include steps to harden the configuration, such as enabling certain password policies, improving encryption settings, or setting up audit logs.

#### 4. Advice for managing ID ranges:
For environments with complex user management, especially when using trusts, you can receive advice on managing **ID ranges**:

```bash
ipa-advice idrange-management
```

This will provide recommendations on how to manage and configure ID ranges for external users.

### Common Options:

- **`--list`**: Lists all available advice topics without running any specific advice.
  
  Example:
  ```bash
  ipa-advice --list
  ```

- **`--check`**: Checks the FreeIPA configuration and suggests possible advice that applies to the current state of the system.
  
  Example:
  ```bash
  ipa-advice --check
  ```

### Example Output:

An example output for Kerberos cross-realm trust advice might look like this:

```bash
# ipa-advice realm-crossover
1. On the FreeIPA server:
    - Edit /etc/krb5.conf to include the new realm.
    - Add DNS SRV records for the other realm.
    - Restart the Kerberos services.

2. On the other realm’s KDC:
    - Ensure the FreeIPA realm is added to their KDC configuration.
    - Exchange trust principals between the realms.
```

### Conclusion:

The `ipa-advice` tool is a convenient way to receive specific guidance and best practices directly from the FreeIPA system. It helps administrators quickly identify the steps required to configure key features, improve security, or apply configurations for optimal performance. Each advice topic is designed to offer clear, actionable steps for implementing configurations or resolving common challenges in a FreeIPA environment.

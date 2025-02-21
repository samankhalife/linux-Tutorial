# krb5.conf

`krb5.conf` is the main configuration file for Kerberos 5 on Unix-like systems. It defines the settings for Kerberos realms, the Key Distribution Centers (KDCs), and various defaults for Kerberos clients and services. Proper configuration of `krb5.conf` is essential for successful Kerberos authentication, including integration with Active Directory environments.

## Overview

- **Purpose**:  
  Provides the Kerberos client and server with the necessary information to locate and communicate with KDCs, define realms, and set default options for ticket lifetimes, encryption types, and more.

- **Location**:  
  Typically found at `/etc/krb5.conf` on most Linux distributions. Some systems may use alternative locations or include additional configuration files.

## Basic Structure

The file is divided into several main sections:

- **[libdefaults]**:  
  Contains default settings used by the Kerberos libraries.
  
- **[realms]**:  
  Specifies configuration for each Kerberos realm, including KDC addresses and administrative servers.
  
- **[domain_realm]**:  
  Maps domain names to Kerberos realms, enabling clients to determine the appropriate realm for a given domain.
  
- **[logging]**:  
  Configures logging options for Kerberos events.

## Key Sections and Options

### [libdefaults]

Defines default parameters for Kerberos operations.

```ini
[libdefaults]
   default_realm = EXAMPLE.COM
   dns_lookup_realm = false
   dns_lookup_kdc = true
   ticket_lifetime = 24h
   renew_lifetime = 7d
   forwardable = true
   rdns = false
```

- **default_realm**:  
  The default realm to use if none is specified (usually in uppercase, e.g., `EXAMPLE.COM`).
  
- **dns_lookup_kdc**:  
  If set to `true`, the client will use DNS to locate the KDC.
  
- **ticket_lifetime** and **renew_lifetime**:  
  Define the duration for which tickets are valid and renewable.

### [realms]

Specifies each Kerberos realm and its associated KDCs and admin servers.

```ini
[realms]
   EXAMPLE.COM = {
      kdc = kdc.example.com
      admin_server = kdc.example.com
      default_domain = example.com
   }
```

- **kdc**:  
  The hostname (or IP address) of the Key Distribution Center.
  
- **admin_server**:  
  The server used for administrative operations (often the same as the KDC).
  
- **default_domain**:  
  Associates a domain with the realm.

### [domain_realm]

Maps DNS domains to Kerberos realms, which helps the Kerberos client determine the realm for a given domain.

```ini
[domain_realm]
   .example.com = EXAMPLE.COM
   example.com = EXAMPLE.COM
```

- The leading dot in `.example.com` applies the mapping to all subdomains as well.

### [logging]

Configures where Kerberos logs are written.

```ini
[logging]
   default = FILE:/var/log/krb5libs.log
   kdc = FILE:/var/log/krb5kdc.log
   admin_server = FILE:/var/log/kadmind.log
```

- Logs can be directed to files, syslog, or other logging systems.

## Example krb5.conf

Below is a complete example of a typical `krb5.conf` file for a Kerberos realm integrated with Active Directory:

```ini
[libdefaults]
   default_realm = EXAMPLE.COM
   dns_lookup_realm = false
   dns_lookup_kdc = true
   ticket_lifetime = 24h
   renew_lifetime = 7d
   forwardable = true
   rdns = false

[realms]
   EXAMPLE.COM = {
      kdc = kdc.example.com
      admin_server = kdc.example.com
      default_domain = example.com
   }

[domain_realm]
   .example.com = EXAMPLE.COM
   example.com = EXAMPLE.COM

[logging]
   default = FILE:/var/log/krb5libs.log
   kdc = FILE:/var/log/krb5kdc.log
   admin_server = FILE:/var/log/kadmind.log
```

## Best Practices

- **Time Synchronization**:  
  Ensure that system clocks are synchronized (using NTP) since Kerberos is highly time-sensitive.
  
- **DNS Configuration**:  
  Proper DNS setup is critical, especially when using `dns_lookup_kdc`. Make sure your DNS entries for KDCs and admin servers are accurate.

- **Secure Permissions**:  
  Restrict access to `krb5.conf` since it may contain sensitive configuration details. Typically, permissions are set to 644 or 600.

- **Testing**:  
  After making changes to `krb5.conf`, use `kinit` to obtain a ticket and `klist` to verify that tickets are correctly issued.

## Conclusion

The `krb5.conf` file is essential for configuring Kerberos authentication on Unix-like systems. By correctly setting realms, default options, and logging preferences, administrators can ensure secure and efficient Kerberos operations, which are critical for systems integrated with Windows Active Directory and other Kerberos-based services.


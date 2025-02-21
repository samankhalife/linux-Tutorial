# sssd.conf

`sssd.conf` is the main configuration file for the System Security Services Daemon (SSSD) on Unix-like systems. SSSD provides centralized access to remote identity and authentication providers (such as LDAP, Active Directory, etc.) and caches this information locally to improve performance and support offline authentication. The file is typically located at `/etc/sssd/sssd.conf` and must be secured with restrictive permissions.

## Overview

- **Purpose**:  
  Configure SSSD to retrieve and cache identity and authentication data from remote sources. This enables features like single sign-on (SSO), offline authentication, and centralized identity management.

- **Location**:  
  `/etc/sssd/sssd.conf`

- **Security**:  
  Since the file may contain sensitive information (including credentials), it should be owned by root and have permissions set to 600.

## Key Sections

### [sssd]

This section contains global settings for SSSD.

**Example:**
```ini
[sssd]
services = nss, pam
config_file_version = 2
domains = EXAMPLE
debug_level = 5
```
- **services**: Specifies the services SSSD provides (e.g., `nss` for Name Service Switch, `pam` for authentication).
- **config_file_version**: The version of the configuration file format (typically `2`).
- **domains**: A comma-separated list of domains SSSD will manage.
- **debug_level**: Sets the verbosity of log output (higher values generate more detailed logs).

### [domain/<domain>]

Each domain section defines how SSSD connects to a remote identity provider. Replace `<domain>` with your actual domain (e.g., `[domain/example.com]`).

**Example:**
```ini
[domain/example.com]
id_provider = ldap
auth_provider = ldap
ldap_uri = ldap://ldap.example.com
ldap_search_base = dc=example,dc=com
cache_credentials = True
enumerate = True
ldap_tls_reqcert = demand
```
- **id_provider**: Specifies the source for identity data (e.g., `ldap`, `ad`).
- **auth_provider**: Specifies the source for authentication.
- **ldap_uri**: The URI of the LDAP server.
- **ldap_search_base**: The base DN for searching user and group entries.
- **cache_credentials**: Enables caching for offline authentication.
- **enumerate**: Determines whether SSSD should list all users and groups from the domain.
- **ldap_tls_reqcert**: Controls the TLS certificate requirement when connecting to the LDAP server.

### [nss]

(Optional) This section allows you to set options related to the Name Service Switch (NSS).

**Example:**
```ini
[nss]
filter_users = root,ldap,nobody
filter_groups = root
```
- **filter_users / filter_groups**: Prevents certain local accounts from being enumerated by SSSD, reducing load and improving security.

### [pam]

(Optional) This section configures PAM-related settings.

**Example:**
```ini
[pam]
offline_credentials_expiration = 2
```
- **offline_credentials_expiration**: Specifies, in days, how long cached credentials remain valid when the system is offline.

## Best Practices

- **Secure the Configuration**:  
  Set file permissions to 600 (e.g., `chmod 600 /etc/sssd/sssd.conf`) and ensure the file is owned by root.

- **Minimize Unnecessary Enumeration**:  
  Use the `[nss]` filters to exclude system accounts or other unnecessary entries from SSSD’s cache.

- **Test Changes Carefully**:  
  After modifying `sssd.conf`, restart SSSD (`systemctl restart sssd`) and review logs in `/var/log/sssd/` to verify that changes are correctly applied.

- **Regular Updates**:  
  Keep SSSD and its configuration updated to benefit from security and performance improvements.

## Conclusion

`sssd.conf` is a critical file for configuring SSSD, enabling efficient and secure centralized identity and authentication management. Proper configuration of this file is essential for integrating Unix-like systems with remote identity sources such as LDAP or Active Directory, and for ensuring robust offline authentication capabilities. By following best practices in security, testing, and maintenance, administrators can ensure a stable and secure SSSD environment.


# sss_cache

`sss_cache` is a command-line utility provided by SSSD (System Security Services Daemon) that is used to expire (i.e., clear) cached identity and authentication information. This is especially useful when changes have been made in remote identity sources (such as LDAP or Active Directory), and you need the local system to refresh its cache to reflect those changes.

## Purpose

- **Refresh Cached Data**:  
  Clears out stale or outdated user, group, or domain information that SSSD stores locally.
  
- **Troubleshooting**:  
  Helps resolve issues where incorrect or old credentials are causing authentication problems.
  
- **Offline Mode**:  
  Ensures that the local system uses current data, particularly after changes like password updates or group membership modifications.

## Basic Syntax

```bash
sss_cache [OPTIONS]
```

## Common Options

- **`-E`, `--expire`**:  
  Expires all cached data for all configured domains.
  ```bash
  sss_cache -E
  ```

- **`-u <username>`**:  
  Expires the cache entries for a specific user.
  ```bash
  sss_cache -u alice
  ```

- **`-g <groupname>`**:  
  Expires the cache entries for a specific group.
  ```bash
  sss_cache -g developers
  ```

- **`-d <domain>`**:  
  Expires the cache entries for a specific domain.
  ```bash
  sss_cache -d example.com
  ```

- **`--help`**:  
  Displays help information and available options.
  ```bash
  sss_cache --help
  ```

## Example Usage

1. **Expire All Cached Data**:  
   To clear all SSSD caches:
   ```bash
   sss_cache -E
   ```
   This forces SSSD to re-query remote identity sources for fresh data.

2. **Expire Cache for a Specific User**:  
   If a user’s information has changed, you can clear their cache:
   ```bash
   sss_cache -u alice
   ```

3. **Expire Cache for a Specific Group**:  
   To refresh the cache for a group:
   ```bash
   sss_cache -g developers
   ```

4. **Expire Cache for a Specific Domain**:  
   For systems with multiple domains, you can target one domain:
   ```bash
   sss_cache -d example.com
   ```

## Best Practices

- **Regular Cache Management**:  
  Incorporate cache expiration into routine maintenance to ensure authentication data stays current.

- **Troubleshooting**:  
  When encountering authentication or lookup issues, run `sss_cache -E` to force a cache refresh before investigating further.

- **Monitoring**:  
  Check SSSD log files (usually in `/var/log/sssd/`) after clearing the cache to confirm that new data is being fetched correctly.

## Conclusion

`sss_cache` is a vital utility for ensuring that SSSD’s locally cached identity and authentication data is up-to-date. By clearing stale cache entries, it helps maintain consistency between local and remote identity sources, ensuring smooth and accurate authentication in environments that rely on centralized directories.


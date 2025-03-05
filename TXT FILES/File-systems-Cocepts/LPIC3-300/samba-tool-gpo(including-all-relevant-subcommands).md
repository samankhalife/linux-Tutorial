# samba-tool gpo

The `samba-tool gpo` command is part of the Samba suite and is used for managing Group Policy Objects (GPOs) in a Samba Active Directory Domain Controller environment. With this tool, administrators can create, list, display details, delete, backup, and restore GPOs, enabling centralized management of policies for domain-joined clients.

Below is an overview of the key subcommands and options available with `samba-tool gpo`:

## Key Subcommands

### 1. **create**
Creates a new Group Policy Object.

- **Usage:**
  ```bash
  samba-tool gpo create <GPO_name>
  ```
- **Example:**
  ```bash
  samba-tool gpo create "Default Domain Policy"
  ```

### 2. **list**
Lists all GPOs in the domain.

- **Usage:**
  ```bash
  samba-tool gpo list
  ```
- **Example:**
  ```bash
  samba-tool gpo list
  ```
  *Output may display a list similar to:*
  ```
  GPO Name                           GUID
  -------------------------------------------------------------
  Default Domain Policy              {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}
  Custom Policy                      {yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy}
  ```

### 3. **show**
Displays detailed information about a specific GPO.

- **Usage:**
  ```bash
  samba-tool gpo show <GPO_name>
  ```
- **Example:**
  ```bash
  samba-tool gpo show "Default Domain Policy"
  ```

### 4. **delete**
Deletes an existing GPO from the domain.

- **Usage:**
  ```bash
  samba-tool gpo delete <GPO_name>
  ```
- **Example:**
  ```bash
  samba-tool gpo delete "Custom Policy"
  ```


### 5. **backup**
Creates a backup of one or more GPOs, storing them in a specified directory.

- **Usage:**
  ```bash
  samba-tool gpo backup --target=<backup_directory>
  ```
- **Example:**
  ```bash
  samba-tool gpo backup --target=/var/backups/gpo
  ```

### 6. **restore**
Restores GPOs from a backup.

- **Usage:**
  ```bash
  samba-tool gpo restore --target=<backup_directory> [--gpo=<GPO_name>]
  ```
- **Example:**
  ```bash
  samba-tool gpo restore --target=/var/backups/gpo --gpo="Default Domain Policy"
  ```

### 7. **edit** *(if available)*
Opens an editor to modify the attributes or settings of a GPO directly.  
*Note: This subcommand might not be available or may have limited functionality depending on your Samba version.*

- **Usage:**
  ```bash
  samba-tool gpo edit <GPO_name>
  ```
- **Example:**
  ```bash
  samba-tool gpo edit "Default Domain Policy"
  ```

## Additional Options

Depending on your Samba version and configuration, you might have extra options available for fine-tuning backup locations, specifying verbosity, or filtering output. Consult the built-in help:

```bash
samba-tool gpo --help
```

## Conclusion

The `samba-tool gpo` utility provides a command-line method to manage Group Policy Objects in a Samba AD environment. By using its subcommands—**create**, **list**, **show**, **delete**, **backup**, **restore**, and possibly **edit**—administrators can efficiently control and maintain GPOs, ensuring consistent policy enforcement across domain-joined systems.

This suite of tools is essential for environments that rely on centralized group policy management, helping streamline configuration and disaster recovery through backup and restoration functionalities.

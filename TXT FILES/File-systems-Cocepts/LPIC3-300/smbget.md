# smbget

`smbget` is a command-line utility that is part of the Samba suite. It is used for non-interactively downloading files from SMB/CIFS shares, functioning similarly to the well-known `wget` command but specifically designed for the SMB protocol.

## Purpose

- **File Retrieval**:  
  Download files from SMB shares hosted on Windows or Samba servers.
  
- **Automated Downloads**:  
  Useful for scripting and automation tasks, such as regularly retrieving files from a remote share.

- **Recursive Downloading**:  
  Supports recursive downloads, allowing you to download entire directories from an SMB share.

## Basic Syntax

```bash
smbget [options] URL...
```

- **`URL`**:  
  Specifies the SMB URL of the file or directory to download. SMB URLs typically follow the format:
  ```
  smb://server/share/path/to/file
  ```

## Common Options

- **`-u, --user=USER`**:  
  Specify the username for authentication.
  ```bash
  smbget -u username smb://server/share/file.txt
  ```

- **`-p, --password=PASS`**:  
  Specify the password for authentication. If omitted, `smbget` will prompt for it.
  ```bash
  smbget -u username -p secret smb://server/share/file.txt
  ```

- **`-R, --recursive`**:  
  Enable recursive downloading of directories.
  ```bash
  smbget -R smb://server/share/directory/
  ```

- **`-c, --continue`**:  
  Continue/resume a previously interrupted download.
  ```bash
  smbget -c smb://server/share/largefile.iso
  ```

- **`-d, --debug`**:  
  Increase the debug level to get more verbose output, useful for troubleshooting.
  ```bash
  smbget -d 3 smb://server/share/file.txt
  ```

- **`-h, --help`**:  
  Display help and usage information.
  ```bash
  smbget --help
  ```


## Examples

1. **Download a Single File**

   Download a file from an SMB share:
   ```bash
   smbget smb://fileserver/shared/document.pdf
   ```

2. **Download with Authentication**

   Specify a username (and optionally a password):
   ```bash
   smbget -u alice smb://fileserver/shared/report.docx
   ```
   *You will be prompted for the password if it is not provided via `-p`.*

3. **Recursive Download**

   Download an entire directory recursively from an SMB share:
   ```bash
   smbget -R smb://fileserver/shared/photos/
   ```

4. **Resume a Download**

   Continue downloading a file that was previously interrupted:
   ```bash
   smbget -c smb://fileserver/shared/largefile.zip
   ```

## Conclusion

`smbget` is a valuable tool for retrieving files from SMB shares in a non-interactive manner. Its support for authentication, recursive downloads, and download resumption makes it ideal for both manual file retrieval and automated backup or synchronization scripts in environments that utilize SMB/CIFS file sharing.

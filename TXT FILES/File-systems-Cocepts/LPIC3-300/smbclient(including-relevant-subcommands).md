# smbclient

`smbclient` is a versatile command-line tool provided by Samba that allows you to interact with SMB/CIFS shares on remote servers. It works similarly to an FTP client, enabling you to list shares, transfer files, and execute remote commands against Windows or Samba servers. This utility is useful for both ad-hoc file transfers and scripting automated interactions with network shares.

## Basic Syntax

```
smbclient [OPTIONS] //<server>/<share> [password]
```

- **`<server>`**: The hostname or IP address of the server hosting the share.
- **`<share>`**: The name of the share to connect to.
- **`[OPTIONS]`**: Various command-line options that modify the behavior of the connection.
- **`[password]`**: Optionally, you can supply the password on the command line (not recommended for security reasons).

## Common Global Options

- **`-U username`**:  
  Specifies the username for authentication.
  ```
  smbclient //server/share -U username
  ```

- **`-W workgroup`**:  
  Specifies the workgroup or domain.
  ```
  smbclient //server/share -U username -W WORKGROUP
  ```

- **`-I ip_address`**:  
  Specifies the IP address of the server.
  ```
  smbclient //server/share -U username -I 192.168.1.100
  ```

- **`-m SMB_version`**:  
  Specifies the SMB protocol version (e.g., SMB2, SMB3).
  ```
  smbclient //server/share -U username -m SMB3
  ```

- **`-d debug_level`**:  
  Sets the debug level to provide more verbose output for troubleshooting.
  ```
  smbclient //server/share -U username -d 3
  ```

- **`-c "command"`**:  
  Runs a single command non-interactively and then exits.
  ```
  smbclient //server/share -U username -c "ls"
  ```

- **`--help`**:  
  Displays usage information.

## Interactive Shell Subcommands

Once connected to a share, `smbclient` provides an interactive shell similar to FTP. Common commands include:

### File and Directory Operations

- **`ls`**  
  Lists files and directories in the current directory.
  ```
  smb: \> ls
  ```

- **`cd <directory>`**  
  Changes the current directory on the remote share.
  ```
  smb: \> cd documents
  ```

- **`mkdir <directory>`**  
  Creates a new directory on the remote share.
  ```
  smb: \> mkdir newfolder
  ```

- **`rmdir <directory>`**  
  Removes a directory on the remote share.
  ```
  smb: \> rmdir oldfolder
  ```

- **`del <filename>`**  
  Deletes a file on the remote share.
  ```
  smb: \> del report.doc
  ```

- **`get <remote_file> [local_file]`**  
  Downloads a file from the remote share. If `local_file` is omitted, the file is saved with the same name.
  ```
  smb: \> get data.csv
  ```

- **`put <local_file> [remote_file]`**  
  Uploads a file to the remote share. If `remote_file` is omitted, the file is saved with the same name.
  ```
  smb: \> put localfile.txt remotefile.txt
  ```

### Share and Disk Information

- **`df`**  
  Displays free disk space on the remote share.
  ```
  smb: \> df
  ```

- **`du [directory]`**  
  Shows disk usage for the specified directory or the current directory if omitted.
  ```
  smb: \> du reports/
  ```

### Miscellaneous Commands

- **`help`**  
  Displays a list of available commands within the interactive shell.
  ```
  smb: \> help
  ```

- **`exit` or `quit`**  
  Exits the interactive session.
  ```
  smb: \> exit
  ```

## Example Usage

### Listing Available Shares on a Server
To list all shares available on a server:
```bash
smbclient -L //server -U username
```
This command will display a list of shares, such as `IPC$`, `print$`, and user-defined shares.

### Connecting to a Share and Running Commands
To connect to a share and interact with it interactively:
```bash
smbclient //server/share -U username
```
Once connected, you can use commands like:
```plaintext
smb: \> ls
smb: \> cd documents
smb: \> get file.txt
smb: \> put localfile.txt
```

### Non-Interactive Command Execution
To execute a command non-interactively, use the `-c` option:
```bash
smbclient //server/share -U username -c "ls; cd documents; get report.pdf"
```

## Conclusion

`smbclient` is a powerful tool for accessing and managing SMB/CIFS shares from the command line. Its combination of global options and interactive shell commands makes it suitable for both ad-hoc file transfers and scripting automated tasks. By using options like `-L`, `-U`, and `-c`, and interactive commands like `ls`, `get`, and `put`, administrators and users can effectively manage files on remote SMB servers.


# rdesktop

`rdesktop` is an open-source command-line client for Microsoft's Remote Desktop Protocol (RDP). It allows Linux and Unix users to connect to and control Windows-based computers over a network, making it useful for remote administration, technical support, and accessing Windows applications or desktops from a non-Windows environment.

## Purpose

- **Remote Desktop Access**:  
  Connect to Windows terminal servers or desktops remotely.
- **Cross-Platform Compatibility**:  
  Enables Linux and Unix users to interact with Windows environments using RDP.
- **Command-Line Flexibility**:  
  Offers a range of options for tailoring connection settings such as screen resolution, color depth, authentication, and more.

## Basic Syntax

```bash
rdesktop [options] server[:port]
```

- **`server`**: The hostname or IP address of the Windows machine to connect to.
- **`port`**: (Optional) The port number for the RDP service (default is 3389).

## Common Options

- **`-u <username>`**:  
  Specify the username for login.
  ```bash
  rdesktop -u john_doe server.example.com
  ```

- **`-p <password>`**:  
  Specify the password for login (use with caution as it may be visible in process listings).
  ```bash
  rdesktop -u john_doe -p secret server.example.com
  ```

- **`-g <geometry>`**:  
  Set the screen resolution. Acceptable formats include `<width>x<height>`, e.g., `1024x768`.
  ```bash
  rdesktop -g 1280x1024 server.example.com
  ```

- **`-a <depth>`**:  
  Specify the color depth (in bits). Common values are `8`, `16`, or `32`.
  ```bash
  rdesktop -a 16 server.example.com
  ```

- **`-f`**:  
  Launch in full-screen mode.
  ```bash
  rdesktop -f server.example.com
  ```

- **`-k <layout>`**:  
  Set the keyboard layout (e.g., `en-us`, `fr`, etc.).
  ```bash
  rdesktop -k en-us server.example.com
  ```

- **`-d <domain>`**:  
  Specify the domain for authentication (useful in corporate environments).
  ```bash
  rdesktop -d MYDOMAIN -u john_doe server.example.com
  ```

- **`-r sound:local`**:  
  Redirect sound from the remote machine to the local machine.
  ```bash
  rdesktop -r sound:local server.example.com
  ```

- **`-r clipboard:PRIMARYCLIPBOARD`**:  
  Enable clipboard sharing between the local and remote systems.
  ```bash
  rdesktop -r clipboard:PRIMARYCLIPBOARD server.example.com
  ```

## Examples

1. **Basic Connection**:
   ```bash
   rdesktop server.example.com
   ```
   Connects to the Windows machine at `server.example.com` using default settings.

2. **Specify User and Domain**:
   ```bash
   rdesktop -u john_doe -d MYDOMAIN server.example.com
   ```
   Connects with the username `john_doe` in the domain `MYDOMAIN`.

3. **Full-Screen with Custom Resolution**:
   ```bash
   rdesktop -f -g 1920x1080 server.example.com
   ```
   Launches the connection in full-screen mode with a resolution of 1920x1080 pixels.

4. **Connection with Specified Color Depth and Clipboard Redirection**:
   ```bash
   rdesktop -a 16 -r clipboard:PRIMARYCLIPBOARD server.example.com
   ```
   Connects using 16-bit color depth and enables clipboard sharing.

## Conclusion

`rdesktop` is a powerful tool for Linux and Unix users who need to access Windows systems remotely using RDP. Its extensive range of options allows users to customize connections for various requirements, such as screen resolution, authentication, and peripheral redirection. Whether for administrative tasks or everyday remote desktop use, `rdesktop` offers a flexible solution for cross-platform connectivity.

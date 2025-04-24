The `capsh` command in Linux is used to examine and modify the capabilities of processes. Capabilities are a set of privileges that can be granted to processes or executables, allowing fine-grained control over the actions a process can perform. This tool is often used for managing process capabilities in conjunction with security frameworks like SELinux or AppArmor.

### What Are Capabilities?

Linux capabilities divide the root user's privileges into distinct units. This allows for more granular control over what actions a process can perform without giving it full root access. For example, a process might have the capability to bind to low-numbered ports but not the capability to change system time.

Common capabilities include:

- **CAP_NET_ADMIN**: Network administration (e.g., changing network interfaces).
- **CAP_SYS_ADMIN**: System administration (e.g., mounting filesystems, configuring kernel parameters).
- **CAP_DAC_OVERRIDE**: Bypass file read, write, and execute permission checks.
- **CAP_KILL**: Send signals to processes.

### Usage of `capsh`

The `capsh` command is used to interact with process capabilities in the following ways:

1. **Display the current capabilities of the calling process**.
2. **Execute a command with a modified set of capabilities**.
3. **Display the full list of capabilities available on the system**.

### Basic Syntax

```bash
capsh [options] [command]
```

### Options and Examples

#### 1. **Display the Current Capabilities of the Calling Process**

To see the capabilities of the current process:

```bash
capsh --print
```

This will output something like:

```bash
Current: =cap_sys_admin,cap_dac_override+ep
Bounding set: =cap_sys_admin,cap_dac_override
```

This shows the effective capabilities and the bounding set of the process. The bounding set limits what capabilities can be granted to the process.

#### 2. **Run a Command with Specific Capabilities**

You can use `capsh` to run a command with a specific set of capabilities. For example, to run a command with the `CAP_NET_ADMIN` capability (which allows network administration), use:

```bash
capsh --caps="cap_net_admin+ep" -- /path/to/command
```

This command will execute `/path/to/command` with the `CAP_NET_ADMIN` capability.

#### 3. **Add or Remove Capabilities for the Current Process**

You can modify the current process's capabilities by adding or removing them. For example, to add `CAP_NET_ADMIN`:

```bash
capsh --caps="cap_net_admin+ep" --print
```

To remove a capability, such as `CAP_SYS_ADMIN`:

```bash
capsh --caps="cap_sys_admin-ep" --print
```

#### 4. **Show All Available Capabilities**

You can list all available capabilities on the system:

```bash
capsh --list
```

This will display all the available capabilities that can be assigned to processes.

### Common Use Cases

1. **Running Containers with Reduced Privileges**: When running containers, you often want to restrict the set of capabilities available to the container's processes. Using `capsh`, you can ensure the container process only has the specific capabilities it needs.

2. **Security Testing**: When testing the security of a process or application, `capsh` can help you simulate different privilege levels by adding or removing capabilities, ensuring that only the required privileges are granted.

3. **Kernel and System Administration**: Administrators can use `capsh` to modify the capabilities of system processes without giving them full root privileges.

### Conclusion

`capsh` is a powerful utility for managing Linux capabilities, allowing you to modify the privileges of processes in a fine-grained manner. It is a useful tool for security-conscious system administrators, container developers, and anyone managing Linux processes that require specific, limited privileges.

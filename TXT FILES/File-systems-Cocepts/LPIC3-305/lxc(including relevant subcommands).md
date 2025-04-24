# LXC (Linux Containers)

LXC (Linux Containers) is a lightweight virtualization technology that allows running multiple isolated Linux systems (containers) on a single host. LXC is a userspace interface for the Linux kernel’s cgroups and namespaces, providing an operating system-level virtualization solution.

Unlike traditional virtualization, which involves running separate virtual machines, LXC containers share the host’s kernel but provide isolated environments for running applications, making them faster and more efficient.

### Basic Structure of LXC

LXC provides a set of tools to create, manage, and operate containers. It allows you to:

- Create containers from prebuilt images
- Manage their lifecycle (start, stop, restart, delete)
- Configure networking, file systems, and resource limits
- Provide isolation for processes and file systems

### Main LXC Commands and Subcommands

Here are the key LXC commands and their associated subcommands:

## 1. **lxc-create**
This command is used to create a new container from a specified template.

### Syntax
```bash
lxc-create -n <container_name> -t <template>
```

- **-n <container_name>**: Specifies the name of the container.
- **-t <template>**: Specifies the template used to create the container (e.g., `ubuntu`, `debian`, etc.).

### Example:
```bash
lxc-create -n mycontainer -t ubuntu
```
This will create a new container named `mycontainer` using the `ubuntu` template.

## 2. **lxc-start**
This command starts the container in the background.

### Syntax
```bash
lxc-start -n <container_name> -d
```

- **-n <container_name>**: Specifies the name of the container to start.
- **-d**: Runs the container in the background.

### Example:
```bash
lxc-start -n mycontainer -d
```
This starts the container `mycontainer` in the background.

## 3. **lxc-stop**
This command stops a running container.

### Syntax
```bash
lxc-stop -n <container_name>
```

- **-n <container_name>**: Specifies the container to stop.

### Example:
```bash
lxc-stop -n mycontainer
```
This will stop the `mycontainer` container.

## 4. **lxc-restart**
This command restarts a running container.

### Syntax
```bash
lxc-restart -n <container_name>
```

- **-n <container_name>**: Specifies the container to restart.

### Example:
```bash
lxc-restart -n mycontainer
```
This will restart the `mycontainer` container.

## 5. **lxc-info**
This command displays information about a running container, such as its state and resource usage.

### Syntax
```bash
lxc-info -n <container_name>
```

- **-n <container_name>**: Specifies the container whose information you want to view.

### Example:
```bash
lxc-info -n mycontainer
```
This will show detailed information about the `mycontainer` container.

## 6. **lxc-attach**
This command attaches to a running container and allows you to interact with its shell.

### Syntax
```bash
lxc-attach -n <container_name>
```

- **-n <container_name>**: Specifies the container to attach to.

### Example:
```bash
lxc-attach -n mycontainer
```
This will attach to the `mycontainer` container and open a shell inside it.

## 7. **lxc-ls**
This command lists all containers, whether running or stopped.

### Syntax
```bash
lxc-ls --fancy
```

- **--fancy**: Displays a more detailed and formatted output.

### Example:
```bash
lxc-ls --fancy
```
This will list all containers with additional information such as their status (running or stopped).

## 8. **lxc-clone**
This command clones an existing container to create a new one with the same configuration.

### Syntax
```bash
lxc-clone -o <source_container> -n <new_container>
```

- **-o <source_container>**: Specifies the container to clone.
- **-n <new_container>**: Specifies the name of the new cloned container.

### Example:
```bash
lxc-clone -o mycontainer -n mycontainer_clone
```
This will clone the `mycontainer` container to a new container named `mycontainer_clone`.

## 9. **lxc-destroy**
This command deletes a container, along with its filesystem and configuration.

### Syntax
```bash
lxc-destroy -n <container_name>
```

- **-n <container_name>**: Specifies the container to destroy.

### Example:
```bash
lxc-destroy -n mycontainer
```
This will destroy the `mycontainer` container.

## 10. **lxc-freeze**
This command freezes a running container, effectively suspending its processes.

### Syntax
```bash
lxc-freeze -n <container_name>
```

- **-n <container_name>**: Specifies the container to freeze.

### Example:
```bash
lxc-freeze -n mycontainer
```
This will freeze the `mycontainer` container.

## 11. **lxc-unfreeze**
This command unfreezes a previously frozen container.

### Syntax
```bash
lxc-unfreeze -n <container_name>
```

- **-n <container_name>**: Specifies the container to unfreeze.

### Example:
```bash
lxc-unfreeze -n mycontainer
```
This will unfreeze the `mycontainer` container.

## 12. **lxc-snapshot**
This command takes a snapshot of a container, allowing you to roll back to a previous state.

### Syntax
```bash
lxc-snapshot -n <container_name>
```

- **-n <container_name>**: Specifies the container to snapshot.

### Example:
```bash
lxc-snapshot -n mycontainer
```
This will create a snapshot of the `mycontainer` container.

## 13. **lxc-cgroup**
This command manages cgroups (control groups) for a container, allowing you to set limits on CPU, memory, and other resources.

### Syntax
```bash
lxc-cgroup -n <container_name> <cgroup_option>
```

- **-n <container_name>**: Specifies the container to manage.
- **<cgroup_option>**: Specifies the cgroup option to apply (e.g., setting CPU limits, memory limits).

### Example:
```bash
lxc-cgroup -n mycontainer memory.limit_in_bytes 512M
```
This command sets a memory limit of 512MB for the `mycontainer` container.

## LXC Networking

LXC allows containers to use different types of network configurations. Below are common commands related to networking:

- **lxc-net**: Manages networking for LXC containers, such as setting up bridges or network interfaces.
- **lxc-attach -n <container_name> --netns <namespace>**: Attaches a container to a specific network namespace.

### Example of setting up networking for LXC container:

```bash
lxc-net addbr lxcbr0
```

This command creates a virtual bridge (`lxcbr0`) that containers can use for network communication.

## Conclusion

LXC provides powerful container management tools for creating and managing lightweight Linux containers. It is a great option for developers and system administrators who want to run isolated Linux systems without the overhead of traditional virtual machines. By understanding and using the commands mentioned above, you can efficiently manage containers, their resources, and network configurations.

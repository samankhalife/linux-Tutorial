# authkeys
In Ceph, **authkeys** refer to the authentication keys used to control access to the Ceph cluster. Ceph implements an authentication system known as **Cephx**, which ensures that clients and services have the correct privileges before accessing resources. These keys are crucial for secure communication between Ceph clients, monitors (MONs), and object storage daemons (OSDs). Each service and client in Ceph is assigned an authentication key that is used for secure access control.

Ceph stores authentication keys in its configuration and keyring files, and these keys can be managed using tools such as `ceph-authtool`, `ceph` CLI commands, or manually through the configuration files.

## Key Concepts of Authentication in Ceph

- **Cephx**: Ceph’s built-in authentication system that uses shared secret keys (authkeys) for authentication and authorization.
- **Keyring**: A file that stores the authentication keys (authkeys) for Ceph services and clients. Each keyring file can contain multiple keys, with each key associated with an entity (such as an OSD, MON, or client).



## Common Commands for Managing Authkeys in Ceph

### 1. **Generating an Auth Key**

Use the `ceph-authtool` command to generate a new authentication key.

```bash
ceph-authtool --gen-print-key
```

This generates a new Cephx authentication key and prints it to the terminal.

### 2. **Adding Auth Key to a Keyring**

Add a newly generated authentication key to a keyring file.

```bash
ceph-authtool <keyring-file> --create-keyring --name=<entity-name> --add-key=<auth-key>
```

- Example:
  ```bash
  ceph-authtool /etc/ceph/ceph.client.admin.keyring --create-keyring --name=client.admin --add-key=<auth-key>
  ```

This command creates a new keyring file and adds the provided authentication key for the `client.admin` entity.

### 3. **List Auth Keys in a Keyring**

You can list all authentication keys in a specific keyring using:

```bash
ceph-authtool <keyring-file> --print-key
```

- Example:
  ```bash
  ceph-authtool /etc/ceph/ceph.client.admin.keyring --print-key
  ```

This command lists the authentication key(s) in the specified keyring file.

### 4. **Creating a Client or Service Auth Key in Ceph**

You can create a new authentication key for a client or service (OSD, MON, MDS, etc.) using the `ceph` CLI.

```bash
ceph auth get-or-create <entity-name> <capabilities> -o <keyring-file>
```

- Example:
  ```bash
  ceph auth get-or-create client.user mon 'allow r' osd 'allow rwx' -o /etc/ceph/ceph.client.user.keyring
  ```

This command creates a new keyring file (`ceph.client.user.keyring`) for `client.user` and grants it read permission on the MON and read-write-execute permissions on the OSD.

### 5. **Retrieving an Existing Auth Key**

To retrieve the authentication key for a specific client or service:

```bash
ceph auth get <entity-name>
```

- Example:
  ```bash
  ceph auth get client.admin
  ```

This retrieves the authentication key for `client.admin`.

### 6. **Deleting an Auth Key**

To remove an existing authentication key for a particular entity:

```bash
ceph auth del <entity-name>
```

- Example:
  ```bash
  ceph auth del client.user
  ```

This deletes the authentication key for `client.user`.

### 7. **Modifying Capabilities of an Existing Auth Key**

You can modify the access capabilities (permissions) for a client or service.

```bash
ceph auth caps <entity-name> <capabilities>
```

- Example:
  ```bash
  ceph auth caps client.user mon 'allow r' osd 'allow rw'
  ```

This command updates the capabilities for `client.user`, allowing read access to the MON and read-write access to the OSD.



## Capabilities Overview

When setting or modifying capabilities, Ceph administrators define what actions an entity (e.g., client, OSD, MON) can perform. The following are some common capabilities:

- **MON (Monitor)**: Manages cluster state and metadata.
  - `allow r` – Grants read access to monitor data.
  - `allow rw` – Grants read and write access to monitor data.
  
- **OSD (Object Storage Daemon)**: Handles storage and replication.
  - `allow rwx` – Grants read, write, and execute access to OSD data.
  - `allow rw` – Grants read and write access to OSD data.
  
- **MDS (Metadata Server)**: Manages metadata for CephFS.
  - `allow r` – Grants read access to metadata.
  - `allow rw` – Grants read and write access to metadata.

- **RGW (RADOS Gateway)**: Manages object storage for Ceph’s S3 and Swift APIs.
  - `allow r` – Grants read access to RGW.
  - `allow rw` – Grants read and write access to RGW.



## Example: Setting Up a Key for a New Client

1. **Generate a key for the client:**

   ```bash
   ceph auth get-or-create client.myuser mon 'allow r' osd 'allow rwx' -o /etc/ceph/ceph.client.myuser.keyring
   ```

   This generates a keyring for `client.myuser` with read access to the monitor and read-write-execute access to the OSD.

2. **List all the clients and services with auth keys:**

   ```bash
   ceph auth list
   ```

   This will list all entities (clients, OSDs, MONs, MDS, etc.) that have authentication keys.



## Keyring File Example

Here’s what a typical `keyring` file looks like:

```plaintext
[client.admin]
    key = AQCfH9tUjJuNCBAAHFylj4lcQpHQKdMuT7trbQ==
    caps mon = "allow *"
    caps osd = "allow *"
```

In this example, the `client.admin` keyring grants full access (`allow *`) to both the monitor and OSD services.



## Conclusion

Ceph's `authkeys` are essential for ensuring secure communication and access control within the cluster. By leveraging `ceph-authtool`, the `ceph` CLI, and keyring management, administrators can create, modify, and manage authentication keys for clients and services, as well as control their capabilities across the Ceph cluster.

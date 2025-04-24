# cloud-init

**cloud-init** is the de facto standard for early initialization of cloud instances across major cloud providers including AWS, Azure, GCP, OpenStack, and others. It automates tasks like instance configuration, user setup, package installation, and running custom scripts during the first boot.

---

## What cloud-init Does

cloud-init automates cloud VM provisioning by reading metadata and user-provided configuration, typically via `user-data`. Its key functions include:

- Setting the hostname
- Creating users and setting SSH keys
- Installing packages
- Configuring the network
- Mounting volumes
- Running arbitrary scripts or configuration management tools

---

## Initialization Lifecycle

cloud-init executes in multiple stages:

1. **local** – Reads instance metadata and configures low-level settings
2. **network** – Waits for and verifies networking
3. **config** – Applies configuration modules (user-data, package installs)
4. **final** – Runs final scripts, reports status, and completes setup

Check status with:

```bash
cloud-init status --long
```

---

## Key Directories and Files

| Path                            | Description                                     |
|---------------------------------|-------------------------------------------------|
| `/var/lib/cloud/`              | State and instance cache directory              |
| `/etc/cloud/cloud.cfg`         | Main configuration file                         |
| `/etc/cloud/cloud.cfg.d/`      | Drop-in configuration fragments                 |
| `/var/log/cloud-init.log`      | Main log file for debugging                     |
| `/var/lib/cloud/instances/`    | Per-instance runtime data                       |

---

## Supported `user-data` Formats

cloud-init can process various data formats:

- **Shell script** (must begin with `#!/bin/bash` or similar)
- **Cloud-config YAML** (`#cloud-config`)
- **Multi-part MIME** (combines scripts, cloud-config, etc.)
- **Include or Bootstrap** formats (e.g., pointing to Ansible playbooks or remote URLs)

---

## Example cloud-config

```yaml
#cloud-config
hostname: example-vm
users:
  - name: devops
    groups: sudo
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    shell: /bin/bash
    ssh-authorized-keys:
      - ssh-rsa AAAAB3...

packages:
  - nginx
  - htop

runcmd:
  - systemctl start nginx
  - echo "Provisioning complete" > /home/devops/complete.txt
```

---

## Useful Commands

| Command                              | Description                                  |
|-------------------------------------|----------------------------------------------|
| `cloud-init status`                 | Check current status                         |
| `cloud-init analyze`                | Analyze boot stages                          |
| `cloud-init clean`                  | Reset state and re-trigger on reboot         |
| `cloud-init single --file`          | Run a specific cloud-init module             |
| `cloud-init devel schema`           | Validate cloud-config YAML                   |

---

## Re-running cloud-init

To reinitialize cloud-init (e.g., after snapshotting or testing):

```bash
sudo cloud-init clean --logs
```

This clears all instance state from `/var/lib/cloud`.

---

## Security Consideration

Avoid embedding passwords or sensitive credentials directly in `user-data`. Use encrypted secrets, external vaults, or secure boot-time provisioning mechanisms when possible.

---

## Supported Environments

cloud-init is supported on:

- AWS EC2
- Microsoft Azure
- Google Cloud Platform
- OpenStack
- Oracle Cloud
- DigitalOcean
- VMware (with customization)
- LXC/LXD containers
- Bare metal (via NoCloud or ISO seed images)

---

## Adoption and Activity

**GitHub (https://github.com/canonical/cloud-init)**:
- Stars: ~2.6k
- Open issues: ~160
- Closed issues: 2.7k+
- Primary Maintainer: Canonical (Ubuntu developers)

**StackOverflow**:
- Approx. 1,500 questions under the `cloud-init` tag
- Frequent topics: SSH key provisioning, cloud-config formatting, EC2 user-data, OpenStack instance customization

---

Let me know if you'd like to compare this with **Ignition**, **kickstart**, or **Ansible cloud-init integration**, or need help crafting complex multi-part MIME templates.

# /var/lib/cloud

The `/var/lib/cloud` directory is a key location used by **cloud-init**, the standard tool for early initialization of cloud instances. This directory stores persistent state, metadata, instance configuration, and logs related to how an instance was provisioned by cloud-init.

---

### Purpose of `/var/lib/cloud`

This directory helps cloud-init track the instance lifecycle across reboots, ensuring that initialization scripts and user-data are only run when appropriate. It distinguishes between first boot and subsequent boots.

---

### Directory Structure

Typical structure of `/var/lib/cloud/` includes:

```plaintext
/var/lib/cloud/
├── data/
│   ├── result.json            # Final cloud-init result in JSON format
│   └── status.json            # Contains execution status
├── handlers/                  # For custom handler scripts
├── instance/                  # Symlink to current instance directory
├── instances/
│   └── <instance-id>/         # Stores metadata and user-data for this instance
├── scripts/
│   ├── per-boot/              # Scripts run on every boot
│   ├── per-instance/          # Scripts run once per instance
│   ├── per-once/              # Scripts run only once ever
│   └── vendor/                # Scripts provided by the image vendor
├── sem/                       # Semaphore files to track script execution
```

---

### Key Files and Directories

- **`data/status.json`**: Indicates whether cloud-init ran successfully.
- **`instances/<instance-id>/`**: Contains metadata, user-data, and seed information specific to the current instance.
- **`scripts/*`**: Custom scripts executed by cloud-init at different lifecycle stages.
- **`sem/`**: Tracks whether specific modules or stages have completed to avoid re-execution.

---

### Usage Example

If you want to debug or verify what happened during the boot process:

```bash
cat /var/lib/cloud/data/status.json
```

To examine the user-data provided to the instance:

```bash
cat /var/lib/cloud/instances/<instance-id>/user-data.txt
```

To check logs:

```bash
less /var/log/cloud-init.log
```

---

### Cleanup for Re-Provisioning

If you're reusing a VM image and want cloud-init to rerun on first boot:

```bash
sudo cloud-init clean --logs
```

This clears `/var/lib/cloud/` and resets the instance metadata and state.

---

### Security Considerations

- Protect access to `/var/lib/cloud` as it may contain sensitive instance metadata.
- Be cautious when copying VM images with populated `/var/lib/cloud`; use `cloud-init clean`.

---

### Conclusion

The `/var/lib/cloud` directory is essential for managing instance initialization via cloud-init. It provides transparency and control over instance lifecycle configuration, allowing cloud platforms to automate deployment and configuration securely and efficiently.

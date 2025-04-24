# user-data

The `user-data` file is a core component of **cloud-init**, used to customize and configure cloud instances during their first boot. It allows users to inject scripts, configuration, or even full YAML-formatted cloud-init directives into cloud instances to automate provisioning tasks.

---

### Purpose of `user-data`

`user-data` enables automation of initial configuration such as:

- Installing software packages
- Creating users and setting SSH keys
- Configuring network interfaces
- Mounting volumes
- Running custom shell scripts or configuration management tools (e.g., Ansible, Puppet)

---

### Supported Formats

cloud-init supports various formats for `user-data`. The most common include:

#### 1. **Shell Scripts**

```bash
#!/bin/bash
echo "Hello from user-data script" > /home/ubuntu/welcome.txt
```

Must start with a shebang (`#!/bin/bash`).

#### 2. **Cloud-Config (YAML)**

```yaml
#cloud-config
users:
  - name: devuser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3...

packages:
  - nginx
  - git

runcmd:
  - [ systemctl, start, nginx ]
```

Starts with `#cloud-config`.

#### 3. **Multi-Part MIME Archives**

For combining shell scripts, cloud-config, and other formats.

```bash
Content-Type: multipart/mixed; boundary="===============123=="
MIME-Version: 1.0

--===============123==
Content-Type: text/cloud-config

#cloud-config
hostname: myserver

--===============123==
Content-Type: text/x-shellscript

#!/bin/bash
echo "Configuring server" > /tmp/setup.log

--===============123==--
```

Generated using tools like `cloud-init devel make-mime`.

---

### How to Provide `user-data`

- **AWS EC2**: Via `--user-data` parameter in CLI or through the console.
- **OpenStack**: Through Horizon UI or `nova boot --user-data`.
- **Vagrant**: By placing it in the `Vagrantfile` under `config.vm.provision`.

Example with Vagrant:

```ruby
config.vm.provision "file", source: "user-data", destination: "/tmp/user-data"
```

---

### Viewing user-data on a Running Instance

```bash
cat /var/lib/cloud/instances/$(cloud-init query instance_id)/user-data.txt
```

Or for EC2:

```bash
curl http://169.254.169.254/latest/user-data
```

---

### Tips for Writing `user-data`

- Always validate cloud-config YAML using `cloud-init schema --config-file <file>`.
- Use `cloud-init single --file <file> --name <module>` to test modules.
- Avoid putting sensitive data in plain text `user-data`.

---

### Conclusion

The `user-data` file is a powerful and flexible way to automate cloud instance initialization, supporting everything from basic scripting to full-blown configuration management. When properly used, it enables reproducible, hands-free infrastructure provisioning in cloud-native environments.

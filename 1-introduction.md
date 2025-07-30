# Ansible 

Ansible is an open source IT automation engine that automates

- provisioning
- configuration management
- application deployment
- orchestration
- other IT processes. 

It is free to use, and the project benefits from the experience and intelligence of its thousands of contributors.

### Working of Ansible

Ansible is agentless in nature, which means you don't need install any software on the manage nodes.

Ansible connects to the managed node using SSH or WinRM.
It pushes small programs called modules to perform tasks (like installing a package, starting a service, copying files).
These modules describe the desired state (e.g., “nginx should be installed”).
The module is executed on the remote system.
Once done, the module is removed from the system.

### Ansible Modules

These are small scripts written in Python, PowerShell, or other languages.
They are idempotent — meaning, if the system is already in the desired state, nothing changes.

```
- name: Install nginx
  apt:
    name: nginx
    state: present
```

If nginx is already installed, Ansible won’t do anything.

### Benifits of Ansible Over Shell Scripts

- Shell Scripting works only for Linux. Ansible works for both Linux and Windows. It connects over SSH (Linux) or WinRM (Windows), making setup easy and lightweight.
- Ansible modules are idempotent, meaning they only make changes when needed. Shell scripts re-run commands blindly, which can cause errors or unnecessary changes.
- Ansible uses YAML for playbooks, which is easier to read, write, and maintain than shell scripts full of complex commands.
- Ansible automatically handles task failures and can stop the playbook or skip steps based on conditions. In shell scripts, error handling must be written manually (if, exit, ||, etc.).
- Ansible can manage hundreds or thousands of servers at once using inventories. Shell scripts are hard to scale — often require loops and manual IP management.
- Ansible supports roles to organize tasks, variables, handlers, and templates. We can easily reuse them as per our requirements.
- Ansible has 1000+ ready-to-use modules (for packages, users, files, services, cloud, etc.). Shell scripts require writing everything from scratch.
- Ansible can define groups of servers and run tasks only on selected groups. In shell scripts, this needs manual looping and is error-prone.
- Ansible supports --check mode to preview changes without applying them. Shell scripts have no such built-in capability.


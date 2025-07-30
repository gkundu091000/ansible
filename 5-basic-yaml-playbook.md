# Playbook

A **Playbook** is a YAML file that defines a series of actions to be executed on managed nodes. It contains one or more "plays" that map groups of hosts to roles.

## Play

A Play is a single, complete execution unit within a playbook. It specifies which hosts to target and what tasks to execute on those hosts. Plays are used to group related tasks and execute them in a specific order.

```
- name: Install and configure Nginx
  hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

## Modules

Modules are the building blocks of Ansible tasks. They are small programs that perform a specific action on a managed node, such as installing a package, copying a file, or managing services.
Example

The apt module used in a task to install a package:

```
- name: Install Nginx
  apt:
    name: nginx
    state: present
```

## Tasks

Tasks are individual actions within a play that use modules to perform operations on managed nodes. Each task is executed in order and can include conditionals, loops, and handlers.
      
```
- name: Install Nginx
  apt:
    name: nginx
    state: present

- name: Start Nginx service
  service:
    name: nginx
    state: started
```

## Collections

A Collection is a packaging format in Ansible that bundles:

- Roles
- Modules
- Plugins
- Playbooks
- Documentation

Collections make it easy to distribute, share, and reuse Ansible content across projects.
Example

A collection structure might look like this:

```
my_collection/
├── roles/
│   └── my_role/
│       └── tasks/
│           └── main.yml
├── plugins/
│   └── modules/
│       └── my_module.py
├── docs/
│   └── index.md
├── README.md
└── galaxy.yml

```


### Playbook for Installing Apache

```yaml
# Installing Apache on WebServers

- name: Installing Apache on Ubuntu Web-Servers
  hosts: ubuntu-web-servers
  remote_user: ubuntu
  become: yes

  tasks:
  - name: Updating Apt Cache
    apt:
      update_cache: yes

  - name: Installing Apache
    apt:
      name: apache2
      state: present

  - name: Starting Apache Service
    service:
      name: apache2
      state: started
      enabled: yes


- name: Installing Apache on Redhat Web-Servers
  hosts: redhat-web-servers
  remote_user: admin-user
  become: yes

  tasks:
  - name: Updating Yum Cache
    yum:
      update_cache: yes

  - name: Installing Apache
    yum:
      name: httpd
      state: present

  - name: Starting Apache Service
    service:
      name: httpd
      state: started
      enabled: yes
  - name: Open HTTP port in firewalld (if enabled)
      firewalld:
        service: httpd
        permanent: yes
        state: enabled
        immediate: yes
      when: ansible_facts.services['firewalld'].state == 'running'
```

### Playbook For Updating DB Servers

```yaml
- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.yum:
      name: postgresql
      state: latest

  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started
```


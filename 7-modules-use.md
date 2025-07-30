### Service Module

- name: service_name
- state: started | stopped | restarted | reloaded
- enabled: yes | no

```yaml
- name: Ensure SSH is running and enabled
  ansible.builtin.service:
    name: ssh
    state: started
    enabled: yes
```

```yaml
- name: Copy my.cnf
  ansible.builtin.copy:
    src: files/my.cnf
    dest: /etc/mysql/my.cnf
    notify:
      - Restart MySQL

- name: Restart MySQL
  ansible.builtin.service:
    name: mysql
    state: restarted
  listen: Restart MySQL
```

### User Module

- name: username
- state: present | absent
- password: hashed_password
- uid: user-id
- group: primary-group
- groups: secondary-group
- append: yes				#  To append user to groups without removing from others
- shell: /bin/bash
- home: home_directory_of_user
- create_home: yes | no
- password_lock: Lock or unlock the password


```yaml
- name: Create a user with details
  ansible.builtin.user:
    name: devuser
    comment: "Developer Account"
    shell: /bin/bash
    home: /home/devuser
    create_home: yes
```

```yaml
- name: Add user with UID and groups
  ansible.builtin.user:
    name: devops
    uid: 1050
    group: devs
    groups: docker,sudo
    append: yes
```


### Copy Module

- src: Source file path on control node
- dest: Destination path on the target host
- owner: Set file owner
- group: Set file group owner
- mode: File Permissions ( e.g., '0644', '0755' )
- force: Replace file if content differs (default: yes)
- backup: If `yes`, create a backup of existing file before overwriting
- content: Inline content instead of using src
- remote_src: If `yes`, copy file from remote to remote (not from control machine)


```yaml
- name: Copy config file with permissions
  ansible.builtin.copy:
    src: files/my.conf
    dest: /etc/myapp/my.conf
    owner: root
    group: root
    mode: '0644'
```

```yaml
- name: Write a message to /etc/motd
  ansible.builtin.copy:
    content: "Welcome to the server managed by Ansible.\n"
    dest: /etc/motd
```

```yaml
- name: Copy file with backup enabled
  ansible.builtin.copy:
    src: files/my.cnf
    dest: /etc/mysql/my.cnf
    backup: yes
```

```yaml
- name: Copy file from one location to another on the same remote host
  hosts: server1
  become: yes
  tasks:
    - name: Copy file using remote_src
      ansible.builtin.copy:
        src: /etc/nginx/nginx.conf
        dest: /tmp/nginx_backup.conf
        remote_src: yes
        backup: yes
```

### apt Module


```yaml
- hosts: all
  become: yes
  tasks:
    - name: Install packages
      apt:
        name: ['git', 'curl', 'vim']
        state: present
        update_cache: yes
```

### Reboot Module

```yaml
- hosts: all
  become: yes
  tasks:
    - name: Reboot the server
      reboot:
        reboot_timeout: 300
```


### cron Module

- name: Identifier to help manage this cron job
- job: The actual command to run
- minute: Minute field (0-59, *, etc.)
- hour: Hour field (0-23, *, etc.)
- day: Day of month (1-31, *)
- month: Month (1-12, *)
- weekday: Day of week (0-6 or sun-sat, *)
- user: User under whom the cron runs
- state: `present` (default) or `absent` (to remove the job)
- disabled: `yes` or `no` – disables the job without deleting it

```yaml
- name: Cron
  hosts: server1
  become: yes
  tasks:
    - name: Setting Up Cron Job Every 1 Min
      ansible.builtin.cron:
        minute: 2
        hour: "*"
        day: "*"
        month: "*"
        # weekday: *
        name: Cal Job
        job: cal >> /home/ubuntu/cal.txt
        user: ubuntu
```

```yaml
- name: Cron
  hosts: server1
  become: yes
  tasks:
    - name: Setting Up Cron Job Every 1 Min
      ansible.builtin.cron:
        name: Cal Job
        user: ubuntu
        state: absent
```

### File Module

It is used to change file permissions on remote machines

- path: File or directory path to manage
- state: file, directory, absent, touch, link, or hard
- mode: Permissions (e.g., '0644', '0755')
- owner: File owner
- group: File group
- recurse: If yes, applies owner/mode recursively (only for dirs)
- src: Source path for link or hard links
- force: For symlinks, `yes` to replace existing file


```yaml
- name: Create log directory
  ansible.builtin.file:
    path: /var/log/myapp
    state: directory
    owner: root
    group: root
    mode: '0755'
```

```yaml
- name: Create an empty file
  ansible.builtin.file:
    path: /tmp/testfile.txt
    state: touch
    mode: '0644'
```

```yaml
- name: Delete a file
  ansible.builtin.file:
    path: /tmp/oldfile.txt
    state: absent
```

```yaml
- name: Create a symlink
  ansible.builtin.file:
    src: /usr/bin/python3
    path: /usr/bin/python
    state: link
```

### hostname

```yaml
- hosts: all
  become: yes
  tasks:
    - name: Set hostname
      hostname:
        name: web-{{ inventory_hostname }}
```












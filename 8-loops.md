# Looping Over a List

A list in Ansible is a collection of values. It’s often used to loop over multiple items.

```bash
packages:
  - nginx
  - git
  - curl
```

```yaml
- name: Install multiple packages
  hosts: all
  become: yes
  vars:
    packages:
      - nginx
      - git
      - curl

  tasks:
    - name: Install packages
      ansible.builtin.apt:
        name: "{{ item }}"
        state: present
      loop: "{{ packages }}"
```

```yaml
- name: Create multiple users # Loop with Inline List
  ansible.builtin.user:
    name: "{{ item }}"
    state: present
  loop:
    - user1
    - user2
    - user3
```

```yaml
- name: Create users with shell # Looping with Dictionary (key-value pair)
  ansible.builtin.user:
    name: "{{ item.name }}"
    shell: "{{ item.shell }}"
  loop:
    - { name: 'dev1', shell: '/bin/bash' }
    - { name: 'dev2', shell: '/bin/zsh' }
```

### Using with_items (old method, now replaced by loop)

```yaml
- name: Add multiple lines to file
  ansible.builtin.lineinfile:
    path: /etc/motd
    line: "{{ item }}"
  with_items:
    - "Welcome to the server"
    - "Authorized access only"
```



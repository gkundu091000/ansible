# Ansible Roles

An Ansible Role is a modular, reusable, and self-contained unit of automation used to organize related tasks, variables, templates, files, and handlers into a standardized file structure.

Roles are extremely useful for:
- Reusability of code
- Clean and readable playbooks
- Easier collaboration
- Better scalability and maintainability

## Ansible Role Directory Structure

```
<role_name>/
├── defaults/        # Default variables (lowest priority)
│   └── main.yml
├── vars/            # Role-specific variables (higher priority than defaults)
│   └── main.yml
├── files/           # Static files to copy (e.g., .conf files, scripts)
├── templates/       # Jinja2 templates (.j2 files) rendered during execution
├── tasks/           # Main list of role tasks
│   └── main.yml
├── handlers/        # Handlers triggered by tasks (e.g., restart service)
│   └── main.yml
├── meta/            # Metadata, including dependencies
│   └── main.yml
├── library/         # Custom modules (optional)
├── module_defaults/ # Default parameters for modules (optional)
└── lookup_plugins/  # Custom lookup plugins (optional)
```

## Key Components of an Ansible Role

### Tasks
The main list of actions that the role performs.

### Handlers
Tasks that are triggered by changes in other tasks, typically used for actions like restarting services.

### Files
Static files that need to be transferred to managed hosts.

### Templates
Jinja2 templates that can be rendered and transferred to managed hosts.

### Vars
Variables that are used within the role.

### Defaults
Default variables for the role, which can be overridden.

### Meta
Metadata about the role, including dependencies on other roles.

### Library
Custom modules or plugins used within the role.

### Module_defaults
Default module parameters for the role.

### Lookup_plugins
Custom lookup plugins for the role.


## Push your Ansible roles to Ansible Galaxy

1. Make sure your role is structured correctly. The basic structure should look like this:

```
my_role/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
├── tests/
│   ├── inventory
│   └── test.yml
└── vars/
    └── main.yml
```

2. Make sure ansible-galaxy CLI exists
```
ansible-galaxy --version
```

3. Push Your Role to GitHub
```
cd <role-name>
git init
git remote add origin <https://github.com/your_github_username/my_role.git>
git add .
git commit -m "Initial commit"
git push -u origin main
```

4. Import the Role to Ansible Galaxy

```
ansible-galaxy role import <your_github_username> <role-name>
```

# Understanding YAML

**YAML** is a **human-readable** data serialization format, commonly used for:
- Configuration files (like in Ansible, Docker, Kubernetes)
- Data exchange between programming languages
- Structured data representation (cleaner than JSON or XML)

### Strings, Numbers, and Booleans

```yaml
message: "Hello, World!"
number: 42
is_active: true
```
Strings can be quoted (" ") or unquoted if no special characters are used.
Booleans: true / false (lowercase)

###  List (Array)

```yaml
fruits:
  - Apple
  - Orange
  - Banana
```
Each list item starts with - and is indented under the key.

### Dictionary (Map)

```yaml
person:
  name: John Doe
  age: 30
  city: New York
```

Keys and values are separated by : and must be properly indented.

### List of Dictionaries

YAML supports nesting for complex data structures.

```yaml
family:
  parents:
    - name: Jane
      age: 50
    - name: John
      age: 52
  children:
    - name: Jimmy
      age: 22
    - name: Jenny
      age: 20
```

The parents and children keys each map to a list of dictionaries.



# 📘 Ansible Concepts & Troubleshooting Guide

## 🔧 Ansible Core Concepts

### 1. **What is Ansible?**

Ansible is an open-source IT automation tool that enables configuration management, application deployment, task automation, and multi-node orchestration.

### 2. **Key Features**

* Agentless (uses SSH)
* YAML-based playbooks
* Idempotent tasks (can be run multiple times without changing the result)
* Push-based configuration

### 3. **Ansible Architecture**

* **Control Node**: The system where Ansible is installed.
* **Managed Nodes**: The machines Ansible manages.
* **Inventory**: A file listing the managed nodes.
* **Modules**: Units of work executed by Ansible (e.g., `yum`, `copy`, `file`).
* **Playbook**: YAML file containing a set of tasks.
* **Task**: A single action to perform.
* **Role**: A way to organize playbooks and tasks for reuse.

### 4. **Inventory Management**

* INI format:

  ```ini
  [web]
  server1 ansible_host=192.168.1.100 ansible_user=ubuntu
  ```
* YAML format:

  ```yaml
  all:
    hosts:
      server1:
        ansible_host: 192.168.1.100
        ansible_user: ubuntu
  ```

### 5. **Ansible Commands**

* `ansible all -m ping`: Ping all hosts
* `ansible-playbook site.yml`: Run a playbook
* `ansible-inventory --list`: View inventory in JSON

### 6. **Playbook Structure**

```yaml
- hosts: webservers
  become: true
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

### 7. **Variables and Templates**

* Variables defined in `vars/`, `group_vars/`, `host_vars/`
* Jinja2 templating syntax: `{{ variable_name }}`

### 8. **Roles**

Structure:

```
roles/
  webserver/
    tasks/
      main.yml
    handlers/
    templates/
    vars/
    defaults/
```

Usage:

```yaml
- hosts: all
  roles:
    - webserver
```

### 9. **Handlers**

Used for operations that should run only when notified by another task.

```yaml
handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```


# 🛠️ Ansible Troubleshooting Scenarios

### 1. **SSH Connectivity Issues**

* **Symptom**: Host unreachable or timeout.
* **Fix**:

  * Ensure SSH access works manually.
  * Check inventory for `ansible_host`, `ansible_user`, or `ansible_ssh_private_key_file`.
  * Use `-vvvv` for verbose debugging.

### 2. **Permission Denied**

* **Symptom**: Access denied errors.
* **Fix**:

  * Use `--ask-become-pass` or set `become: true`.
  * Confirm the user has `sudo` privileges.

### 3. **Syntax Errors in Playbook**

* **Symptom**: YAML parsing errors.
* **Fix**:

  * Use `ansible-playbook --syntax-check`.
  * Use YAML validators like yamllint.

### 4. **Undefined Variables**

* **Symptom**: `variable is undefined` error.
* **Fix**:

  * Ensure variables are defined in correct scope (e.g., `group_vars`, `host_vars`).
  * Use `default` filter: `{{ my_var | default('value') }}`.

### 5. **Incorrect Module Usage**

* **Symptom**: Unexpected results from module execution.
* **Fix**:

  * Read official module documentation (e.g., `ansible-doc yum`).
  * Validate task structure and parameters.

### 6. **Handlers Not Triggering**

* **Symptom**: Changes made, but service not restarted.
* **Fix**:

  * Use `notify` properly within tasks.
  * Ensure `changed_when:` is triggering change status.

### 7. **Role Not Found**

* **Symptom**: Role missing error during playbook run.
* **Fix**:

  * Check roles/ directory or install via Ansible Galaxy: `ansible-galaxy install <role>`.
  * Validate path in `requirements.yml` and `ansible.cfg`.

### 8. **Template Errors**

* **Symptom**: Jinja2 template syntax errors.
* **Fix**:

  * Use `{% raw %}` tags for escaping.
  * Validate with `ansible-playbook --check`.

### 9. **Inventory File Not Detected**

* **Symptom**: No hosts matched error.
* **Fix**:

  * Use `-i inventory_file`.
  * Check group names and host entries.

### 10. **Facts Not Gathered**

* **Symptom**: `ansible_facts` variables are missing.
* **Fix**:

  * Ensure `gather_facts: true`.
  * Manually gather with `setup` module.

---

## ✅ Best Practices

* Use roles and folder structure for clean code.
* Store secrets securely (Ansible Vault).
* Use `ansible-lint` for linting.
* Write idempotent tasks.
* Use `check` and `diff` mode for dry-runs.
* Centralize inventory with dynamic inventory scripts or plugins.


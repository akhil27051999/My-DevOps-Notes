# 📘 Ansible & Argo CD Concepts & Troubleshooting Guide

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

* Ensure SSH works manually.
* Validate `ansible_host`, `ansible_user`, `ansible_ssh_private_key_file`.
* Use `-vvvv` for debug output.

### 2. **Permission Denied**

* Use `--ask-become-pass`.
* Ensure the user has sudo privileges.

### 3. **Syntax Errors in Playbook**

* Run `ansible-playbook --syntax-check`.
* Validate YAML formatting.

### 4. **Undefined Variables**

* Ensure variable is defined in the correct file.
* Use `default` filter to handle missing vars.

### 5. **Incorrect Module Usage**

* Read module documentation: `ansible-doc <module>`.

### 6. **Handlers Not Triggering**

* Ensure `notify` is used correctly and `changed_when:` is meaningful.

### 7. **Role Not Found**

* Install via `ansible-galaxy` or check role path.

### 8. **Template Errors**

* Validate Jinja2 syntax.
* Escape with `{% raw %}` where needed.

### 9. **Inventory Not Detected**

* Check `-i` flag and inventory structure.

### 10. **Facts Not Gathered**

* Use `gather_facts: true`.
* Run the `setup` module manually.


## ✅ Best Practices (Ansible)

* Use roles and folder structure.
* Store secrets in Ansible Vault.
* Write idempotent tasks.
* Use `ansible-lint`.
* Use `check` and `diff` mode.

---

## 🚀 Argo CD Concepts & Troubleshooting

### 🔍 What is Argo CD?

Argo CD is a declarative GitOps continuous delivery tool for Kubernetes.
It synchronizes application manifests in Git repositories with live Kubernetes clusters.

### 🔧 Core Concepts

* **Application**: Defines how a Git repo maps to Kubernetes resources.
* **Sync**: Applies desired state from Git to the cluster.
* **Repositories**: Git, Helm, or Kustomize sources.
* **Projects**: Group applications with RBAC control.
* **App of Apps**: Meta-application to manage multiple child apps.

### 🛠 Common Commands

* `argocd login <ARGOCD_SERVER>`
* `argocd app list`
* `argocd app sync <APP_NAME>`
* `argocd app delete <APP_NAME>`

### 🔑 GitOps Workflow

1. Developer commits to Git repo.
2. Argo CD detects changes.
3. Sync is triggered (manual or auto).
4. Cluster state is updated.

---

## 🧪 Argo CD Troubleshooting Scenarios

### 1. **App not syncing automatically**

* Check if auto-sync is enabled.
* Use UI or CLI: `argocd app set <APP> --sync-policy automated`

### 2. **Invalid manifest or YAML errors**

* Use `kubectl apply -f` locally to debug YAML.
* Check Argo CD logs or app details page.

### 3. **Permissions or RBAC Denied**

* Argo CD needs access via ServiceAccount.
* Review RBAC rules.

### 4. **Image not updating with latest tag**

* Use image updater or configure webhook with `argoproj-labs/argocd-image-updater`
* Avoid `:latest` tag for reproducibility.

### 5. **Kustomize/Helm build errors**

* Validate locally using `kustomize build` or `helm template`.
* Check repo path configuration.

### 6. **App stuck in OutOfSync state**

* Check diff tab in Argo CD UI.
* Use `argocd app diff` to see differences.

### 7. **Sync fails with resource conflict**

* Some resources may be managed by another controller.
* Use `argocd app sync --force` cautiously.

### 8. **App not showing in Argo CD UI**

* Ensure it is defined in the correct namespace.
* Verify `argocd app create` was successful.


## ✅ Best Practices (Argo CD)

* Use separate Git repos or folders per environment (dev/stage/prod).
* Enable `auto-prune` to remove orphaned resources.
* Use `sync-wave` annotations to control resource ordering.
* Monitor via Prometheus metrics exposed by Argo CD.
* Combine with Helm/Kustomize for templating.

Let me know if you want a real-world GitOps project example using Argo CD + Kubernetes + CI/CD.

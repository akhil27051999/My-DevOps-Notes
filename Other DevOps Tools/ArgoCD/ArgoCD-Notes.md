# 🚀 Argo CD Concepts & Troubleshooting

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


# 🧪 Argo CD Troubleshooting Scenarios

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

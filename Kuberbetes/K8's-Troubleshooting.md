# 🛠️ Kubernetes Troubleshooting Guide

## 📦 1. Pod Issues

### ❌ Issue: Pod stuck in `CrashLoopBackOff`

**Causes:**

* App crashes due to bugs or config issues
* Wrong image or environment variables

**Debug Steps:**

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

**Solution:**

* Check `logs` for application errors
* Verify env variables, configMaps, secrets
* If imagePullError, check image name or registry

---

### ⏳ Issue: Pod stuck in `Pending`

**Causes:**

* Insufficient resources (CPU/Memory)
* No matching node (taints, affinity)

**Debug Steps:**

```bash
kubectl describe pod <pod-name>
kubectl get nodes
```

**Solution:**

* Check if nodes have enough allocatable resources
* Adjust `requests/limits` in pod spec
* Remove `nodeSelector`, affinity, or taints if needed


## 🧠 2. Node Issues

### 🔌 Issue: Node in `NotReady` state

**Causes:**

* kubelet is down
* Network/CNI issues
* Resource exhaustion

**Debug Steps:**

```bash
kubectl get nodes
kubectl describe node <node-name>
ssh <node> && journalctl -u kubelet
```

**Solution:**

* Restart kubelet: `systemctl restart kubelet`
* Check disk space, CPU
* Validate CNI plugins are configured


## 🌐 3. Service & Networking Issues

### 🤭 Issue: Service not reachable (ClusterIP/NodePort)

**Causes:**

* Wrong selector
* Target pod not running
* Firewall or network policy blocking traffic

**Debug Steps:**

```bash
kubectl get svc
kubectl describe svc <service-name>
kubectl get endpoints <service-name>
```

**Solution:**

* Ensure pod labels match service `selector`
* Verify port config (`targetPort`, `port`, `nodePort`)
* Check if pods are actually running and healthy

---

### 🌐 Issue: External access not working (LoadBalancer/NodePort)

**Causes:**

* LoadBalancer not provisioned by cloud provider
* NodePort not open in firewall

**Solution:**

* For LoadBalancer, ensure cloud integration (e.g., AWS ELB created)
* For NodePort, open the port in cloud firewall
* Use `curl http://<nodeIP>:<nodePort>` to test


## 🌍 4. Ingress Issues

### 🔐 Issue: Ingress returns 404 or 503

**Causes:**

* Ingress controller not installed
* Wrong backend service name/port
* TLS misconfigured

**Debug Steps:**

```bash
kubectl get ingress
kubectl describe ingress <ingress-name>
kubectl get svc
kubectl get pods -n ingress-nginx
```

**Solution:**

* Verify `ingress-nginx` controller is running
* Match backend service name & port in ingress spec
* Use correct `host`, `pathType: Prefix`, and TLS secret


## 🔒 5. ConfigMap/Secret Issues

### ⚙️ Issue: Env variables not injecting

**Causes:**

* Wrong key name
* ConfigMap/Secret not found

**Debug Steps:**

```bash
kubectl describe pod <pod-name>
kubectl get configmap
kubectl get secret
```

**Solution:**

* Check `env.valueFrom.configMapKeyRef/secretKeyRef`
* Ensure resource exists and keys are correct


## 🧱 6. Volume & PVC Issues

### 📁 Issue: PVC stuck in `Pending`

**Causes:**

* No matching PV
* StorageClass misconfigured

**Debug Steps:**

```bash
kubectl get pvc
kubectl describe pvc <pvc-name>
kubectl get storageclass
```

**Solution:**

* Ensure PV exists with same `accessMode` and size
* Check if default `StorageClass` exists
* Fix provisioner or reclaim policy if using dynamic provisioning

---

### 📦 Issue: VolumeMount errors in Pod

**Causes:**

* Wrong mount path or claimName
* PVC not bound

**Solution:**

* Match `claimName` exactly
* Validate PVC is `Bound`
* Inspect volume permissions (`hostPath` issues)


## 🚥 7. Scaling & Autoscaling Issues

### 📉 Issue: HPA not scaling pods

**Causes:**

* Metrics server not installed
* Wrong HPA config

**Debug Steps:**

```bash
kubectl get hpa
kubectl top pod
kubectl describe hpa
```

**Solution:**

* Install metrics-server
* Ensure target CPU utilization is configured
* Verify workload supports scaling (e.g., Deployment)


## 🧰 8. CI/CD & Image Pull Issues

### ❌ Issue: `ImagePullBackOff` / `ErrImagePull`

**Causes:**

* Wrong image name
* Private registry without credentials

**Debug Steps:**

```bash
kubectl describe pod <pod-name>
```

**Solution:**

* Correct the image name
* Create imagePullSecret for private registries:

```bash
kubectl create secret docker-registry regcred \
  --docker-server=<registry> \
  --docker-username=<user> \
  --docker-password=<pass> \
  --docker-email=<email>
```

## 🔒 9. RBAC & Permission Issues

### 🔐 Issue: `Forbidden` error when accessing API

**Causes:**

* Missing RBAC permissions
* Wrong ServiceAccount

**Debug Steps:**

```bash
kubectl auth can-i <verb> <resource> --as <user>
kubectl describe rolebinding <rb>
```

**Solution:**

* Use `Role`, `RoleBinding`, `ClusterRole` as needed
* Bind proper permissions to the service account

---

## 🎯 Summary Cheatsheet

| Area        | Issue            | Command / Fix                  |
| ----------- | ---------------- | ------------------------------ |
| Pod         | CrashLoopBackOff | `kubectl logs`, fix env/image  |
| Service     | Not reachable    | Check endpoints, selector      |
| Ingress     | 404 / 503        | Verify controller, backend svc |
| Volume      | PVC Pending      | Check PV, StorageClass         |
| Autoscaling | HPA not working  | Install metrics-server         |
| RBAC        | Forbidden errors | Assign roles/roleBindings      |


* 💡 **Pro Tip**: Always start with `kubectl describe` and `kubectl logs` — 80% of issues are revealed through them!


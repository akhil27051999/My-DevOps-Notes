# 📘 Kubernetes Interview Questions & Answers

This document contains the most frequently asked Kubernetes interview questions, categorized by topic with sample answers and explanations.

---

## 🧱 1. Core Concepts

### Q1. What is Kubernetes?

**Answer:** Kubernetes (K8s) is an open-source container orchestration platform for automating deployment, scaling, and management of containerized applications.

### Q2. What is a Pod in Kubernetes?

**Answer:** A Pod is the smallest and simplest unit in Kubernetes. It can contain one or more containers that share the same network namespace and storage.

### Q3. What is a ReplicaSet?

**Answer:** ReplicaSet ensures a specified number of replicas of a Pod are running at any time. It replaces failed Pods automatically.

### Q4. What is a Deployment?

**Answer:** A Deployment manages ReplicaSets and provides declarative updates to Pods. It supports rolling updates and rollbacks.

---

## 🚀 2. Services & Networking

### Q5. What are the different types of services in Kubernetes?

**Answer:**

* ClusterIP (default): Internal communication
* NodePort: Exposes service on static port on each node
* LoadBalancer: Exposes service via cloud load balancer
* ExternalName: Maps service to external DNS

### Q6. How does service discovery work in Kubernetes?

**Answer:** Kubernetes uses DNS and environment variables to discover services. Each service gets a DNS entry.

---

## 📦 3. Storage & Volumes

### Q7. What is a PersistentVolume (PV) and PersistentVolumeClaim (PVC)?

**Answer:**

* PV: Actual storage resource in the cluster
* PVC: User request for storage resources

### Q8. What is a StorageClass?

**Answer:** It allows dynamic provisioning of storage and defines how PVs are created.

---

## 🔐 4. Security & RBAC

### Q9. What is a ConfigMap and Secret?

**Answer:**

* ConfigMap: Stores non-confidential configuration data
* Secret: Stores sensitive data like passwords in base64 encoded format

### Q10. What is the difference between Role and ClusterRole?

**Answer:**

* Role: Grants permissions within a namespace
* ClusterRole: Grants permissions cluster-wide

---

## 📊 5. Scaling & Auto Healing

### Q11. How does Kubernetes auto-scale?

**Answer:** With HorizontalPodAutoscaler (HPA), which scales pods based on metrics (CPU/memory).

### Q12. What is a Liveness Probe and Readiness Probe?

**Answer:**

* Liveness: Checks if the app is alive; restarts if failed
* Readiness: Checks if the app is ready to serve traffic

---

## 🛠️ 6. Troubleshooting

### Q13. How do you debug a pod stuck in CrashLoopBackOff?

**Answer:**

* Run `kubectl describe pod <pod>`
* Check logs with `kubectl logs <pod>`
* Look for init container issues or bad env vars

### Q14. What do you do if a service is not reachable?

**Answer:**

* Validate endpoints: `kubectl get endpoints`
* Check pod IPs, labels, and selectors
* Use `nslookup`, `curl`, and `netshoot`

---

## ⛓️ 7. CI/CD & GitOps

### Q15. How does GitOps work with Kubernetes?

**Answer:** GitOps uses Git as the source of truth. Tools like ArgoCD or Flux sync Kubernetes manifests from Git to clusters.

### Q16. How do you deploy applications in Kubernetes using Helm?

**Answer:**

* Package app as Helm chart
* Use `helm install` or `helm upgrade` for deployment

---

## 📘 8. Advanced Topics

### Q17. What are Taints and Tolerations?

**Answer:**

* Taints prevent pods from scheduling on certain nodes
* Tolerations allow exceptions to taints

### Q18. What is a StatefulSet?

**Answer:** Used for managing stateful applications with persistent storage and stable network identities (e.g., databases)

### Q19. What is a DaemonSet?

**Answer:** Ensures that a pod runs on all (or some) nodes. Common for logging, monitoring agents.

### Q20. What is a Sidecar Container?

**Answer:** A helper container in the same Pod as the main app. Often used for logging, proxies, service mesh (e.g., Istio Envoy).

---

## ✅ Bonus: Commands Cheat Sheet

```bash
kubectl get pods
kubectl describe pod <pod>
kubectl logs <pod>
kubectl exec -it <pod> -- /bin/sh
kubectl get svc
kubectl get nodes
kubectl top pod
kubectl apply -f deployment.yaml
```

Let me know if you'd like behavioral questions or mock interview scenarios added too.

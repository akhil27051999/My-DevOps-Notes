# 🚀 Kubernetes (K8s) - Complete Overview and Resources

Kubernetes (K8s) is an 🛠️ open-source container orchestration platform that automates deployment, scaling, and management of containerized applications 🚢. It is essential for managing microservices architecture 🖥️ with features like:

- 📈 Auto-scaling
- 🌐 Networking
- 📊 Monitoring
- ⚖️ Load balancing

---

## 🏗️ Kubernetes Architecture

Kubernetes follows a **client-server architecture** with **Master Nodes** and **Worker Nodes**.

### 1. Master Node Components 👑
| Component | Description |
|----------|-------------|
| **API Server** | Entry point for all REST operations on cluster objects |
| **Scheduler** | Places Pods on the most appropriate nodes |
| **Controller Manager** | Maintains desired state of the cluster |
| **etcd** | Key-value store for all cluster data |
| **Cloud Controller Manager** | Integrates Kubernetes with cloud providers |

### 2. Worker Node Components 🧑‍💻
| Component | Description |
|----------|-------------|
| **Kubelet** | Ensures containers are running properly |
| **Kube Proxy** | Manages networking rules for Pod communication |
| **Container Runtime** | Executes containers (Docker, containerd) |


## 🔑 Key Kubernetes Components

- **Pods**: Smallest unit; encapsulates containers.
- **ReplicaSets**: Ensures defined number of Pods run at all times.
- **Deployments**: Manages ReplicaSets and provides rolling updates.
- **Services**: Exposes Pods using DNS and load balancing.
- **Namespaces**: Logical partitioning of cluster resources.


## 🚀 Why Kubernetes is Used

- 📈 **Scalability** – Auto scale apps with changing demand.
- 🏞️ **Portability** – Supports public, private, and hybrid clouds.
- 🤖 **Automation** – Handles self-healing, rollouts, updates.
- 🔋 **Efficiency** – Optimizes resource utilization.
- 🖥️ **Microservices Friendly** – Perfect for service-oriented apps.


## 🌍 Real-World Use Cases

- 💻 Web Hosting (Highly available apps)
- ⚙️ CI/CD Pipelines (Automated testing/deployments)
- 🌐 Hybrid Cloud Deployments
- 📊 Big Data Workloads (Spark, Hadoop)
- 🌱 IoT Applications (Edge device management)


## 🔍 Industry Needs Fulfilled by Kubernetes

- ⏱️ Faster deployments
- ⚡ Improved productivity
- 💪 High availability
- 💸 Cost efficiency
- 🌀 Environment consistency



# 🧠 1. Compute / Workload Resources

## 📦 1. Pod

**Definition:**  
The smallest and simplest unit in Kubernetes. A Pod represents a single instance of a running process and can contain one or more containers.

**Use Case:**  
Running applications or services in containers.

**YAML:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
      ports:
        - containerPort: 80
```

## 🧬 2. ReplicaSet

**Definition:**  
Ensures a specified number of identical Pods are running at any given time. Often controlled by a Deployment.

**Use Case:** 
Maintaining a specific number of replicas for a Pod.

**YAML:**

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```

## 🚀 3. Deployment
**Definition:**  
Provides declarative updates to Pods and manages ReplicaSets. Supports rolling updates, rollbacks, and scaling.

**Use Case:** 
Rolling updates, rollback, and horizontal scaling of applications.

**YAML:**

```yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```
            
## 💾 4. StatefulSet
**Definition:**  
Used for managing stateful applications requiring persistent storage and stable network IDs. Maintains the order and uniqueness of Pods.

**Use Case:** 
Running databases and distributed systems.

**YAML:**

```yaml

apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-statefulset
spec:
  serviceName: "nginx"
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```

## 🛡️ 5. DaemonSet
**Definition:**  
Ensures a Pod runs on every node (or selected nodes) in the cluster. Commonly used for log collection, monitoring agents, etc.

**Use Case:** 
Running system-level services on all cluster nodes.

**YAML:**

```yaml

apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
spec:
  selector:
    matchLabels:
      name: log-agent
  template:
    metadata:
      labels:
        name: log-agent
    spec:
      containers:
        - name: fluentd
          image: fluent/fluentd
```

## 📅 6. Job
**Definition:**  
Manages the execution of one or more Pods to completion. Ensures the Pods terminate successfully.

**Use Case:** 
Running one-time or batch jobs (e.g., database backups).

**YAML:**

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: my-job
spec:
  template:
    metadata:
      name: my-job-pod
    spec:
      containers:
        - name: my-job
          image: busybox
          command: ["echo", "Hello World"]
      restartPolicy: Never
  ```

## ⏰ 7. CronJob
**Definition:**  
Schedules Jobs to run at specific intervals, similar to cron jobs in Unix systems.

**Use Case:** 
Running tasks like backups, report generation, and cleanup on schedule.

**YAML:**

```yaml

apiVersion: batch/v1
kind: CronJob
metadata:
  name: my-cronjob
spec:
  schedule: "*/5 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: hello
              image: busybox
              command: ["echo", "Scheduled Task"]
          restartPolicy: OnFailure
  ```        

# 🔌 2. Networking Resources

## 📡 Service (ClusterIP)

**Definition:**  
A `Service` provides a stable internal endpoint for accessing a group of Pods. The `ClusterIP` type is the default, and is only accessible from within the cluster.

**Use Case:**  
Internal communication between microservices or applications.

**YAML:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-clusterip-service
spec:
  type: ClusterIP
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
```

## 🌐 Service (NodePort)
**Definition:**  
Exposes the service on each node’s IP at a static port (30000–32767). Useful for development/testing or when not using a cloud provider.

**Use Case:** 
External access to services without using Ingress.

**YAML:**

```yaml

apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30080
```

## ☁️ Service (LoadBalancer)
**Definition:**  
Creates an external load balancer (in supported cloud environments) to route traffic to the service.

**Use Case:** 
Production-grade access from the internet via a cloud provider’s load balancer.

**YAML:**

```yaml

apiVersion: v1
kind: Service
metadata:
  name: my-lb-service
spec:
  type: LoadBalancer
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
```
## 🧭 Ingress
**Definition:**  
An Ingress manages external HTTP/HTTPS access to services. It allows SSL termination, path-based routing, and domain-based routing.

**Use Case:** 
Expose multiple services via a single external IP with routing rules.

**YAML:**

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-clusterip-service
                port:
                  number: 80
```

## 🔐 NetworkPolicy
**Definition:**
Defines rules for ingress and egress traffic between Pods. By default, Kubernetes allows all traffic; NetworkPolicy lets you restrict access.

**Use Case:**
Secure Pod-to-Pod communication, limit access by labels or namespaces.

**YAML:**

```yaml

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend
spec:
  podSelector:
    matchLabels:
      role: frontend
  policyTypes:
    - Ingress
  ingress:
    - from:
        - podSelector:
            matchLabels:
              role: backend
```

# 💾 3. Storage Resources

## 📦 PersistentVolume (PV)
**Definition:**
A PersistentVolume (PV) is a piece of storage in the cluster, provisioned manually or dynamically. It provides storage to Pods.

**Use Case:**
Define available storage resources in the cluster.

**YAML:**

```yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

## 📨 PersistentVolumeClaim (PVC)
**Definition:**
A PersistentVolumeClaim (PVC) is a request for storage by a Pod. It binds to an available PV that matches the request.

**Use Case:**
Claiming storage from a PV for use inside a container.

**YAML:**

```yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

## 🧱 StorageClass
**Definition:**
A StorageClass enables dynamic provisioning of PersistentVolumes. Different classes can define different types of storage (e.g., SSD, HDD).

**Use Case:**
Provision PVs on demand using different performance tiers.

**YAML:**

```yaml

apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
```

## 🔗 VolumeMount (in Pod)
**Definition:**
A VolumeMount is used to mount a PVC into a container at a specified path.

**Use Case:**
Attach persistent storage to a container.

**YAML:**

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: pod-with-volume
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: html-volume
  volumes:
    - name: html-volume
      persistentVolumeClaim:
        claimName: my-pvc
```

# 🔐 4. Security & Access Control

## 📄 ConfigMap

**Definition:**  
Stores non-sensitive config data in key-value format. Useful for app configuration.

**Use Case:**  
Pass environment variables or files to containers.

**YAML:**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  APP_ENV: production
  DB_HOST: db-service

```

## 🧬 Mount ConfigMap in Pod
**Use Case:**
Inject configuration into Pods via environment variables or volume mounts.

**YAML:**

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: pod-using-configmap
spec:
  containers:
    - name: myapp
      image: myapp:latest
      env:
        - name: APP_ENV
          valueFrom:
            configMapKeyRef:
              name: my-configmap
              key: APP_ENV
      volumeMounts:
        - mountPath: "/etc/config"
          name: config-volume
  volumes:
    - name: config-volume
      configMap:
        name: my-configmap
```

## 🔐 Secret

**Definition:**
Stores sensitive information like credentials, tokens, SSH keys in base64 encoded format.

**Use Case:**
Inject secrets into Pods securely.

**YAML:**

```yaml

apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: YWRtaW4=
  password: cGFzc3dvcmQ=
```

## 🔐 Mount Secret in Pod
**Use Case:**
Use secrets as environment variables or files in containers.

**YAML:**

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: pod-using-secret
spec:
  containers:
    - name: myapp
      image: myapp:latest
      env:
        - name: DB_USER
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: username
        - name: DB_PASS
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: password
```
# 🛡 5. Access Control (RBAC)

## 🧾 ServiceAccount
**Use Case:**
Provides identity to a Pod for Kubernetes API interaction.

**YAML:**

```yaml

apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-serviceaccount
```
## 👤 Role
**Use Case:**
Defines permissions (get/list/watch) in a namespace.

**YAML:**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "watch", "list"]
```
## 🔗 RoleBinding
**Use Case:**
Assign a Role to a user/group/ServiceAccount in a namespace.

**YAML:**

```yaml

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
  - kind: ServiceAccount
    name: my-serviceaccount
    namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
## 🌐 ClusterRole
**Use Case:**
Define global (cluster-wide) permissions.

**YAML:**

```yaml

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-admin
rules:
  - apiGroups: [""]
    resources: ["*"]
    verbs: ["*"]
```
## 🌐 ClusterRoleBinding
**Use Case:**
Assign a ClusterRole across the cluster to ServiceAccounts/users.

**YAML:**

```yaml

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-binding
subjects:
  - kind: ServiceAccount
    name: my-serviceaccount
    namespace: default
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```

# 🧩 6. Miscellaneous Resources
## 🗂 Namespace
**Definition:**
Isolates resources by team or environment.

**YAML:**

```yaml

apiVersion: v1
kind: Namespace
metadata:
  name: dev-environment
```

## 🚫 ResourceQuota
**Use Case:**
Limit CPU/Memory usage to prevent abuse.

**YAML:**

```yaml

apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev-environment
spec:
  hard:
    requests.cpu: "2"
    requests.memory: 1Gi
    limits.cpu: "4"
    limits.memory: 2Gi
```

## 📏 LimitRange
**Use Case:**
Enforce CPU/Memory default limits per container.

**YAML:**

```yaml

apiVersion: v1
kind: LimitRange
metadata:
  name: limit-range
  namespace: dev-environment
spec:
  limits:
    - default:
        cpu: 500m
        memory: 512Mi
      defaultRequest:
        cpu: 250m
        memory: 256Mi
      type: Container
```

## ⚖ HorizontalPodAutoscaler (HPA)
**Use Case:**
Auto-scale pods based on CPU/memory usage.

**YAML:**

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-deployment
  minReplicas: 2
  maxReplicas: 5
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```

## 🚨 PodDisruptionBudget (PDB)
**Use Case:**
Maintain service availability during voluntary disruptions.

**YAML:**

```yaml

apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: myapp-pdb
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: myapp
```


# 🔍 7. Observability & Monitoring

Monitoring is essential to ensure your workloads are healthy and performing as expected. Kubernetes offers built-in tools to inspect logs, metrics, and events.

| Tool/Resource              | Description                          | Practice Tools                    |
|---------------------------|--------------------------------------|----------------------------------|
| **Events**                | Cluster-level event logs             | `kubectl get events`             |
| **Logs**                  | View container logs from a Pod       | `kubectl logs <pod-name>`        |
| **Metrics Server**        | View CPU/Memory usage of pods/nodes  | `kubectl top pod` / `kubectl top node` |
| **Liveness/Readiness Probes** | Health checks for apps         | Prevent bad pods from serving    |

### ✅ Tips

- Liveness probes detect app crashes and restart containers.
- Readiness probes delay traffic until app is ready.
- Use Prometheus + Grafana for full observability dashboards.


# 🚀 8. Advanced & Production Resources

These features are critical when deploying Kubernetes in real-world or enterprise environments. They help improve **availability, scalability, scheduling**, and **startup logic**.

| Resource Type              | Description                                  | Practice Examples                    |
|---------------------------|----------------------------------------------|--------------------------------------|
| **HorizontalPodAutoscaler (HPA)** | Auto-scale Pods based on CPU/memory     | Scale based on CPU                   |
| **VerticalPodAutoscaler (VPA)**   | Auto-adjust Pod resource requests/limits | Tune memory/CPU usage                |
| **PodDisruptionBudget (PDB)**     | Maintain availability during disruptions | Limit concurrent updates             |
| **Affinity / AntiAffinity**       | Control pod placement on nodes           | Spread across zones/racks            |
| **Taints & Tolerations**          | Isolate workloads to specific nodes      | Use GPU nodes for ML apps            |
| **Init Containers**              | Pre-run tasks before main container      | DB schema migrations, config checks  |
| **Sidecar Containers**          | Add helper containers to main app pod    | Logging agent, service mesh proxy    |

### 📌 Notes

- Use **HPA** with Metrics Server or Prometheus Adapter.
- PDB helps during rolling updates to avoid full outages.
- Affinity/AntiAffinity is useful for HA and zone-aware deployments.

---

# ⚙️ 9. Tools for Practice & Real-World Workflow

Use these tools to **practice Kubernetes locally** and **manage production clusters** efficiently.

| Tool             | Use Case                             | Practice Idea                             |
|------------------|--------------------------------------|-------------------------------------------|
| **kubectl**      | CLI to manage Kubernetes             | Learn and practice all commands           |
| **K9s**          | Terminal UI for navigating clusters  | Manage pods, logs, events in TUI          |
| **Helm**         | Kubernetes package manager           | Deploy complex apps using Helm charts     |
| **Minikube / Kind** | Local Kubernetes cluster (multi-node) | Practice realistic cluster setups     |
| **Lens**         | Kubernetes dashboard GUI             | Visualize workloads, namespaces, pods     |

### 🔧 Recommended Practice Flow

1. Use **Kind** to set up a 3-node local cluster.
2. Deploy apps using **Helm**.
3. Monitor them via **Lens** or `kubectl`.
4. Simulate disruptions and autoscaling using **HPA**, **PDB**, and **affinity**.
5. Use **K9s** for fast debugging and navigation.

---











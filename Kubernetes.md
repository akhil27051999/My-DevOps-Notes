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

---

## 🔑 Key Kubernetes Components

- **Pods**: Smallest unit; encapsulates containers.
- **ReplicaSets**: Ensures defined number of Pods run at all times.
- **Deployments**: Manages ReplicaSets and provides rolling updates.
- **Services**: Exposes Pods using DNS and load balancing.
- **Namespaces**: Logical partitioning of cluster resources.

---

## 🚀 Why Kubernetes is Used

- 📈 **Scalability** – Auto scale apps with changing demand.
- 🏞️ **Portability** – Supports public, private, and hybrid clouds.
- 🤖 **Automation** – Handles self-healing, rollouts, updates.
- 🔋 **Efficiency** – Optimizes resource utilization.
- 🖥️ **Microservices Friendly** – Perfect for service-oriented apps.

---

## 🌍 Real-World Use Cases

- 💻 Web Hosting (Highly available apps)
- ⚙️ CI/CD Pipelines (Automated testing/deployments)
- 🌐 Hybrid Cloud Deployments
- 📊 Big Data Workloads (Spark, Hadoop)
- 🌱 IoT Applications (Edge device management)

---

## 🔍 Industry Needs Fulfilled by Kubernetes

- ⏱️ Faster deployments
- ⚡ Improved productivity
- 💪 High availability
- 💸 Cost efficiency
- 🌀 Environment consistency

---

## 🌟 Kubernetes Resources - YAML Examples

### 1️⃣ Pod

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

### 2️⃣ ReplicaSet
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

### 3️⃣ Deployment

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

### 4️⃣ StatefulSet

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

### 5️⃣ DaemonSet

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

### 6️⃣ Job
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

### 7️⃣ CronJob

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






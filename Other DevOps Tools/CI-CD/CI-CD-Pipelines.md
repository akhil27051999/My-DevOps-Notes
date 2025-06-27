# 🚀 CI/CD Pipeline Patterns for Modern Applications

This guide provides **end-to-end CI/CD pipeline strategies** using various tools like GitHub Actions, Jenkins, Docker, Kubernetes, Terraform, and ArgoCD. These patterns are commonly used in DevOps for microservices, serverless, GitOps, and secure deployments.

---

## 1. CI/CD Pipeline for Microservices

### 🎯 Objective

Automate the process of testing, building, and deploying multiple microservices.

### 🛠️ Tools

* **CI Tool**: GitHub Actions / Jenkins
* **Containerization**: Docker
* **Orchestration**: Kubernetes

### 🔁 Pipeline Steps

1. **Build**: Docker image per microservice using `docker build`
2. **Test**: Run unit tests (e.g., PyTest, Jest)
3. **Deploy**: Push to Kubernetes using manifests or Helm

### 📄 GitHub Actions Example

```yaml
yaml
name: CI/CD for Microservices
on:
  push:
    branches: [main]
jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Build Docker Image
        run: |
          docker build -t myapp:$GITHUB_SHA .
          docker push myapp:$GITHUB_SHA

      - name: Deploy to Kubernetes
        run: |
          kubectl apply -f k8s/deployment.yaml
          kubectl apply -f k8s/service.yaml
```

---

## 2. Jenkins Pipeline for Multi-Environment Deployment

### 🎯 Objective

Deploy applications to **Dev → Staging → Prod** environments.

### 📄 Jenkinsfile

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        script {
          docker.build("myapp:${GIT_COMMIT}")
        }
      }
    }
    stage('Deploy to Dev') {
      steps {
        script { deployToK8s('dev') }
      }
    }
    stage('Deploy to Staging') {
      steps {
        script { deployToK8s('staging') }
      }
    }
    stage('Deploy to Prod') {
      steps {
        script { deployToK8s('prod') }
      }
    }
  }
}

def deployToK8s(env) {
  sh "kubectl config use-context ${env}-context"
  sh "kubectl apply -f k8s/${env}/deployment.yaml"
  sh "kubectl apply -f k8s/${env}/service.yaml"
}
```

---

## 3. CI/CD with Infrastructure as Code (IaC)

### 🎯 Objective

Provision infrastructure using **Terraform** in the pipeline.

### 📄 GitHub Actions with Terraform

```yaml
name: IaC Pipeline
on:
  push:
    branches: [main]
jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Terraform
        uses: hashicorp/setup-terraform@v1

      - name: Terraform Init
        run: terraform init

      - name: Terraform Plan
        run: terraform plan

      - name: Terraform Apply
        run: terraform apply -auto-approve

      - name: Deploy App
        run: |
          kubectl apply -f k8s/deployment.yaml
          kubectl apply -f k8s/service.yaml
```

---

## 4. Docker + Kubernetes CI/CD Pipeline

### 📄 Jenkinsfile

```groovy
pipeline {
  agent any
  stages {
    stage('Build Docker Image') {
      steps {
        script { docker.build("myapp:${GIT_COMMIT}") }
      }
    }
    stage('Push Image') {
      steps {
        script { docker.push("myapp:${GIT_COMMIT}") }
      }
    }
    stage('Deploy to K8s') {
      steps {
        script {
          sh "kubectl apply -f k8s/deployment.yaml"
          sh "kubectl apply -f k8s/service.yaml"
        }
      }
    }
  }
}
```

---

## 5. CI/CD for Serverless (AWS Lambda)

### 📄 GitHub Actions

```yaml
name: Serverless CI/CD
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up AWS CLI
        run: |
          aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws configure set region ${{ secrets.AWS_REGION }}

      - name: Deploy Lambda
        run: |
          aws lambda update-function-code \
            --function-name my-function \
            --zip-file fileb://function.zip
```

---

## 6. Rollback Automation in CI/CD

### 📄 GitHub Actions

```yaml
name: CI/CD with Rollback
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Deploy
        run: kubectl apply -f k8s/deployment.yaml

      - name: Monitor & Rollback
        run: |
          kubectl rollout status deployment/myapp
          if [ $? -ne 0 ]; then
            echo "Rollback triggered"
            kubectl rollout undo deployment/myapp
          fi
```

---

## 7. GitOps Pipeline with ArgoCD

### 📄 ArgoCD App Manifest

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp
spec:
  destination:
    server: https://kubernetes.default.svc
    namespace: default
  source:
    repoURL: 'https://github.com/myorg/myapp.git'
    targetRevision: HEAD
    path: k8s/
  syncPolicy:
    automated: {}
```

> 💡 GitOps ensures that Git is the source of truth for deployments.

---

## 8. Multistage Dockerfile + CI/CD

### 📄 Dockerfile

```dockerfile
# Stage 1: Build
FROM node:14 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Stage 2: Run
FROM node:14
WORKDIR /app
COPY --from=build /app/dist .
CMD ["npm", "start"]
```

> 💡 Multistage builds reduce image size and separate concerns.

---

## 9. CI/CD with Security & Compliance

### 📄 GitHub Actions

```yaml
name: CI/CD with Security
on:
  push:
    branches: [main]
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Snyk Scan
        run: snyk test

      - name: SonarQube Analysis
        run: sonar-scanner

      - name: Deploy
        run: kubectl apply -f k8s/deployment.yaml
```

---

## 10. Canary and Blue-Green Deployments

### 📄 GitHub Actions for Canary

```yaml
name: Canary Deployment
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Deploy to Canary
        run: kubectl apply -f k8s/canary-deployment.yaml

      - name: Monitor & Promote
        run: |
          kubectl rollout status deployment/myapp-canary
          if [ $? -eq 0 ]; then
            kubectl apply -f k8s/production-deployment.yaml
```

---

> 🔐 **Key Concepts Covered:**

* CI/CD Pipelines with Docker, Kubernetes, Jenkins, GitHub Actions
* Serverless & GitOps Deployments
* Infrastructure as Code with Terraform
* Multistage Docker Builds
* Security, Compliance, and Rollback Strategies
* Canary & Blue-Green Deployments

Let me know if you want all examples in separate files or explained as part of a specific stack!

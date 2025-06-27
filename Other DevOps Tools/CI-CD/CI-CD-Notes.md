# 🚀 CI/CD Interview Cheat Sheet & Real-world Scenarios

## 📘 1. What is Continuous Integration (CI)?

* CI is a practice where developers frequently integrate code into a shared repository.
* Each integration is verified with automated builds and tests.

### ✅ Benefits:

* Early bug detection
* Faster development cycles
* Better collaboration and code quality

---

## 📘 2. What is Continuous Delivery (CD) vs Continuous Deployment?

* **Continuous Delivery**: Keeps the app in a deployable state. Manual approval for production deployment.
* **Continuous Deployment**: Automates deployment to production after passing tests.

### 🔁 Key Difference:

* Delivery = Manual push to production
* Deployment = Automated push to production

---

## 📘 3. What is the Purpose of a CI/CD Pipeline?

* Automates building, testing, and deployment.

### ✅ Goals:

* Reduce manual effort
* Ensure quality via automated testing
* Faster and reliable delivery
* Minimal downtime and rollback support

---

## ⚠️ 4. Handling CI/CD Failures

* Use **automated rollback**
* Configure **Slack/email notifications**
* Enable **manual approval gates**
* Apply strategies like retries or Blue/Green/Canary deployment

---

## 🛠️ 5. Typical CI/CD Pipeline Steps

1. **Code Commit**
2. **Build**
3. **Test** (Unit + Integration)
4. **Static Code Analysis** (SonarQube etc.)
5. **Staging Deployment**
6. **Manual Approval**
7. **Production Deployment**
8. **Post-Deployment Checks**

---

## 🔧 6. Tools for CI/CD Pipelines

* Jenkins
* GitHub Actions
* GitLab CI
* CircleCI
* Travis CI
* Bamboo
* ArgoCD (GitOps)
* Spinnaker

---

## 📦 7. Docker in CI/CD

* Ensures consistent environments
* Enables isolated, portable deployments
* Supports parallel testing
* Simplifies deployment with containers

---

## 🔒 8. Versioning the Pipeline Itself

* Store Jenkinsfile / YAML files in Git
* Use Terraform/Ansible for infrastructure as code
* Version control all scripts and build logic

---

## 🌍 9. Multi-Environment Deployment

* Use environment variables/configs for Dev, Test, Prod
* Include approval gates
* Apply Infra-as-Code (Terraform, Helm)

---

## 🔐 10. CI/CD Security Best Practices

* Secrets mgmt: Vault, AWS Secrets Manager
* Static & dynamic security tests (SAST/DAST)
* Role-based access control
* Enable audit logging and approvals

---

## 🧾 11. Pipeline as Code

* Define pipelines in versioned code (e.g. Jenkinsfile, .gitlab-ci.yml)
* Enables reproducibility, versioning, collaboration

---

## 📈 12. Role of Continuous Monitoring

* Use tools like Prometheus, Grafana, Datadog
* Monitor deployments, performance, uptime
* Detect regressions early

---

# 🔎 Real-World CI/CD Troubleshooting Scenarios

## 1. ❌ Application Crash After Deployment

* Check logs (app, infra, container)
* Check CPU, RAM usage (Prometheus/Grafana)
* Rollback to previous version if needed
* Verify configs and dependencies

---

## 2. 🐢 High Latency in Production

* Check app logs for slow code paths
* Monitor CPU/mem/network/disk
* Analyze DB query performance
* Check load balancer and DNS
* Scale horizontally or vertically if needed

---

## 3. 🔥 Service Downtime Due to Resource Exhaustion

* Monitor metrics (memory, CPU)
* Check logs for OOM errors
* Adjust Kubernetes resource limits or VM size
* Optimize app code and DB queries

---

## 4. 🚀 Zero Downtime Deployments

* Use Blue/Green, Canary, or Rolling deployment strategies
* Ensure load balancers handle traffic split
* Apply backward-compatible DB migrations

---

## 5. 🧨 Service Crash After DB Upgrade

* Check DB and app logs
* Confirm schema compatibility
* Validate DB connection strings
* Revert DB version if needed
* Reproduce in staging

---

## 6. 🌐 Intermittent Network Issues

* Check load balancer/firewall logs
* Monitor service-to-service communication
* Use ping/traceroute/netstat for debugging
* Add retry logic and timeout configurations

---

## 7. 🧠 Memory Leak in Production

* Use profiling tools (JProfiler, memory dump)
* Track usage via Prometheus
* Analyze GC logs and heap dumps
* Patch and redeploy with optimized memory management

---

## 8. 🔒 Database Locking Issues

* Analyze DB logs and slow queries
* Use `SHOW PROCESSLIST` (MySQL) or `pg_stat_activity` (Postgres)
* Tune isolation levels
* Apply indexing and query optimization
* Handle deadlocks in code

---

> 💡 This cheat sheet is ideal for interview prep and real-world DevOps scenarios. Want the next one on Jenkins or Kubernetes?

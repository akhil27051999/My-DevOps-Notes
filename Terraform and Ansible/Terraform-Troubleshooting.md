# 🚨 Terraform Troubleshooting and Recovery Guide

## 🔧 1. Terraform State Corruption

* **Restore from Backup**: Use S3 versioning or local `.tfstate.backup`.
* **Repair State**: Use `terraform state list`, `rm`, or `mv`.
* **Manual Edits**: Open `.tfstate` cautiously (last resort).
* **Re-import**: Use `terraform import` to reconstruct state.

---

## ⚠️ 2. Error: Invalid Resource Type

* **Typo**: e.g., `aws_instace` vs `aws_instance`.
* **Missing Provider Block**: Define and `terraform init`.
* **Version Mismatch**: Check `required_providers` block.

---

## 📉 3. terraform apply Fails

* **Analyze Output**: Error message often points to issue.
* **Run Plan**: `terraform plan` for pre-validation.
* **Validation**: `terraform validate` for syntax.
* **Debug**: Use `TF_LOG=DEBUG`.

---

## ♻️ 4. Resource Recreation (Unexpected)

* **Drift**: Manual infra changes.
* **Immutable Field Change**: e.g., `ami`, `subnet_id`.
* **Lost State**: Reinitialize or re-import.
* **Provider Behavior**: Check resource schema.

---

## 🕓 5. Stuck in Planning

* **Slow APIs**: AWS/GCP slowness.
* **Bad Credentials**: Misconfigured providers.
* **Use Logs**: `TF_LOG=DEBUG` for bottlenecks.

---

## 🔄 6. No Change Detected

* **Run `terraform refresh`**.
* **Lock Conflicts**: Shared usage without remote state.
* **Re-import** if needed.

---

## 🧩 7. tfvars Changes Ignored

* **Load Manually**: `-var-file="dev.tfvars"`
* **Check for Overrides**: CLI or config block values.

---

## 🔗 8. Broken Modules

* **Source Path**: Correct local or Git URL.
* **Input/Output Mismatches**: Check usage in `main.tf`.

---

## ⏱️ 9. Timeout waiting for resource state

* **Check Cloud Console**: Is resource stuck?
* **Add timeouts** block.
* **Retry apply** after verification.

---

## 📤 10. Missing Outputs

* **Syntax**: `value = correct_reference`
* **Check `terraform output`**
* **Run `terraform refresh`**

---

## 🔐 11. State File Lost/Corrupted

* **Restore from Backup**
* **Avoid Manual Edits**
* **Use Remote State + Locking**

---

## 🚧 12. Unexpected Resource Replacement

* **Immutable Fields**: Detect and isolate changes.
* **Lifecycle**: Use `prevent_destroy`, `create_before_destroy`.

---

## 🌀 13. Drift from Real Infra

* **Run `terraform plan` regularly**
* **Avoid Console Changes**
* **Use `terraform refresh`**

---

## 🔒 14. State Lock Timeout

* **Use `terraform force-unlock <LOCK_ID>`**
* **Manually delete lock in DynamoDB** (caution).

---

## 🕵️ 15. Secrets in State or Plan

* **Use `sensitive = true`**
* **Integrate Secrets Manager/Vault**

---

## 🕰️ 16. terraform apply Timeout

* **Long-Running Resources**: Add timeouts.
* **Split Modules**: For better control.

---

## ❗ 17. Resource Already Exists

* **Import It**: `terraform import resource.name id`
* **Avoid Static Names**: Use `random_id` for uniqueness.

---

## ⛓️ 18. Module Version Breaks

* **Pin Version**: Use `?ref=tag` or SHA.
* **Maintain Forks** of critical modules.

---

## 🧬 19. Parallel Execution Conflict

* **Enable Locking**: With S3 + DynamoDB.
* **Use Workspaces**: For team isolation.

---

## 🚫 20. AWS Limits Exceeded

* **Read Error**: e.g., `Too many ENIs`.
* **Raise Quotas** in AWS Console.
* **Add Pre-checks** or validation rules.

---

## ☢️ 21. terraform destroy in Production

* **Use RBAC and IAM**
* **`prevent_destroy`** in sensitive modules
* **Secure state backend**

---

## 🌐 22. Env Variable Misuse

* **Use `.auto.tfvars` or separate directories**
* **Avoid hardcoding**

---

## 🧳 23. Cloned Repo Missing Modules

* **Run `terraform init` again**
* **Use full module sources** (Git, Registry)

---

## 🔐 24. Provider Authentication Issues

* **Verify AWS credentials**
* **Run `aws sts get-caller-identity`**

---

## ⚙️ 25. Breaking Changes after Upgrade

* **Pin Versions**: In `terraform` block
* **Test in Staging**
* **Check upgrade notes**

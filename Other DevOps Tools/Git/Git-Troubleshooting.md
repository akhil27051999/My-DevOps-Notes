# 🛠️ Git Troubleshooting Scenarios & Solutions

## 1. Accidentally Committed Sensitive Information

### 🔍 Problem

You committed sensitive files (e.g., `.env`, secrets) to Git and pushed them.

### ✅ Solution

**Remove the file from the entire Git history:**

```bash
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch path/to/sensitive-file" \
  --prune-empty --tag-name-filter cat -- --all
```

**Or using `git filter-repo` (recommended):**

```bash
git filter-repo --path path/to/sensitive-file --invert-paths
```

**Force push to rewrite history:**

```bash
git push origin --force --all
git push origin --force --tags
```

> ⚠️ Inform all collaborators to re-clone the repo.

---

## 2. Merge Conflicts After Branch Merge

### 🔍 Problem

You merged a branch and encountered file conflicts.

### ✅ Solution

```bash
git status              # See conflicted files
```

Edit each conflicted file manually and remove conflict markers `<<<<<<<`, `=======`, `>>>>>>>`.

```bash
git add <file>          # Mark as resolved
git commit              # Complete the merge
```

---

## 3. Accidentally Pushed to the Wrong Branch

### 🔍 Problem

Changes were pushed to the wrong branch.

### ✅ Solution

```bash
git checkout correct-branch

# Cherry-pick changes
git cherry-pick <commit-hash>

# Remove changes from wrong branch
git checkout wrong-branch
git reset --hard HEAD~n

# Push to remote
git push origin correct-branch
git push origin wrong-branch --force
```

---

## 4. Undoing a Commit That’s Already Pushed

### ✅ Solution

**Safe Way (creates new commit):**

```bash
git revert <commit-hash>
git push origin <branch-name>
```

**Destructive Way (rewrite history):**

```bash
git reset --hard <commit-hash>
git push origin <branch-name> --force
```

---

## 5. Local Repo Out of Sync with Remote

### ✅ Solution

```bash
git fetch
git status

# If behind, pull changes
git pull origin <branch-name>

# Resolve conflicts and push
# (see conflict resolution section)
git push origin <branch-name>
```

---

## 6. Handling Large Binary Files

### ✅ Solution

Use **Git LFS (Large File Storage)**:

```bash
git lfs install
git lfs track "*.psd"      # or other file type

# Commit and push
git add .gitattributes
git add <large-file>
git commit -m "Add large file"
git push origin <branch-name>
```

> Everyone must have Git LFS installed.

---

## 7. Error: `fatal: refusing to merge unrelated histories`

### ✅ Solution

```bash
git merge <branch-name> --allow-unrelated-histories
```

> Used when merging unrelated repositories or new roots.

---

## 8. Merge Conflicts During `git pull`

### ✅ Solution

```bash
git status                # Identify conflicted files

# Open and resolve conflicts manually

# Mark resolved
git add <file-name>

# Finalize merge
git commit
```

---

## 9. Undo Last Git Push

### ✅ Solution

```bash
git reset --hard HEAD~1
# ⚠️ This removes last commit

git push origin <branch-name> --force
```

---

## 10. Error: Non-fast-forward Push

### ✅ Solution

```bash
git fetch origin

# Merge changes
git merge origin/<branch-name>

# Then push
git push origin <branch-name>
```

---

## 11. Recover Deleted Branch

### ✅ Solution

```bash
git reflog                       # Get commit hash of deleted branch

# Recover branch
git checkout -b <branch-name> <commit-hash>

git push origin <branch-name>
```

---

> 💡 These Git troubleshooting scenarios prepare you for real-world DevOps and development challenges.

Let me know if you want similar cheat sheets for GitHub Actions, Jenkins, Docker, Kubernetes, etc.

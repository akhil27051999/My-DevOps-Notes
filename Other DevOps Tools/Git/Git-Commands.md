# 📘 Git Commands Complete Notes & Cheat Sheet

## 📦 1. Git Configuration

```bash
git config --global user.name "Your Name"      # Set your Git username
git config --global user.email "your@example.com"  # Set your Git email

# Set default editor
git config --global core.editor nano

# View configuration
git config --list

# Create aliases
git config --global alias.co checkout
```

---

## 🗂️ 2. Repository Initialization

```bash
git init                     # Initialize new repo
git clone <repo_url>         # Clone an existing repo
```

---

## 📄 3. Basic Snapshot Commands

```bash
git status                   # Check status of files
git add file                 # Stage a specific file
git add .                    # Stage all files
git commit -m "message"      # Commit with a message
git commit -am "message"     # Add & commit tracked files
```

---

## 🔍 4. Viewing Changes

```bash
git diff                     # Show unstaged changes
git diff --staged            # Show staged vs last commit
git log                      # View full commit history
git log --oneline            # Compact commit history
git show <commit_id>         # View details of a commit
```

---

## 🔄 5. Branching & Merging

```bash
git branch                   # List branches
git branch <name>            # Create a new branch
git checkout <branch>        # Switch branch
git checkout -b <name>       # Create & switch

git merge <branch>           # Merge another branch

git branch -d <name>         # Delete merged branch
git branch -D <name>         # Force delete unmerged
```

---

## 🧲 6. Remote Repositories

```bash
git remote -v                # View remotes
git remote add origin <url>  # Add new remote

git push -u origin main      # Push & track main branch
git push                     # Push changes
git pull                     # Pull changes
git fetch                    # Fetch changes without merge
```

---

## 🧪 7. Stashing Changes

```bash
git stash                    # Stash changes
git stash list               # List stashes
git stash apply              # Apply latest stash
git stash pop                # Apply & remove latest
```

---

## 🗑️ 8. Undoing Changes

```bash
git checkout -- file         # Discard changes
git reset file               # Unstage file
git reset --soft HEAD~1      # Undo commit, keep staged
git reset --mixed HEAD~1     # Undo commit, keep changes
git reset --hard HEAD~1      # Undo commit & changes
git revert <commit>          # Create new commit to undo
```

---

## 📊 9. Tagging

```bash
git tag                      # List tags
git tag v1.0                 # Create lightweight tag
git tag -a v1.0 -m "Version" # Annotated tag
git push origin v1.0         # Push tag
```

---

## 🛠️ 10. Git Tools & Cleanup

```bash
git clean -n                 # Preview clean
git clean -f                 # Remove untracked files
git fsck                     # Verify repo integrity
git gc                       # Garbage collection
```

---

## 👥 11. Collaboration & Contribution

```bash
git pull origin main         # Pull from main branch
git push origin <branch>     # Push branch to remote
git rebase <branch>          # Reapply commits on base
git cherry-pick <commit>     # Apply specific commit
```

---

## 📝 12. Git Ignore & Attributes

* `.gitignore` – Exclude files from tracking
* `.gitattributes` – Define file treatment (e.g., diff, merge rules)

```bash
# .gitignore example
node_modules/
*.log
.env

# .gitattributes example
*.sh text eol=lf
*.jpg binary
```

---

## 📚 Additional Tips

* Use `git reflog` to recover lost commits.
* Combine commands with aliases to save time.
* Regularly `pull`, `commit`, and `push` for sync.

---

✅ Now you’re ready to master Git with confidence!

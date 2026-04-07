# 🧱 Git Fundamentals & Workflow (Deep Dive)

This section explains **core Git concepts, commands, and real-time usage** with practical examples.

---

# 🧠 Stages of Git (Core Concept)

```text
Working Directory → Staging Area → Local Repository → Remote Repository
     (edit)            (add)            (commit)            (push)
```

### 📌 Explanation

| Stage                | Description                              |
| -------------------- | ---------------------------------------- |
| 📝 Working Directory | Where you write/edit code                |
| 📦 Staging Area      | Where changes are prepared (`git add`)   |
| 🗂 Local Repository  | Stored in `.git` folder (commit history) |
| ☁️ Remote Repository | GitHub / remote storage                  |

---

# ⚙️ Setup Git Environment (RHEL / Linux)

```bash
sudo -s
mkdir gitproject
cd gitproject

yum install git -y
git --version
```

---

# 🚀 Initialize Repository

```bash
git init
```

👉 Creates `.git` directory (stores history + metadata)

```bash
git status
```

---

# 📂 First File Workflow

```bash
touch index.html
vi index.html
```

```bash
git status
```

🔴 Untracked → not added yet

```bash
git add index.html
```

🟢 Tracked (staged)

```bash
git commit -m "my first commit"
```

---

# 🧩 Git Flow Diagram

```text
index.html
   ↓
Working Directory
   ↓ git add
Staging Area
   ↓ git commit
Local Repository (.git)
```

---

# 📄 Multiple File Commits

```bash
touch hello.txt
git add hello.txt
git commit -m "second commit"

touch test.txt
git add test.txt
git commit -m "third commit"
```

---

# 📌 File Modes in Git

```text
100644 → Normal file
100755 → Executable file
```

---

# 📜 Git Logs & History

```bash
git log
git log --oneline
git log --oneline -2
git log -p -2
git log --stat
```

### Custom Format

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

---

# 🔍 Inspect Changes

```bash
git show
git show <commit-id>
```

---

# 🧾 Git Blame (Line Tracking)

```bash
git blame index.html
```

👉 Shows who changed each line

---

# 🔄 Git Diff (Compare Changes)

### Working vs Staging

```bash
git diff
```

### Staging vs Repository

```bash
git diff --staged
```

### Working vs Last Commit

```bash
git diff HEAD
```

### Between Commits

```bash
git diff <commit1>..<commit2>
```

---

# 🧩 Diff Visual

```text
Working Dir ≠ Staging → git diff
Staging ≠ Repo       → git diff --staged
Working ≠ Repo       → git diff HEAD
```

---

# 👤 Git User Configuration

```bash
git config user.name "your-name"
git config user.email "your-email"
```

Check:

```bash
git config --list
```

Global config:

```bash
git config --global --edit
```

---

# 🔍 Filter Logs by Author

```bash
git log --author="User"
```

---

# 📦 Add Multiple Files

```bash
touch python{1..5}
git add .
git commit -m "multiple files"
```

---

# 🧠 Important Observations

* `.git` folder stores **entire history**
* `git add` = move to staging
* `git commit` = save snapshot
* `git status` = current state
* `git diff` = compare changes

---

# 🎯 Summary

```text
git init      → initialize repo
git add       → stage changes
git commit    → save snapshot
git log       → view history
git diff      → compare changes
git blame     → track line changes
```

---

# ⭐ Pro Tips

* Always check `git status` before commit
* Use `git diff` to avoid mistakes
* Configure username before committing
* Keep commits small and meaningful

---

---
# 🚀 Git Learning Notes (Hands-on + Visual Guide)

Welcome to my **Git Practical Learning Repository** 📘
This guide includes real-world Git commands with **clear explanations and diagrams**.

---

# 🧠 Git Basics (How Git Works)

```text
Working Directory  →  Staging Area  →  Repository
     (edit)            (git add)         (commit)
```

---

# 📂 1. Basic Workflow

```bash
vi index.html
git add index.html
git commit -m "1st commit"
```

👉 Repeat changes and commits multiple times to build history.

---

# ✏️ 2. Git Amend (Modify Last Commit)

```bash
git commit --amend -m "updated message"
```

### 🧩 Diagram

```text
Before:
A → B → C (HEAD)

After:
A → B → C' (HEAD)
```

---

# 🔁 3. Git Rebase (Modify Multiple Commits)

```bash
git rebase -i HEAD~3
```

* Opens interactive mode
* Replace `pick` with `reword`
* Modify commit messages

### 🧩 Diagram

```text
Before:
A → B → C → D (HEAD)

After:
A → B' → C' → D' (HEAD)
```

---

# 🧩 4. Squashing Commits

```bash
git rebase -i HEAD~3
```

### 🧩 Before

```text
A → B → C → D (HEAD)
```

### 🧩 After (Squash)

```text
A → B → D' (HEAD)
```

👉 Multiple commits → One clean commit

---

# ⚠️ 5. Git Reset (Move HEAD)

## Soft Reset

```bash
git reset --soft HEAD^
```

```text
A → B → C (HEAD)

After:
A → B (HEAD)
Changes still in staging
```

---

## Hard Reset

```bash
git reset --hard HEAD^
```

```text
A → B → C (HEAD)

After:
A → B (HEAD)
Changes ❌ deleted
```

---

# 🔄 6. Git Checkout (Restore Files)

```bash
git show <commit-id>:index.html
git checkout <commit-id> -- index.html
```

Restore all files:

```bash
git checkout <commit-id> -- *
```

Return to latest:

```bash
git checkout master -- index.html
```

---

# 🆕 7. Git Restore (Modern Alternative)

## Undo local changes

```bash
git restore file.txt
```

## Unstage file

```bash
git restore --staged file.txt
```

OR

```bash
git rm --cached file.txt
```

---

# 📊 Restore vs Reset

| Feature         | git restore           | git reset |
| --------------- | --------------------- | --------- |
| Scope           | Working dir / staging | Full repo |
| Affects history | ❌ No                  | ✅ Yes     |
| Use case        | Undo changes          | Move HEAD |
| Safety          | Safe                  | Risky     |

---

# 🧠 8. HEAD Explained

```text
HEAD → current branch → latest commit
```

### Example

```text
HEAD → master → A → B → C
```

### Detached HEAD

```text
HEAD → C
master → B
```

---

# 📦 9. Git Stash (Temporary Work Save)

## Flow Diagram

```text
Working Directory
     ↓
 git stash
     ↓
[ Saved in stash ]
     ↓
Working Directory Clean
```

---

## 🧪 Real Scenario

### Step 1: Work on Story1

```bash
vi story1
git add story1
git stash
```

---

### Step 2: Work on Story2

```bash
vi story2
git add story2
git commit -m "story2"
```

---

### Step 3: Restore Story1

```bash
git stash apply
```

---

## 📋 Useful Commands

```bash
git stash list
git stash apply
git stash clear
```

---

## Stash Specific Files

```bash
git stash push -m "message" -- story1 story2
```

---

# 🧹 10. Cleanup Repo

```bash
rm -rf *
git add .
git commit -m "clean"
```

---

# 🎯 Summary Cheat Sheet

```text
git add        → stage changes
git commit     → save changes
git amend      → fix last commit
git rebase     → edit history
git reset      → move HEAD
git restore    → undo changes
git stash      → temporary save
```

---

# ⭐ Pro Tips

* ✅ Use `git restore` instead of checkout
* ⚠️ Avoid `git reset --hard` unless sure
* 🧠 Understand HEAD before using rebase
* 🚀 Keep commit history clean using squash

---

# 🧑‍💻 Author

**Git Practice & Learning Notes**
Built for DevOps & Interview Preparation 🚀

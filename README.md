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

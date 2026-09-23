# Merge_Conflict_Git

A simple Git demo project that walks through **branches**, **commits**, and **merge conflict resolution** using a single Python file (`app.py`).

- **Remote URL:** `git@github.com:rajgenai4u/Merge_Conflict_Git.git`
- **Default branch:** `main`
- **Purpose:** Learn how merge conflicts happen when two branches edit the same lines, and how to resolve them.

---

## 1. Project Overview

This project contains a minimal Python application that prints a welcome message. It was used to simulate two developers (Terminal A and Terminal B) working on the same file at the same time, producing a real merge conflict that was then fixed manually.

## 2. Project Structure

```
merge-conflict-demo/
├── .git/        # Git repository metadata
├── app.py       # Main Python application
└── README.md    # This documentation
```

## 3. Project Documentation

### app.py

Final version on `main` (after resolving the conflict):

```python
def welcome():
    print("Welcome to the Terminal A &  B")

if __name__ == "__main__":
    welcome()
```

To run:

```bash
python3 app.py
```

**Output:** `Welcome to the Terminal A &  B`

---

## 4. Branches

| Branch       | Points at | Description                                              |
|--------------|-----------|----------------------------------------------------------|
| `main`       | `c3bb65a` | Main line of development; contains the merged result.    |
| `feature-a`  | `c19fb4a` | Simulates work from Terminal A.                          |
| `feature-b`  | `dda319d` | Simulates work from Terminal B; caused the conflict.     |

Branch graph:

```
*   c3bb65a  (main)  Resolve merge conflict between main and feature-b
|\
| * dda319d  (feature-b)  updated app.py in feature-b
* | c19fb4a  (feature-a)  file added in feature-a
|/
* af4035d  Initial commit on main
```

---

## 5. Commits

| Commit     | Branch    | Date (2026-09-23) | Message                                       |
|------------|-----------|-------------------|-----------------------------------------------|
| `af4035d`  | main      | 18:56             | Initial commit on main                        |
| `c19fb4a`  | feature-a | 19:07             | file added in feature-a                       |
| `dda319d`  | feature-b | 19:10             | updated app.py in feature-b                   |
| `c3bb65a`  | main      | 19:20             | Resolve merge conflict between main and feature-b |

Author: **Karre Rajesh** `<rajsai4us@gmail.com>`

### What changed on each branch

- **main (`af4035d`):** Created `app.py` printing `Welcome to the application!`
- **feature-a (`c19fb4a`):** Changed the print message to `Update welcome message in feature-b`
- **feature-b (`dda319d`):** Changed the same print message to `Welcome to the Terminal B`
- **main (`c3bb65a`):** Merged both branches and resolved the conflict to `Welcome to the Terminal A & B`

---

## 6. Complete Git Command History

### Step 1: Initialize the repository

```bash
mkdir merge-conflict-demo
cd merge-conflict-demo
git init
```

### Step 2: Create the app and initial commit

```bash
# (write app.py with a welcome() function)
git add app.py
git commit -m "Initial commit on main"          # commit af4035d
```

### Step 3: Link the remote repository

```bash
git remote add origin git@github.com:rajgenai4u/Merge_Conflict_Git.git
```

### Step 4: Create and work on feature-a (Terminal A)

```bash
git checkout -b feature-a                       # branch from main
# (edit app.py: change the print message)
git add app.py
git commit -m "file added in feature-a"         # commit c19fb4a
```

### Step 5: Create and work on feature-b (Terminal B)

```bash
git checkout main                               # go back to main
git checkout -b feature-b                       # branch from main
# (edit app.py: change the SAME print message)
git add app.py
git commit -m "updated app.py in feature-b"     # commit dda319d
```

### Step 6: Merge feature-a into main (fast-forward)

```bash
git checkout main
git merge feature-a                             # fast-forward to c19fb4a
```

### Step 7: Merge feature-b into main (CONFLICT!)

```bash
git merge feature-b
```

Git cannot auto-merge because both `feature-a` and `feature-b` changed the
same line in `app.py`. The file now contains conflict markers:

```txt
<<<<<<< HEAD
    print("Update welcome message in feature-b")
=======
    print("Welcome to the Terminal B")
>>>>>>> feature-b
```

### Step 8: Resolve the conflict

Edit `app.py`, choose the desired message, and remove the markers:

```python
def welcome():
    print("Welcome to the Terminal A &  B")
```

Then mark it resolved and commit:

```bash
git add app.py
git commit -m "Resolve merge conflict between main and feature-b"  # commit c3bb65a
```

### Step 9: Push everything to GitHub

```bash
git push origin main
git push origin feature-a
git push origin feature-b
```

---

## 7. Useful Commands Used Along the Way

```bash
# Inspect branches
git branch
git branch -a

# View history
git log --oneline --graph --all
git log --oneline --all --decorate

# Check the working tree
git status
```

---

## 8. Key Takeaway

Merge conflicts are normal in Git. They happen when two branches modify the
same lines of the same file. The fix is to **manually resolve the conflicting
lines, `git add` the file, and finish the merge commit**.
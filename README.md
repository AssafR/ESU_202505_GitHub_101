# Git Class Exercise Guide

This document contains a complete, classroom-ready set of Git exercises
designed to be run in a terminal and IDE. It aligns with your two-part Git
presentation and introduces all core Git concepts step-by-step.

---

## Block 0 – Setup & Ground Rules (5–10 minutes)

### Verify Git and create a workspace

```bash
git --version
pwd
mkdir git_playground
cd git_playground
```

---

## Block 1 – First Local Repository: Core Workflow

```bash
mkdir hello_git
cd hello_git
git init
git status
```

Create a file:

```bash
echo "print('Hello Git')" > app.py
git status
git add app.py
git commit -m "Add hello world script"
git log --oneline
```

---

## Block 2 – Changing & Undoing Safely

Modify the file:

```bash
echo "print('Version 2')" >> app.py
git status
git diff
git add app.py
git commit -m "Append version 2 message"
git log --oneline
```

Break the file and restore it:

```bash
echo "this is not valid python" > app.py
git status
git diff
git checkout -- app.py
```

Undo a commit safely:

```bash
echo "# TODO" >> app.py
git add app.py
git commit -m "Add temp TODO"
git revert HEAD
```

---

## Block 3 – Branching & Merging

```bash
git switch -c feature-new-message
echo "print('Feature branch message')" >> app.py
git add app.py
git commit -m "Add feature branch message"

git switch main
git merge feature-new-message
git branch -d feature-new-message
```

---

## Block 4 – Working With Remotes (GitHub)

Create repo on GitHub and connect:

```bash
git remote add origin https://github.com/YOURUSER/hello-git-CLASSNAME.git
git remote -v
git push -u origin main
```

Clone it elsewhere:

```bash
cd ..
git clone https://github.com/YOURUSER/hello-git-CLASSNAME.git hello_git_clone
cd hello_git_clone
ls
```

---

## Block 5 – Fetch vs Pull (Essential Demo)

### In original repo

```bash
cd ../hello_git
echo "print('Change from A')" >> app.py
git add app.py
git commit -m "Change from A"
git push
```

### In clone repo

```bash
cd ../hello_git_clone
git fetch
git log origin/main --oneline
git pull
git log --oneline
```

---

## Block 6 – Merge Conflict (Predictable & Educational)

### Repo A

```bash
cd ../hello_git
echo "print('Change A')" > conflict_demo.py
git add conflict_demo.py
git commit -m "Add conflict from A"
git push
```

### Repo B

```bash
cd ../hello_git_clone
echo "print('Change B')" > conflict_demo.py
git add conflict_demo.py
git commit -m "Add conflict from B"
git push     # fails
git pull     # conflict
```

Resolve conflict manually and commit:

```bash
git add conflict_demo.py
git commit -m "Resolve merge conflict"
git push
```

---

## Block 7 – AI-Focused Exercise: Config Versioning & Experiment Tracking

```bash
cd ../git_playground
mkdir ml_experiments
cd ml_experiments
git init
```

Create baseline config:

```bash
cat > config.yaml << 'EOF'
model: "baseline-mlp"
learning_rate: 0.001
batch_size: 32
epochs: 10
EOF

git add config.yaml
git commit -m "Add baseline training config"
```

Experiment on a branch:

```bash
git switch -c exp-lr-1e-4
# edit config.yaml manually or via sed
git add config.yaml
git commit -m "Lower learning rate for experiment"
git tag best-lr-1e-4
git switch main
```

---

## Block 8 – Confidence Checklist

By the end of this lab, students should be able to:

- Create repositories with `git init`
- Track files using:
  - `git status`
  - `git add`
  - `git commit`
  - `git log`
- Restore files with `git checkout -- <file>`
- Safely undo with `git revert`
- Create and merge branches  
- Connect to a remote repo
- Push, pull, and fetch updates
- Resolve merge conflicts
- Track ML experiments and configs with tags and branches

---

Happy coding!

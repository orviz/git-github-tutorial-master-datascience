# 01 - Git Basics

This tutorial is based on ["Pro Git"](https://git-scm.com/book/en/v2) by Scott Chacon (2nd edition, 2014).


## 010 - Git Configuration

* Three Git configuration files on your system (from *lowest to highest priority*):
    - System's `/etc/gitconfig`
    - User space: `$HOME/.gitconfig` or `$HOME/.config/git/config`
    - Repository level: `.git/config` within your repository

* `git config` command let you *modify the files above through options*:
    - With `--system` option, reads/writes from `/etc/gitconfig`
    - With `--global` option, reads/writes from user space, aka `$HOME/.gitconfig`
    - With `--local` option, reads/writes from current repository, aka `.git/config`

* `git config --list` shows your current Git configuration.

### First-time Setup

**Step 1: Identify Yourself**

Git needs to know who is making the changes. Run these commands:

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "your-email@example.com"
```

**Step 2: Set the Default Editor**

We will use `nano` editor in the terminal (use `vim` only if you are familiar with it):

```bash
$ git config --global core.editor nano
```

**Step 3: Set the Default Branch**

* *Branching* is more advanced topic that we will cover in a dedicated section of this tutorial
* Curious fact: in 2020, GitHub moved default branch term from `master` to `main` 
    * Reasoning: https://sfconservancy.org/news/2020/jun/23/gitbranchname/
    * Versions lower to Git 3.0 still use `master` for default naming:
        ```bash
        hint: Using 'master' as the name for the initial branch. This default branch name
        hint: will change to "main" in Git 3.0. To configure the initial branch name
        hint: to use in all of your new repositories, which will suppress this warning,
        hint: call:
        hint:
        hint:   git config --global init.defaultBranch <name>
        hint:
        hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
        hint: 'development'. The just-created branch can be renamed via this command:
        hint:
        hint:   git branch -m <name>
        hint:
        hint: Disable this message with "git config set advice.defaultBranchName false"
        ```


Ensure that `main` is always being used as the default branch name:

```bash
$ git config --global init.defaultBranch main
```

## 011: Repository Creation

### Step 1: Initialize a New Repository: `git init`

In practical terms, a repository in Git is represented by a folder in your file system. Create a fresh folder (`mkdir` shell command) for the tutorial and initialize Git:

```bash
$ mkdir git-practice

# Be sure to 'cd' into the repository folder
$ cd git-practice
$ git init
```

**The importance of `git status` to understand each Git operation**

`git status` is an informative command that shall be used anytime we feel we need more information about what's happening within our Git Workflow:

```bash
$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Although still working with an empty repository, we gather important pieces of information:
- *Our current branch name*: this should be `main` if the Git Setup steps above (done through `git config`) have been followed.
- *Status of the files within the repository*: i.e. commits done or to-be-done, tracked/untracked files, ...
- *Hints on how to proceed*: next steps that are often done at the point where the current status is.

### Step 2: Create a File

```bash
# Note: we use the overwriting sign '>'
$ echo "# My Learning Journey" > README.md

$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

**What the status information tells us:**
- `README.md` is untracked (under Untracked files)
- `README.md` was not in the previous snapshot (commit)
- *Hint*: `use "git add" to track`

### Step 3: Start Tracking the File: `git add`

`git add` marks the changes to the file to be added in the next commit. It does it by moving the change to the *Staging Area*:

```bash
$ git add README.md

$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

**What the status information tells us:**
- `README.md` is now staged (under *"Changes to be committed"*)
- *Hint*: the Git command to restore the `add` command (move the staged change back to untracked)

### Step 4: Commit the changes: `git commit`

Considerations about the `git commit` command:
- **Marks the registry of a new *version***, adding the changes that currently exist in the *Staging Area*.
    - Versions can be compared, reverted, etc.
- A **commit implies 1-or-more modifications to 1-or-more files**.
    - Modifications *shall be related, atomic and topical*
    > “A commit should contain related changes and nothing but related changes” (codefoster.com)
- The **commit message shall be descriptive in the long term**: critical to know its purpose at a glance.

```bash
# Shortcut to provide a commit message through `-m` option
$ git commit -m "Initial commit: add README"
[main (root-commit) bbbaa9f] Initial commit: add README
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

$ git status
On branch main
nothing to commit, working tree clean
```

**What the commit information tells us:**
- The identifier of the commit (`bbbaa9f`) and the branch (`main`) where it has been done.
- Number of insertions (lines), how many files changed, and file permisions.

**What the status information tells us:**
- Our working directory is free of untracked or staged changes: `"nothing to commit"`

## 012: Understanding the Staging Lifecycle

![Esquema de la base de datos](images/staging_lifecycle.png)

**The Status of Files**
- Untracked: git does not know about these files
- Tracked: git knows about
    - Unmodified
    - Modified
    - Staged

**The Git Workflow**
1. Edit files &rarr; Modified
2. Stage the required files (`git add`) &rarr; Staged
3. Commit them (`git commit`) &rarr; Unmodified

### Claryfing sample of Git Staging Operation

1. Let's modify again the previous `README.md` file:

```bash
$ echo "Fix #1 added -- You can safely remove this line --" >> README.md

$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

**What the status information tells us:**
- `README.md` is *unstaged* (under *"Changes not staged for commit"*) &rarr; *modified* in the working directory but not *staged*.

2. Add the modification to the Staging Area with `git add`:

```bash
$ git add README.md

$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
```

**What the status information tells us:**
- `README.md` is staged and will go into the next commit

3. ..but before the commit, you've just realized that a last minute change is required..

```bash
$ echo "Fix #2: Very important fix added -- You can safely remove this line --" >> README.md

$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md
```

**What the status information tells us:**
- *`README.md` is staged and unstaged at the same time!?* &rarr; **Git works with insertions/lines added/removed in files, not with the files themselves**

**At this point..**:
- If you commit now, only the first change in `README.md` (“Fix #1..”) will go through.
- You need to `git add` + `git commit` again to stage the last modification.
```bash
$ git add README.md

$ git status
On branch main
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
    modified:   README.md

$ git commit -m "fix: unnecessary messages added to the README.md file"
```
# 04 - Git Advanced

In this chapter we will review:
* [040 - Fork Maintenance](#040---fork-maintenance)
* [041 - Complex Git Flows](#041---complex-git-flows)
* [042 - Ignoring Files](#042---ignoring-files)
* [043 - Time Travel: Rewriting the Past](#043---time-travel)

## 040 - Fork Maintenance

When you fork a repository, you create a **snapshot of that project at that exact moment in time**.
- However, open-source projects and team repositories move fast, **your fork on GitHub and your local machine will fall behind**. 

To fix this, you must configure your local Git CLI to track the original repository.

### The Concept: `origin` vs. `upstream`

In a forking workflow, your local machine needs to talk to **two different remote servers**:
1. **`origin`**: Your personal fork on GitHub (You have read & write access).
2. **`upstream`**: The original repository you forked from (You have read-only access).


```text
 ┌────────────────────────────────────────────────────────┐
 │              Original Repository (upstream)            │
 └───────────────────────────┬────────────────────────────┘
                             │ (Fork via Web)
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │               Your Personal Fork (origin)              │
 └───────────────────────────▲────────────────────────────┘
               (Push changes)│ │ (Clone & Pull)
                             │ ▼
 ┌────────────────────────────────────────────────────────┐
 │                 Your Local Machine (CLI)               │
 └────────────────────────────────────────────────────────┘
```

### Step 1: Link the Upstream Project to your Local Copy
Open your terminal inside your cloned repository. Let's check your current remote connections:
```bash
git remote -v
```
*You will only see your own fork listed as `origin`.*

Now, copy the HTTPS URL of the **upstream repository** and add it as your `upstream` remote:

```bash
git remote add upstream <PASTE-ORIGINAL-REPOSITORY-URL-HERE>
```

Verify it again with `git remote -v`. You should now see both `origin` and `upstream`.

---

### Step 2: Fetch and Merge the Upstream Changes
Whenever you want to update your computer with the latest changes made in the Upstream repo, run this sequence in your terminal:

1. **Switch to your local main branch:**
   ```bash
   git checkout main
   ```
2. **Download all metadata from the original project:**
   ```bash
   git fetch upstream
   ```
3. **Merge the original changes into your local main branch:**
   ```bash
   git merge upstream/main
   ```
   *(Since you haven't touched your local main branch, this will usually be a clean, fast-forward merge).*

---

### Step 3: Update Your Fork on GitHub
Right now, your local machine is perfectly updated, but your fork on GitHub (`origin`) is still old. Let's push the fresh code back to your personal GitHub page:

```bash
git push origin main
```

Now, if you visit your GitHub fork page in the browser, it will proudly say: *"This branch is up to date with [original-owner]/main"*. You are ready to start a new feature!

---

## 041 - Complex Git Flows

GitHub Flow is intentionally easy to implement, which GitHub developers use themselves. However, large projects may require more complex approaches, such as *Git Flow*:

![GitHub Flow](images/github_flow.png)

---

## 042 - Ignoring Files

When you run `git status`, Git tracks every single change in your folder. However, **certain files might never uploaded** to GitHub:
*   **System junk:** Cache files (like macOS `.DS_Store` or Windows `Thumbs.db`).
*   **Dependencies:** External packages and virtual environments (like `node_modules/` or `.venv/`).
*   **Large Data:** Huge datasets (like `.csv`, `.json`, or `.sqlite` files) that slow down Git.
*   **Secrets:** Configuration files containing passwords, API keys, or credentials (like `.env`).

To tell Git to completely ignore these files, we use a special file named `.gitignore`.

### Syntax Cheat Sheet:
*   `filename.txt` &rarr; Ignores a specific file anywhere in the project.
*   `folder/` &rarr; Ignores a whole directory and everything inside it.
*   `*.csv` &rarr; The asterisk is a wildcard. This ignores *any* file ending with `.csv`.
*   `# Comment` &rarr; Lines starting with `#` are ignored by Git and used for notes.


### Step 1: Create Your `.gitignore` File

```bash
# Be sure to be placed under the repo's root path
touch .gitignore
```

*Note: The dot at the beginning is mandatory. It tells the system it is a hidden configuration file.*

### Step 2: Define Some Rules

Open the `.gitignore` file in VS Code and add the following lines:

```text
# Ignore sensitive credential files
.env

# Ignore large data CSV files
*.csv
```

### Step 3: Test It in the Terminal
Let's verify that the CLI is successfully blocking unwanted files.

1. **Create a dummy data file and a dummy secret file:**
   ```bash
   echo "1,2,3,4" > dataset.csv
   echo "PASSWORD=1234" > .env
   ```
2. **Check the status via CLI:**
   ```bash
   git status
   ```
3. **Neither `dataset.csv` nor `.env` will appear in the "Untracked files" list!** Git is completely blind to them, preventing you from accidentally staging or committing them.


---

## 043 - Time Travel

### Rewriting the Past

Earlier, we learned how to use **`git commit --amend` to fix the very last** commit, but Git is more powerful than that.

The CLI gives you a surgical tool to rewrite history interactively:

```bash
git rebase -i HEAD~3
```

*This tells Git: "I want to interactively look at the last 3 commits".*

Your terminal will open your default editor showing a list of your last 3 commits, with words like `pick` next to them.

**What can you do here?**
*   **Change `pick` to `reword`:** To change the commit message of an old commit.
*   **Change `pick` to `squash`:** To merge that commit into the previous one.
*   **Rearrange lines:** To physically change the chronological order of your past commits.

### Removing Traces

#### The Undo Action: `git reset`

- **Keep your code, delete the last commit:** If you want to undo the last commit but keep all the files you edited so you can change them, run:
    ```bash
    git reset --soft HEAD~1
    ```
- **Nuke everything:** If you want to completely erase the last commit AND throw away all the code modifications you did (*dangerous!*), run:
    ```bash
    git reset --hard HEAD~1
    ```

#### The Rescue Action: `git reflog`

Imagine you ran a `git reset --hard` by mistake and lost a week of work. You think it's gone forever. **It isn't.**

Git keeps a secret diary of *every single move* your repository has ever made, even things you deleted. Run:
```bash
git reflog
```
You will see a list of every action (`commit`, `checkout`, `reset`). Locate the commit ID right before you made the mistake, and restore your project back to life:
```bash
git reset --hard <that-ghost-commit-id>
```


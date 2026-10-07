# 02 - Working Remotely

So far, *we have been working locally on our computer*. However, to truly leverage the power of Git, we need to understand **remote repositories**.
- **Remote repositories are alternative copies** of the project you are working with, **hosted on the Internet** such as on [GitHub platform](https://github.com).
- Permissions on remotes:
    * **Write-access copies:** Repositories **you own or *"forks"*** where you have full permission to make changes.
    * **Read-only copies:** Reference repositories (often called `upstream`) where you can **fetch updates (`pull` action) but cannot directly modify the code (`push` action)**.

Mastering remotes is absolutely **required to perform contributions** and foster seamless collaboration within development teams.

### Managing Remotes: Add & Remove

You can check, link, and delete connections to remote servers using the `git remote` command.

* **View remote servers currently connected to your local project:**
  ```bash
  $ git remote -v
  ```

In our case, this command will return nothing as we have been solely working locally. Let's first **create the repository on GitHub** to subsequently add it as a remote:

1. Head over to https://github.com/<your-user-name>
2. Click on *Repositories > New*.
3. Give the repository a (descriptive) name, commonly the same as the one you used locally.
4. Click on *Create repository*.

* **1. Add a new remote repository:**

Now we are ready to *create the remote*. The syntax for adding a remote is:

```bash
git remote add <name> <url>
```

so:

```bash
# Be sure to be placed **within the repository folder** you want to link
$ cd ${HOME}/git-datascience-master-practice

$ git remote add origin https://github.com/<your-user-account/<your-repository-name>
```

*Let's analyse the command:*
- The `<url>` field can be copied/pasted from the landing page of the repository in GitHub.
- By convention, **the primary remote is named `origin`**.
    - Git gives that name also when cloning an existing repository with `git clone`.
    - Same applies when using a *fork*, which the standard is naming the remote as `upstream` (we'll see that later).

And now we can see the remote just added with the initial command:

```bash
$ git remote -v
origin  https://github.com/orviz/git-datascience-master-practice (fetch)
origin  https://github.com/orviz/git-datascience-master-practice (push)
```

* **2. Remove a remote connection:**

Similar syntax as with the `git remote add`:

  ```bash
  git remote remove <name>
  ```

- *Note:* `git remote remove origin` will only delete the remote link, it **does not delete the repository on GitHub**.

---

### Syncing Changes: Push & Pull

Once your remote is configured, you will use two fundamental commands to move your commits back and forth between 1) your local copy on your local machine and 2) the remote repository located at GitHub.

**Step 0: Create a GitHub Personal Access Token (PAT)** &rarr; follow [these steps](./020-github-auth.md).

**Step 1: Let's push the commits done in our local repository: `git push`**

The syntax of the *push* action in Git is as follows:

  ```bash
  git push <remote-name> <branch-name>
  ```

Thus, in our case we shall run:

```bash
$ git push origin main
```

*Your local commits are now available and in sync with the remote Git repository located at the GitHub platform.*

**Step 2: Verifying on GitHub**

1. Open your web browser and head to your **GitHub repository** &rarr; remember: `https://github.com/<your-user>/<your-repository-name>`.
2. **Observe:** Your files (`README.md`, etc.) and your exact commit history are now visible on the website. The web interface is just a reflection of what you pushed via the CLI.

**Step 3: Checking for Updates: `git pull`**

The syntax of the *pull* action in Git is as follows:

  ```bash
  git pull <remote-name> <branch-name>
  ```

Thus, in our case the command to run would be:

```bash
$ git pull origin main
```

*This downloads new commits from GitHub and merges them directly into your current local branch. **But in this case..***
- Nothing happens: the terminal will say `Already up to date.`
- *Why?* &rarr; You are the only developer working on this project, and your local machine is perfectly synced with GitHub. There is nothing new to download.

**Step 4: Simulating a Collaborative Environment**

We will simulate a change in the code on GitHub, which in the real world could have been made by an external collaborator:

1. [GitHub] On your GitHub repository webpage, **click on the `README.md` file**.
2. [GitHub] **Click the *"Edit this file"*** in the top right corner.
3. [GitHub] **Add a new line** at the bottom of the file:
   ```markdown
   > Note: This line was added remotely by a brilliant teammate working from another country.
   ```
4. [GitHub] Scroll down, **write a commit message** (e.g. *"Update README from web"*), and **click the *"Commit changes"*** button.
    - *With these changes, GitHub (the remote) is ahead of your local machine by exactly **1 commit**. Your local repository is outdated!*
5. [Terminal] Go back to the terminal. If you run **`git status`, Git local won't notice anything** yet because it doesn't constantly spy on internet traffic.
6. Let's **fetch and merge** those remote changes:
   ```bash
   $ git pull origin main
   ```
7. Inspect the Results!
    - Look at your terminal output. You will see a fast-forward summary showing that lines were added (`1 file changed, 1 insertion(+)`).
    - To prove the CLI successfully synchronized your project:
      1. Look for the remote line in the local `README.md`: either with your local editor (nano, vim, VSCode) or with `cat` Shell command.
      2. Check the history log (`git log`) and look for the commit.


### Understanding the Syncing Process in Git: Pull (`git pull`) vs Fetch (`git fetch`)

- If you remember, when we switched to the terminal to pull the commit from GitHub, the `git status` command did not complain at all &rarr; **Git did not notify us about changes being done remotely**.
- *Why does this happen?* Because **Git only talks to GitHub when you explicitly tell it to**.
- *Why did it work with `git pull`? Because **`git pull` is the combination on **two actions: `git fetch` (download metadata) + `git merge` (combine into your workspace)**.

Let's simulate another remote change to understand the *Fetch action*:
  
1. [GitHub] Follow the steps to edit the `README.md` file and commit the changes as we did above.
2. [Terminal] Back to the terminal, run `git status` to confirm Git does not know anything about the remote change in GitHub.
3. [Terminal] Force Git to check what is going on at GitHub. For this we use `git fetch`:
   ```bash
   git fetch origin
   ```
4. [Terminal] Check the content of the `README.md` file (`cat`, editor). **The new line is NOT there.** `git fetch` did not modify your files.
5. [Terminal] Run `git status`. Now Git will explicitly warn us about the differences with the remote repository:
   ```text
   Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.
     (use "git pull" to update your local branch)
   ```
*Why `git fetch` is useful?* &rarr; allows you to audit what your team did before bringing it into your computer. For instance, check the exact lines that changed before merging them by running:

```bash
git diff main origin/main
```

And now to complete the *Pull action* (remember: Fetch + Merge) we use `git merge`:

```bash
git merge origin/main
```

Now check your `README.md` locally. **The line has arrived safely!**
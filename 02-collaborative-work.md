# 02 - Collaborative Work through Git+GitHub

In this chapter will focus on the integration of local changes with a remote repository located at the GitHub platform:
* [020 - Integration of Remotes](#020---integration-of-remotes)

---

## 020 - Integration of Remotes

- So far, we have been working locally on our computer. However, to truly leverage the power of Git, we need to understand **remote repositories**.
- Remote repositories are **alternative copies** of the project you are working with, **hosted on the Internet** such as on [GitHub platform](https://github.com).
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

**Push changes to remote repositories:**
  ```bash
  git push <remote-name> <branch-name>
  ```

Let's push the commits done in our local repository (now linked to the remote):

```bash
$ git push origin main
```

  *Example:* `git push origin main` *(This uploads your local commits to the cloud).*

* **Pull changes from remote repositories:**
  ```bash
  git pull <remote-name> <branch-name>
  ```
  *Example:* `git pull origin main` *(This downloads new commits from GitHub and merges them directly into your current local branch).*
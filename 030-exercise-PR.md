# Exercise for the students: Contributing to External Projects

Up until now, you have been working on your own repositories where you have absolute control. But what happens if you want to contribute to an open-source project or a repository owned by another team member where you **do not have write permissions**?

&rarr; If you try to do a `git push` directly to their repository, Git will reject it with a `Permission Denied` error. 
&rarr; To solve this, we use the **Forking Workflow**.

---


## Required Concepts: Fork & Clone

### Concept 1: The Fork (GitHub Web)
A *Fork* is a GitHub feature that **creates a personal copy of someone else's repository under your own GitHub account**.  Then within the *Forking Workflow* we will have two remotes:
* The original repository is called the **Upstream** &rarr; by convention the remote name is: `upstream`.
* Your personal copy is called the **Origin** &rarr; by convention the remote name is: `origin`.

### Concept 2: The Clone (Git CLI)
Once you have your own copy on GitHub, you use `git clone` to download that entire project (including all its history and branches) onto your local computer.
- Syntax:
     ```bash
     git clone <url>
     ```
     where <url> in our case will point to the GitHub repository.
- Upon a successful `git clone` execution, the **`origin` remote is automatically created** for us. 

---

## 🏋️ Practice Challenge: The Open Source Simulation

For this exercise, you will play the role of an open-source contributor. The **main task is to submit a Pull Request (PR) to the Main Teacher's Repository**:

***https://github.com/masterdatascience-UIMP-UC/hellogitworld***

### Part A: Forking the Repository (Web)
1. Open your the URL above. In the **top-right corner of the page, click the *"Fork"* button**.
2. Select **your account as the owner and click *"Create fork"***.
3. GitHub will redirect you to the copy done within your repository: Note that it is now *https://github.com/<your-github-account>>/hellogitworld*

---

### Part B: Cloning the Fork to Your Machine (Git CLI)
Now, let's bring your copy down to your local workspace using the terminal.

1. On your personal fork webpage, **click the *"<> Code"* button and copy the HTTPS URL** (or use the browser's URL field).
2. **Open your terminal** and *make sure you are NOT inside your old project* folder (run `cd ..` to go back if needed).
3. Run the clone command:
   ```bash
   $ git clone https://github.com/<your-github-account>>/hellogitworld
   ```
4. Move inside the newly created directory:
   ```bash
   $ cd hellogitworld
   ```
5. Verify that the remote has been automatically created, and that it points to the `main` branch:
   ```bash
   $ git remote -v
   (..)
   ```

---

### Part C: Propose a Change to the Upstream Repository

**Now it is your turn**, remember that we will **follow the steps we've seen in the GitHub Flow**, i.e.:
1. [Terminal] Add the change/s in a feature branch, other than the `main` branch.
    - A single commit is enough, but feel free to add more than one.
    - The commit/s may imply modifications in more than one file.
    - The commit message/s shall be descriptive.
    - The Git CLI flow is: `Create & Switch Branch > Edit > *add* > *commit* > *push*`. 
2. [GitHub] Create the Pull Request.
    - Select the feature branch in the list.
    - Click on `Contribute > Open pull request`.
    - Look closely at the top dropdown menus. You will see:
        * `base repository`: The *Upstream* project (*where you want your code to go*).
        * `head repository`: Your *Fork* and your feature branch (*where your code is coming from*).
    - Provide a meaningful PR title and description.
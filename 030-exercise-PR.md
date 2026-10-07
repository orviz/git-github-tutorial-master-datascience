# Exercise for the students: Contributing to External Projects

Up until now, you have been working on your own repositories where you have absolute control. But what happens if you want to contribute to an open-source project or a repository owned by another team member where you **do not have write permissions**?

&rarr; If you try to do a `git push` directly to their repository, Git will reject it with a `Permission Denied` error. 
&rarr; To solve this, we use the **Forking Workflow**.

---

### 🧱 Concept 1: The Fork (GitHub Web)
A **Fork** is a GitHub feature that creates a personal copy of someone else's repository under your own GitHub account. 
* The original repository is called the **Upstream**.
* Your personal copy is called the **Origin**.

### 🧱 Concept 2: The Clone (Local CLI)
Once you have your own copy on GitHub, you use `git clone` to download that entire project (including all its history and branches) onto your computer's hard drive so you can work on it using VS Code.

---

## 🏋️ Practice Challenge: The Open Source Simulation

For this exercise, you will play the role of an open-source contributor. You are going to submit a change to the **Main Teacher Repository** (your instructor will provide the exact URL).

### Part A: Forking the Repository (Web)
1. Open your browser and navigate to the **Instructor's Repository URL**.
2. In the top-right corner of the page, click the **"Fork"** button.
3. Ensure your account is selected as the owner and click **"Create fork"**.
*✨ Look at the URL now! It should say `://github.com`. This copy is 100% yours.*

---

### Part B: Cloning to Your Machine (CLI)
Now, let's bring your copy down to your local workspace using the terminal.

1. On your personal fork webpage, click the green **"<> Code"** button and copy the HTTPS URL.
2. Open your VS Code terminal and make sure you are NOT inside your old project folder (run `cd ..` to go back if needed).
3. Run the clone command:
   ```bash
   git clone <PASTE-YOUR-FORK-URL-HERE>
   ```
4. Move inside the newly created directory:
   ```bash
   cd <repository-name>
   ```

---

### Part C: The Feature Branch (CLI)
Following the GitHub Flow, we never edit code on `main`. Let's create a sandbox branch for our contribution:

```bash
git checkout -b add-my-profile
```

Now, open the project in VS Code. Locate the file named `CONTRIBUTORS.md` (or the file specified by your instructor) and add your name and GitHub username to the list:
```markdown
* [Your Name](https://github.com) - Student Practitioner
```
Save the file and commit your changes using your CLI routines:
```bash
git status
git add CONTRIBUTORS.md
git commit -m "docs: add my profile to contributors list"
```

---

### Part D: Pushing Your Branch (CLI)
Push your feature branch to **your** remote repository (your fork) on GitHub:

```bash
git push -u origin add-my-profile
```

---

### Part E: Opening the Pull Request to the Original Project (Web)
This is the magic step. GitHub is smart enough to know your fork came from the original teacher's repository.

1. Go to your fork page on **GitHub.com** in your browser.
2. You will see the familiar yellow banner: **"add-my-profile had recent pushes..."**. Click **"Compare & pull request"**.
3. Look closely at the top dropdown menus. You will see:
   * `base repository`: The instructor's original project (where you want your code to go).
   * `head repository`: Your fork and your feature branch (where your code is coming from).
4. Click **"Create pull request"**.

*🎉 Congratulations! You have officially submitted a contribution to a project you don't own. The instructor can now review, comment, and merge your code into the master project.*
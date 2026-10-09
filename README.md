# Git Hands-on Workshop: Mastering the CLI 🚀

Welcome to the practical guide for this Git workshop. During this session, we will abandon graphical interfaces (GUIs) and embrace the power of the **Command-Line Interface (CLI)**.

## 🎯 Workshop Goals
* Understand what happens behind the scenes of Git.
* Master the local and remote Git workflow.
* Learn how to solve conflicts confidently from the terminal.

## Main Reference

This tutorial is based on ["Pro Git"](https://git-scm.com/book/en/v2) by Scott Chacon (2nd edition, 2014).

## 🛠️ Step 0: Set up your Environment
Before we begin, open your preferred environment and log into your **GitHub account**.

1. Local Git CLI is preferred, and even better the **use of a Git CLI integrated in a IDE [VS Code](https://code.visualstudio.com/), [Cursor](https://cursor.com/), etc.**.
2. If IDE is not an option, enable system's Git CLI:
    - [Follow installation steps based on your operating system](#git-cli-installation-local-option-preferred).
    - Note that *this option implies the use of a Terminal Editor* (`nano`, `vim`, ...)
3. For course's Day 1, and whenever the Git CLI is not available locally (check 1 and 2 above), use the Master's [Data Science Hub service](#git-cli-from-data-science-hub-services-jupyterlab-the-fastest-for-day-0).
4. Lastly, there are alternative *cloud choices* such as *GitHub Codespaces*.

### Git CLI installation: Local Option (the *Preferred Option*)

**Git installation on Linux**

1. Open a shell terminal
2. Type `git --version` + Enter. *If not installed*:
    - For Debian/Ubuntu run: `sudo apt-get install git`
    - For RedHat distros run: `sudo dnf install git`

**Git installation on MacOS**

1. Default shell is available via the `Terminal` program within your `Utilities` folder.
2. Type `git --version`. *If not installed*: [https://git-scm.com/download/mac](https://git-scm.com/download/mac)

**Git installation on Windows**

1. Install [gitforwindows.org's](https://gitforwindows.org/) app.

**Additional reference**: [Git installation steps on Software Carpentries Git tutorial](https://carpentries.github.io/workshop-template/install_instructions/)


### Git CLI from Data Science Hub service's JupyterLab (the *Fastest for Day 0*)

1. Access to the terminal:
    - Go to [Data Science Hub](https://datasciencehub.ifca.es)
    - Log in with your GitHub credentials.
    - Open a terminal: on `Files` (tab) > `New` > `Terminal`

2. Git client shall be available through the terminal.


---

## Workshop Index
Follow the files in chronological order:
* [00 - Shell Reminder](./00-shell-reminder.md) *Reminder of Shell commands targeting rapid file content editting"
* [01 - Git Basics](./01-git-basic.md) *Configuration, staging, committing, and history analysis.*
* [02 - Remote Work](./02-remote-work.md) *Moving local changes to remote GitHub repositories.*
* [03 - Collaborative Work](./03-collaborative-work.md) *Learn the Git/GitHub workflow in collaborative environments.*
    * [Exercise](./030-exercise-PR.md) *Prove your Git and GitHub knowledge.*
* [04 - Advanced Git](./04-git-advanced.md) *Fork maintenance, Complex Git Flows.*
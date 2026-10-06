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

1. Local Git CLI is preferred. If not installed, [follow installation steps based on your operating system](#git-cli-installation-local-option-preferred).
2. If not locally installed, use the Master's [Data Science Hub service](#git-cli-from-data-science-hub-services-jupyterlab-the-fastest-for-day-0).

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
* [02 - Collaborative Work](./02-collaborative-work.md) *Moving local changes to GitHub collaborative environment.*
<!-- * [03 - Advanced Git & Conflicts](./02-git-advanced.md) 🦅 *Branches, manual merging, and resolving conflicts via CLI.* -->
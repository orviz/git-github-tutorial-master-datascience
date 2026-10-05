# 00 - Shell & Terminal Reminder 💡

We primarily target Shell commands that allow us to easily and rapidly modify files, changes that will be grouped and tracked through Git. Hereafter is a quick cheat sheet of essential shell navigation commands and terminal text editors.

## The Basics of Shell

- Shell is the CLI for **running programs on UNIX systems**.
    - Runs the programs/commands and returns the output
- Shell types: *bash*, *sh*, *csh*, *zsh*, *tcsh*, ..
- **Terminal: interacts with the shel**l
    - Just like a web browser with websites
    - *Shell prompt (**$**)*: indicates that it’s ready to accept input commands

## File System Navigation

* `pwd`: Print Working Directory (*Where am I?*).
* `ls`: list the contents of a directoy
    *  `ls -la`: List all files, including hidden ones (like the `.git` folder).
* `cd <folder-name>`: Move into a folder.
* `cd ..`: Move up one level.

```bash
# List the contents of the current directory
$ ls
00-shell-reminder.md  README.md

# Show additional info from files (perms, owner, groups)
$ ls -l
-rw-rw-r-- 1 pablo pablo 2148 Oct  5 11:45 00-shell-reminder.md
-rw-rw-r-- 1 pablo pablo 2400 Oct  5 11:26 README.md
```

# Full path to the current directory
```bash
$ pwd
/home/pablo/repos/docs/git-github-tutorial-master-datascience

$ cd ..

$ pwd
/home/pablo/repos/docs
```

## Organizing File/Directories
* `mkdir <folder-name>`: Create a new directory.
* `rmdir <folder-name>`: Remove an existing empty directory.
* `rm -rf <folder-name>`: Recursively remove an existing directory (incl. with content).
* `mv`: moves files/dirs from one location to another (good to rename files/dirs).
* `touch`: creates an empty file.

```bash
$ cd git-github-tutorial-master-datascience

$ pwd
/home/pablo/repos/docs/git-github-tutorial-master-datascience

$ ls
00-shell-reminder.md  README.md

$ touch 01-git-basico.md

$ ls
00-shell-reminder.md  01-git-basico.md  README.md
```

## Viewing and Printing
* `cat <file-name>`: reads a file and outputs its contents.
* `echo <string>`:  returns whatever string you type afterwards.

## Command Help
* `<command> --help`: provides a summary of command purpose and configuration/options.
* `man <command>`: provide a comprehensive information about how to use the command.

## Redirection to Files

The combination of `echo` and the *redirection signs* provides a powerful and fast way to modify files:
* Overwrite: `>` (**warning**: this will destroy the current content of the file)
* Append: `>>`

```bash
# Create or Overwrite the contents of the `intro.txt` file.
$ echo "Welcome to the Git tutorial" > intro.txt

# Appends a new line to the current content of the `intro.txt` file.
$ echo "We will learn the basics of Git" >> intro.txt

$ cat intro.txt
Welcome to the Git tutorial
We will learn the basics of Git
```
# GIT Best Practices

## Creating a GIT Repository on GitHub
## Accessing GitHub using SSH
### Create SSH Key

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f <filename>
```
**Note:**

* You can skip entering passphrase
* Give a name for the output file when asked
* A private keyfile ```filename``` and public keyfile ```filename.pub``` are created
* Copy both these files to ~/.ssh

### Add SSH Key to ```ssh-agent```
Start SSH Agent in background

```
$ eval "$(ssh-agent -s)"
$ ssh-add -K ~/.ssh/<filename>
```

### Change SSH Config file to use this new file
Add the following to ```~/.ssh/config``` file

```
Host <User-idenfier>.github.com
	HostName github.com
	User <GITHub User name>
	IdentityFile ~/.ssh/<private-key-file>

```
### Add SSH Key to GitHub Account
Copy Public key contents to clipboard
```
$ pbcopy < <public-key-file.pub>
```

User-Profile-Dropdown -> Settings -> SSH and GPG Keys -> New SSH Key -> Paste contents of clipboard

## git init

```
$git init
```
Creates a ```.git``` folder

## Git Config
### Local, Global, System

* System File in ```/etc/gitconfig```, Use ```git --system```
* Global File in ```~/.gitconfig```, Use ```git --global```
* Local file in ```.git/config```, Use ```git --local```
* __Local__ Overrides __Global__ Overrides __System__

### File format
### UserName

```
git config --local user.name "John Doe"
```

### E Mail
```
git config --local user.email "johndoe@example.com"
```

### Editor
```
git config --global core.editor "atom --wait"
```

### Merge Tool

```
$ git config --global merge.tool p4mergetool
$ git config --global mergetool.p4mergetool.cmd \
"/Applications/p4merge.app/Contents/Resources/launchp4merge \$PWD/\$BASE \$PWD/\$REMOTE \$PWD/\$LOCAL \$PWD/\$MERGED"
$ git config --global mergetool.p4mergetool.trustExitCode false
$ git config --global mergetool.keepBackup false
$ git config --global mergetool.prompt false
```

### Diff Tool

```
$ git config --global diff.tool p4mergetool
$ git config --global difftool.p4mergetool.cmd \
"/Applications/p4merge.app/Contents/Resources/launchp4merge \$LOCAL \$REMOTE"
$ git config --global diff
$ git config --global mergetool.prompt false
```

### Setup Line-ending preferences

```
$ git config --global core.autocrlf input
$ git config --global core.safecrlf true
```

## Creating Repository by cloning

```
$ git clone git@<Host-identifier-in-ssh-config>:<git-user-name>/<git repository>

$ git clone git@subbu.github.com:nssubramanya/git-practice.git

or 

$ git clone https://github.com/nssubramanya/git-practice.git
```
## Creating repository by Pull

```
git remote add origin <repo-url>
git pull
```
## Setting a Remote Repository

```
$ git remote set-url origin <repo-url>

$ git remote add origin https://github.com/nssubramanya/git-practice.git
```
## Create Working Area from Scratch
Instead of Cloning, one can start from empty repository

```
$ mkdir git-practice
$ cd git-practice
$ git init
$ git config --local user.name "Subramanya N S"
$ git config --local user.email "subramanya.ns@gmail.com"
$ git remote add origin https://github.com/nssubramanya/git-practice.git
$ git remote -v
```


## Adding to Staging
### git add *

```
$ mkdir css
$ touch css\styles.css
$ git add css
```
### git add <filename>

```
$ echo "print('Hello, World')" > hello.py
 
$ git add hello.py
```

### git add -A
Stage changes from all tracked and un-tracked files

## See Git Status

```
$ git status
```

## Removing un-tracked files
Files that have not been added/tracked by using `git add` can just be removed with `rm` command

## Removing from Staging (back to Working) - Unstage file
If we add/stage a file that we did not intend to commit, unstage it by doing a `reset`

This can mostly happen when we add all files by using a `git add .`

```
$ git reset hello.md

or 

$ git reset .
```

This will ONLY un-stage the file. The file will still be present on disk.

## Commit 

```
$ git commit -m "Initial Commit"
```

## Amend Commit log

### Amend Commit Log with latest Additions
```
$ git add <files-to-add>
$ git commit --amend -m "First Commit"
```
## Un-Commit file (Commit to Stage)

```

```

## List Branches
### List Local branches

```
$ git branch
* master
```
### List Remote Branches

```
$ git branch -r
  origin/master
```
### List All Branches

```
$ git branch -a
* master
  remotes/origin/master
```

## List Files




## Push to Remote
## Look at status - ```git status```
## Look at Log - ```git log```
### File Statistics
### All Logs
### One-Line Logs
### Max-Count
### Since Date/Time
### Until Date/Time
### Log Custom Formatting
### Graph

## .gitignore
Create a file called ```.gitignore```.
Specify what needs to be ingored inside that file. You can specify filenames, foldernames

### .gitignore rules

## Modify Commit before Push
## GIT Diff
### Working Vs Staging
Diff of all files b/w working and staged
```
$ git diff --staged
```

Diff specific file

```
$ git diff --staged hello.py
```

### Staging Vs Commited
### Committed Vs Remote
### b/w Different Branches
### b/w Different Versions

## Git Merge

## Git Reset

## Git Remove
## Git Move
## Git clean

## Git Aliases
It is useful to have abbreviations for common Git Commands

Add the following to Global Git Config directory ~/.gitconfig

```
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```

## GIT Branching
### Create New Branch
### Show All branches
### Switch to Branch
### Delete Branch
### Create Branch on Remote
### Track Branches (-u)
## GIT Merge
## GIT Tagging & Versioning
## GIT Stash





## GIT References

### Beginner
* [GitHub GIT CheatSheet] (https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)
* [Git happens! 6 Common Git mistakes and how to fix them](https://about.gitlab.com/2018/08/08/git-happens/)
* [GIT Immersion - GIT Micro Lab Exercises](http://gitimmersion.com/)

* [Become a Git pro in just one blog. A thorough guide to Git architecture and command-line interface]
(https://itnext.io/become-a-git-pro-in-just-one-blog-a-thorough-guide-to-git-architecture-and-command-line-interface-93fbe9bdb395)

### Pro
* [GIT 7 Best Practices](https://yeti.co/blog/get-the-most-out-of-git-7-best-practices-for-budding-developers/)
	* Use Terminal
	* Use Branching and pull Requests
	* Squash and Merge
	* Avoid Merge Commits
	* Review other's code independently
	* Use git mv
	* Re-write, Don't Rage

* [Git Workflows for Pros: A Good Git Guide](https://www.toptal.com/git/git-workflows-for-pros-a-good-git-guide)

* [GIT SCM Documentation] (https://git-scm.com/docs)
* [The Git workflow you need: How to deal with multiple teams in a single repository](https://blog.logrocket.com/the-git-workflow-you-need-how-to-deal-with-multiple-teams-in-a-single-repository-faf5bb17a6e4/)
* [Minimum Viable Git Best Practices for Small Teams](https://blog.hartleybrody.com/git-small-teams/)

### Books
[Pro GIT - Best GIT Book, an excellent resource for all things Git](https://git-scm.com/book/en/v2)




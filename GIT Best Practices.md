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


## Creating Repository by cloning

```
$ git clone git@<Host-identifier-in-ssh-config>:<git-user-name>/<git repository>

git clone git@subbu.github.com:nssubramanya/git-test.git
```
## Creating repository by Pull

```
git remote add origin <repo-url>
git pull
```
## Setting a Remote Repository

```
$ git remote set-url origin <repo-url>
```
## Working Area, Staging area, Remote
## Adding to Staging
### git add *
### git add -A
### git add <filename>
### 
## Removing from Staging (back to Working)
## Commit 
## Push to Remote
## Look at status ```git status```
## Look at Log
### File Statistics
## .gitignore
Create a file called ```.gitignore```.
Specify what needs to be ingored inside that file. You can specify filenames, foldernames

## Modify Commit before Push
## GIT Diff
### Working Vs Staging
### Staging Vs Commited
### Committed Vs Remote
### b/w Different Branches
### b/w Different Versions

## Git Merge

## Git Reset

## Git Remove
## Git Move
## Git clean

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





* [GIT 7 Best Practices](https://yeti.co/blog/get-the-most-out-of-git-7-best-practices-for-budding-developers/)
	* Use Terminal
	* Use Branching and pull Requests
	* Squash and Merge
	* Avoid Merge Commits
	* Review other's code independently
	* Use git mv
	* Re-write, Don't Rage





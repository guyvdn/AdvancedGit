<!-- $theme: gaia -->

Advanced
===

# ![](images/gitlogo3.png)

###### Created by Guy Van den Nieuwenhof<br/>[https://github.com/guyvdn](https://github.com/guyvdn)

---

<!-- footer: Guy Van den Nieuwenhof - Advanced Git -->

# Advanced Git

- Properly configure Git
- Advanced Git commands 
- Customize Git with Git Hooks
- Further Reading

---

# Advanced Git

<!-- *template: invert -->

- **Properly configure Git**
- Advanced Git commands 
- Customize Git with Git Hooks
- Further Reading

---

<!-- footer: Guy Van den Nieuwenhof - Advanced Git - Properly configure Git -->

# Properly configure Git

1. Files
2. Your Identity
3. Git Credential Manager
4. Editors
5. Checking Your Settings

---

## Files

1. **/etc/gitconfig**
<small>System-wide configuration file. 
Pass the option **--system** to git config.</small>

2. **~/.gitconfig** or **~/.config/git/config**
<small>User-specific configuration file.
Pass the option **--global** to git config.</small>

3. **.git/config** (default)
<small>Repository specific configuration file.
Pass the option **--local** to git config.</small>

---

## Your Identity

**Global Identity**
```console
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@gmail.com
```

**Identity for customer specific repository**
```console
$ git config --local user.email johndoe@customer.com
```
---

## Git Credential Manager
  
<small>
  
Git Credential Managers simplify authentication with your Git repos. They also provide support two-factor authentication.
  
**Windows** 
Download and run the latest Git for Windows installer,
which includes the Git Credential Manager for Windows.
https://git-scm.com/download/win

**macOS and Linux**
```console
> git-credential-manager install
```
</small>

---
## Editors

<small>
  
**Text Editor**

```console
$ git config --global core.editor ✂
"'C:/Program Files (x86)/Notepad++/notepad++.exe' ✂
-multiInst -notabbar -nosession"
```

**Merge and Diff Tool**

```console
$ git config --global --add merge.tool kdiff3
$ git config --global --add mergetool.kdiff3.path "C:/../kdiff3.exe"
$ git config --global --add mergetool.kdiff3.trustExitCode false

$ git config --global --add diff.guitool kdiff3
$ git config --global --add difftool.kdiff3.path "C:/../kdiff3.exe"
$ git config --global --add difftool.kdiff3.trustExitCode false
```

</small>

---

## Checking Your Settings

<small>  
  
If you want to check your configuration settings, you can use the `git config --list` command to list all the settings Git can find at that point.

```console
$ git config --list
user.name=John Doe
user.email=johndoe@example.com
..
```
You may see keys more than once, because Git reads the same key from different files (`~/.gitconfig` and `.git/config`, for example). In this case, Git uses the last value for each unique key it sees.

</small>

---

## Checking Your Settings

<small>  
  
You can also check what Git thinks a specific key’s value is by typing `git config <key>`
```console
$ git config user.name
John Doe
```
  
</small>

---
<!-- footer: Guy Van den Nieuwenhof - Advanced Git -->
<!-- *template: invert -->

# Advanced Git

- Properly configure Git
- **Advanced Git commands**
- Customize Git with Git Hooks
- Further Reading

---

<!-- footer: Guy Van den Nieuwenhof - Advanced Git - Advanced Git commands -->

# Advanced Git commands

1. git log
2. git reset
3. git rebase interactive
4. git worktree
5. git alias

---

## git log
<small><small>
  
Visualising the git history and branches is often an argument to use a git GUI tool but this can perfectly be done from the command line using `git log` with these commands:

<small>
  
**--all**
Shows all commits in the history of branches, tags and other refs

**--graph**
Text-based graphical representation of the commit history.

**--pretty**  
Pretty-print the contents of the commit logs.<br/>Can be oneline, short, medium, full, fuller, email, raw, format:\<string>

**--abbrev-commit**
Show partial prefix of the 40-byte hexadecimal commit object name.

**--oneline**
This is a shorthand for "--pretty=oneline --abbrev-commit" used together.

</small></small></small>

---

##  `$ git log --graph --all --oneline` 

# ![](images/vscode-log.png)

---
<small><small>
  
```console
$ git log --graph --all ✂
--pretty=format:"%C(auto)%d %s %C(yellow)%ad %C(cyan)<%an> %C(green)%h" ✂ 
--date="format-local:%Y-%m-%d %H:%M:%S"
```
</small></small>
  
# ![](images/vscode-log-fancy.png)

---

# git reset

### Can be used to undo changes that are ==local to your computer==

---

## git reset - trees

# ![](images/reset-workflow.png)

---

## git reset - commands

git reset overwrites these trees in a specific order

<small>
  
**git reset --soft**
move the branch HEAD points to
==can be used to undo commits==

**git reset --mixed (default)**
also make the Index look like HEAD
==can be used to unstage changes==

**git reset --hard**
also make the Working Directory look HEAD
==can be used to undo changes==

</small>

---

# git reset - demo

---

# git rebase interactive

<small>
  
**git rebase --interactive**
**git rebase -i**

Make a list of the commits which are about to be rebased. Let the user edit that list before rebasing.

<br/><br/>
 
```text
Do not rebase commits that exist outside your repository.
If you follow that guideline, you’ll be fine. 
If you don’t, people will hate you.
```

</small>

---

## git-rebase-todo file

<small><small>
  
```text
pick 2a6ed8c v4
pick d5a5839 v5
pick 010a3f0 v6

# Rebase fba439a..010a3f0 onto fba439a (3 commands)
#
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
#	However, if you remove everything, the rebase will be aborted.
```

</small></small>

---

## git rebase interactive - commands

<small>
  
**pick**
use commit 
==default, use the commit as is==

**reword**
use commit, but edit the commit message
==do not change the message in the todo file, you will be prompted for a new message==

**edit**
use commit, but stop for amending
==can be used to add, remove or change files in the commit<br/>you will have to **git commit --amend** followed by **git rebase --continue** to complete this step==

</small>

---

## git rebase interactive - commands

<small>
  
**squash**  
use commit, but meld into previous commit
==can be used to combine multiple commits into one<br/>you will be prompted for which commit message to keep==

**fixup**
like "squash", but discard this commit's log message
==skip the prompt for the commit message if the first message is the one you would like to keep==
  
</small>

---

## git rebase interactive - commands

<small>
  
**drop**
remove commit
==e.g. remove merge commits that become irrelevant after rebasing==
  
**label**
label current HEAD with a name
==to create a reference that can later be used==
 
</small>

---

## git worktree

<small>
  
Manage multiple working trees attached to the same repository.

A git repository can support multiple working trees, allowing you to check out more than one branch at a time

This new working tree is called a "**linked working tree**" as opposed to the "**main working tree**" prepared by "**git init**" or "**git clone**"

A repository has one main working tree and zero or more linked working trees.

</small>

---

## git worktree - commands

<small>  

**add**
```console
git worktree add <path> <remote>/<branch>
```
<small> 
  
Create \<path> and checkout into it. The new working directory is linked to the current repository, sharing everything except working directory specific files such as HEAD, index, etc. 

Every branch can only exist in one worktree. You can create a new branch with the option `-b <branch>`

</small> 

**list**
<small> 
  
List details of each worktree. The main worktree is listed first, followed by each of the linked worktrees.

</small> 

</small>

---

## git worktree - commands

<small>  
  
**lock**

<small>  
  
Prevent it from being pruned automatically in case it is on a portable device or networkshare which is not always mounted. 
Also prevents it from being moved or deleted.
 
</small>

**unlock**

<small>  
  
Unlock a working tree, allowing it to be pruned, moved or deleted.

</small>
 
</small>

---

## git worktree - commands

<small>  

**move**

<small> 
  
Move a working tree to a new location. 
 
</small>

**remove**

<small> 
  
Remove a working tree. Only clean working trees (no untracked files and no modification in tracked files) can be removed. Unclean working trees or ones with submodules can be removed with --force. The main working tree cannot be removed.

</small>
  
**prune**

<small> 
  
Prune working tree information in $GIT_DIR/worktrees.

</small>
 
</small>

---

## git alias
<small> 
  
Now that we have seen some advanced commands we can make it easier to use them wit `git alias`. 

For example, to correct the usability problem you encountered with unstaging a file you can add your own unstage alias to Git:

```console
$ git config --global alias.unstage 'reset HEAD --'
```
This makes the following two commands equivalent:

```console
$ git unstage fileA
$ git reset HEAD -- fileA
```
</small>

---

## git alias
<small> 
  
Some more commands

|Alias|Command|
|-:|:-|
|**s**        | status -sb
|**last**     | log -1 HEAD
|**tree**     | log --all --oneline --graph
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**branches** | branch -a
|**stashes**  | stash list
|**aliases**  | !git config -l \| grep alias \| cut -c 7- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
|**echo**     | !echo \"$1\" && :
|**chs**	  | !git checkout && git s && :

</small>

---

## git alias

**Share aliases in team**

You can put all aliases inside a separate config file

```text
[alias]
  a = add
  ..
```

Add this file to your `.config` file as such

```text
[include]
    path = aliases.txt
```

---

# Advanced Git
<!-- footer: Guy Van den Nieuwenhof - Advanced Git -->
<!-- *template: invert -->

- Properly configure Git
- Advanced Git commands 
- **Customize Git with Git Hooks**
- Further Reading

---

<!-- footer: Guy Van den Nieuwenhof - Advanced Git - Customize Git with Git Hooks-->

# Git hooks

 Git has a way to fire off custom scripts when certain important actions occur. 
 
 **Client-side** hooks are triggered by operations such as committing and merging.
 
 **Server-side** hooks run on network operations such as receiving pushed commits.

---

# Git hooks - samples

<small>

Some samples can already be found in the .git\hooks folder

```text
applypatch-msg.sample
commit-msg.sample
fsmonitor-watchman.sample
post-update.sample
pre-applypatch.sample
pre-commit.sample
pre-push.sample
pre-rebase.sample
pre-receive.sample
prepare-commit-msg.sample
update.sample
```

</small>

---

<small> 
  
# Git hooks - commit-msg example

<small>
  
A sample ruby script that will check if the commit message starts with a Jira ticket number.

```ruby
#!/usr/bin/env ruby
message_file = ARGV[0]
message = File.read(message_file)

$regex = /JIRA-(\d+) .+/

if !$regex.match(message)
  puts "[ERROR] Your message should start with a Jira ticket number."
  exit 1
end
```

When executed in the console it will look like this and the commit is not completed.

```console
$ git commit -m blah
[ERROR] Your message should start with a Jira ticket number.
```

</small></small>

---

<small>
  
# Stash unstaged changes before running tests
  
Ensure that code that isn’t part of the commit isn’t tested within your pre-commit script.

```sh
# pre-commit.sh
STASH_NAME="pre-commit-$(date +%s)"
git stash save -q --keep-index $STASH_NAME

# Test prospective commit
...

STASHES=$(git stash list)
if [[ $STASHES == "$STASH_NAME" ]]; then
  git stash pop -q
fi
```

</small>

---

<small>
  
# Skip the pre-commit hook

```console
git commit --no-verify
```

This option bypasses the pre-commit and commit-msg hooks

</small>

---

# Advanced Git
<!-- footer: Guy Van den Nieuwenhof - Advanced Git -->
<!-- *template: invert -->

- Properly configure Git
- Advanced Git commands 
- Customize Git with Git Hooks
- **Further Reading**


---

<small>
  
## Further Reading

<!-- footer: Guy Van den Nieuwenhof - Advanced Git - Further Reading-->
<small>
  
**Git Reference Manual**<small>
  https://git-scm.com/docs
  The official and comprehensive man pages that are included in the Git package itself
</small>

**GitHub Cheat Sheet**<small>
  https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf
  Summarizes commonly used Git command line instructions for quick reference
</small>

**Visual Git Cheat Sheet**<small>
  http://ndpsoftware.com/git-cheatsheet.html
  An interactive cheat sheet from NDP Software
</small>

**Pro Git book**<small>
  https://git-scm.com/book
  Free book by Scott Chacon and Ben Straub. Also available on amazon.com
</small>

**Pluralsight - Mastering Git**  Paolo Perrotta<small> https://app.pluralsight.com/library/courses/mastering-git/
</small>

</small></small>


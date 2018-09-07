<!-- $theme: gaia -->

Advanced
===

# ![](images/gitlogo3.png)

###### Created by Guy Van den Nieuwenhof<br/>[https://github.com/guyvdn](https://github.com/guyvdn)

---

# Agenda

- Properly configure Git
- Advanced Git commands 
- Customize Git with Git Hooks
- Further Reading

---

# Agenda

- **Properly configure Git**
- Advanced Git commands 
- Customize Git with Git Hooks
- Further Reading

---

<!-- *template: invert -->

# Properly configure Git

1. Files
2. Your Identity
3. Git Credential Manager
4. Editors
5. Checking Your Settings

---

<!-- footer: Properly configure Git -->

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

# Agenda

- Properly configure Git
- **Advanced Git commands**
- Customize Git with Git Hooks
- Further Reading




---

# Agenda

- Properly configure Git
- Advanced Git commands 
- Customize Git with Git Hooks
- **Further Reading**


---
## Further Reading
<!-- footer: -->
<small><small>
  
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
  https://git-scm.com/book</br>Free book by **Scott Chacon** and **Ben Straub**. Also available on amazon.com
  </small>
  
</small></small>


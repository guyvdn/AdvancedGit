# Git Reset Demo

###### Created by Guy Van den Nieuwenhof<br/>[https://github.com/guyvdn](https://github.com/guyvdn)

---

<!-- footer: Guy Van den Nieuwenhof - Advanced Git - Git Reset Demo -->

### Initialize Working folder

Initialize git

```console
$ git init
```

Create an alias to quickly show history

```console
$ git config alias.lo "log --oneline"
```
---

### Create a *Green build'*

Create a new file

```console
$ echo green build > file
```
Stage and Commit the file

```console
$ git add -A
$ git commit -m "green build"
```
View history

```console
$ git lo
```
---

### Create a *Red build*

Change the file content

```console
$ echo red build > file
```

Commit changes

```console
$ git commit -a -m "red build"
```

View history

```console
$ git lo
```

---

### Start fixing the build

Change the file content

```console
$  echo partial fix > file
```

Stage the changes

```console
$  git add -A
```

---

### Start final fix

Change the file content

```console
$ echo final fix > file
```

View status and diff

```console
$ git status
$ git diff
```
---

### Somebody wants you to push the *green build*

We don't want to loose our changes in staging and working folder

```console
$ git lo
$ git reset --soft <ref green build>
```

View history, status and diff

```console
$ git lo
$ git status
$ git diff
```

History has changed, staging and working folder did not.
Commit of green build can now be pushed to origin.

---

### You want to review your changes against *green build*

We don't want to loose our changes in working folder but we don't care about the staged version

```console
$ git lo
$ git reset --mixed <ref green build>
```

View status and diff

```console
$ git status
$ git diff
```
Staging has changed to *green build* but working folder is the same.
Diff will now show *final fix* agaisnt green build.

---

### Final fix is complete

Commit *final fix*

```console
$ git commit -a -m "final fix"
$ git lo
```

---

### Someone else fixed the issue. 
We need to discard our changes so that they don't get pushed. 
We also need to reset our working folder.

```console
$ git lo
$ git reset --hard <ref green build>
```

 Verify the changes
```console
$ git lo
$ git status
$ more file
```

All trees are now back at *green build*

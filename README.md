# BUSINESS_INT 
BUSINESS_INT is repo for BI Team.
# BUSINESS_INT_QA 
BUSINESS_INT_QA is repo for QA BI Team.
# DEPLOYMENT_BI
??? is repo for ???.

========================================================================================
##Overview
http://git.c11.telesign.com/

http://nvie.com/posts/a-successful-git-branching-model/
```sh
$ git branch                Show all branches

$ git add .                 Adds all local changes into staging
    $ git add manifest.yml
    
$ git commit -m 'Message'   Creates commit with custom message

$ git push <REMOTENAME> <LOCALBRANCHNAME> Push local branch to a remote repository
    $ git push origin develop
$ git push <REMOTENAME> <LOCALBRANCHNAME>:<REMOTEBRANCHNAME> Rename branch

$ git tag                   Show all tags
$ git tag -l 'v1.4.2.*'     Show all tags with name like v.1.4.2.*
```
##Create branch
Pozicionirati se na granu (master, develop) sa koje zelimo da napravimo novu (develop, feature, releaase, hotfix), a zatim odatle napraviti lokalnu granu.
```sh
$ git checkout master
$ git checkout -b develop

Shorthand for:
 $ git checkout master
 $ git branch develop
 $ git checkout develop
```
### Create more branches
```sh
$ git checkout develop
$ git checkout -b bi-101

Shorthand for:
 $ git checkout develop
 $ git branch bi-101
 $ git checkout bi-101
```
### Create more branches - e.g. other developers
```sh
$ git checkout develop
$ git checkout -b bi-102
```
## Merge 
```sh
$ git checkout develop
$ git merge bi-101
Updating f42c576..3a0874c
Fast-forward
```
Fast-forward happened because there is no divirgent work to merge together. Only pointer has been moved.
### Merge branch in ancestor with diverged history
```sh
$ git checkout develop
$ git merge bi-102
Auto-merging manifest.yml
Merge made by the 'recursive' strategy.
```
Recursive (three-way merge) strategy happened because history diverged from some older point. New commit object has been created. "Merge commit" object is special because it has two parents.
### Basic Merge Conflicts
```sh
$ git status
On branch develop 
You have unmerged paths.
    (fix conflicts and run "git commit")

Unmerged paths:
    (use "git add <file>..." to mark resolution)
    
    both modified:          manifest.yml
no changes added to commit (use "git add" and/or "git commit -a")
```
#### Standard conflict-resolution markers
```sh
<<<<<<< HEAD
databases\table\deploy\bi_101_table_name.sql
=======
databases\table\deploy\bi_102_table_name.sql
>>>>>>> bi-102
```
Continue with merging process. 
```sh
$ notepad manifest.yml
Resolvde merge conflict in editor; CTRL+S; Close notepad
$ git add manifest.yml          (Added manifest.yml to staging)
$ git commit -m 'Description of commit'
$ git push
$ git pull
```
## Delete branch
```sh
$ git branch -d bi-101
Deleted branch bi-101 (was 3a0874c).
$ git branch -d bi-102
Deleted branch bi-102 (was 1b2385a).

$ git branch -d release/1.48 (Credits Milan)
$ git fetch –prune
$ git branch –a       (za proveru)

```
## Tags
```sh
*Show all tags*
$ git tag                   Show all tags
$ git tag -l 'v1.4.2.*'     Show all tags with name like v.1.4.2.*

*Send tags to the server, after commit*
($ git push origin master)
$ git push origin [tagname]
$ git push origin --tags    Push all tags to the server

*Delete tags*
$ git tag -d 1.0
$ git push origin :refs/tags/1.0
```
### Lightweight tags
A lightweight tag is very much like a branch that doesn’t change — it’s just a pointer to a specific commit.
```sh
$ git tag v1.4-lw
```
Show the tag:
```sh
$ git show v1.4-lw
commit 15027957951b64cf874c3557a0f3547bd83b3ff6
Merge: 4a447f7... a6b4c97...
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sun Feb 8 19:02:46 2009 -0800

    Merge branch 'experiment'
```
Show all tags:
```sh
$ git tag
v0.1
v1.3
v1.4
v1.4-lw
v1.5
```
Add tag on the commit later:
```sh
$ git tag -a v1.2 -m 'version 1.2' 9fceb02
```
### Annotated tags
Annotated tags, however, are stored as full objects in the Git database. They’re checksummed; contain the tagger name, e-mail, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG). It’s generally recommended that you create annotated tags so you can have all this information; but if you want a temporary tag or for some reason don’t want to keep the other information, lightweight tags are available too.
```sh
$ git tag -a v1.4 -m 'my version 1.4'
```
Show description of tag:
```sh
$ git show v1.4
tag v1.4
Tagger: Aleksandar Dimitrievski <adimitrievski@telesign.com>
Date:   Tue May 13 14:45:11 2014 +0200

my version 1.4

commit 15027957951b64cf874c3557a0f3547bd83b3ff6
Merge: 4a447f7... a6b4c97...
Author: Aleksandar Dimitrievski <adimitrievski@telesign.com>
Date:   Mon May 12 19:02:46 2014 +0200

    Merge branch 'experiment'
```
### Create branch from tag
```sh
$ git checkout -b new_branch_name commit_id
or
$ git checkout -b new_branch_name tag_name
```

# Credits Aleksandar, BI QA

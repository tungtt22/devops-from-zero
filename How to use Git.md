# Common Command
## 1. Create repository
```sh
    #  Initiate repository.
    $ git init
```
## 2. Registry new change file/folder
```sh
$ git add <filepattern>
```
filepattern: 
    
    > define correctly file name

    > *.txt" define all file with format .txt

    >  . contain all files/folder (sub directory) in directory working

## 3. Commit 
```sh
$ git commit -m "Commit message with action add"
$ git commit -m "Commit message for change "
```
## 4. Status List of Files/Folder 
```sh
$ git status
```
## 5. Show different 
```sh
$ git diff
```
## 6. Show log
```sh
$ git log
```
## 7. Show detail commit
```sh
$ git show <commit>
```
## 8. Move file/folder
```sh
$ git mv <oldfilename> <newfilename>
```
## 9. Delete file
```sh
$ git rm <file>
```
## 10. Clean 
```sh
$ git clean
```
## 11. Checkout
```sh
# Checkout with branch name
$  git checkout  <branchname>
```
```sh
# Checkout with file name
$ git checkout -- <file>
```
# Branch Command

## 1. Show Branch List
```sh
$ git branch # Show local branch
$ git branch -r # Show remote branch
$ git branch -a # Show both remote and local branch
```
## 2. Create new branch
```sh
$ git branch <branchname>
```
## 3. Change branch name
```sh
$ git branch -m <oldbranch> <newbranch>
```
## 4. Delete branch
```sh
$ git branch -d <branchname>
```
## 5. Change branch
```sh
# This command do check out and change to branch
$ git checkout <branch>
```
## 6. Merge branch
```sh
$ git merge <branch>
```
# Remote command
## 1. Clone repository
```sh
$ git clone <giturl>
```
## 2. Add remote repository
```sh
$ git remote  add <name> <giturl>
```
## 3. Show remote repository list
```sh
$ git remote
$ git remote -v # Show more detail remote repository
```

## 4. Delete remote branch
```sh
$ git push --delete <repository> <branchname>
```
# Tag Command
## 1. Show tag list
```sh
$ git tag
$ git tag -n : # Show comment or noted of tag
```
## 2. Create new tag
```sh
$ git tag <tagname>
```
## 3. Create tag wiht comment
```sh
$ git tag -a <tagname>
```
## 4. Delete tag
```sh
$ git tag -d <tagname>
```
# References
[Git Tutorial](https://backlog.com/git-tutorial/vn/reference/) 


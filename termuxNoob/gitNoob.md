# github

    git config --global user.name "Bertland Hope"
    git config --global user.email "bertlandhope@gmail.com"

    install vscode
    install gitbash for windows

# Git Config 

git config command 

    git config --global user.name "Your Name" 
    git config --global user.email "Your Email" 

# create a folder

    open with vscode
    open terminal
    change terminal to gitbash
    git init

# Staging Files 

    git add FILENANE 
    git add  --all
    git add --A 
    git add . 
    git commit -m "First Commit" 
    git log

# Git Environments

Working - working store
Staging - temp store que up changes -use the git add command
Commit - final evn -use the git commit command

# File States

Tracked - Unmodified Modified Staged - files from the previous commit\snapshot
Untracted - anything else eg a new file added since the last commit

# Tracked Files 

Unmodified - no change since last commit
Modified - changes since last commit
Staged - files in staging use git add command

    git status

# Restoring Files 

    git restore . 
    git checkout .

make a change to this file

    git add .
    git status
    git restore --staged gitNoob.md
    git status
    git restore .

    Create a file at project folder root .gitignore
    .DS_Store
    .vscode/
    authentication.js
    node_modules
    notes/
    **/*-todo.md

    git add .
    git commit -a -m "Fifth Commit"

# Global Ignore File

    git config --global core.excludesfile [file]

# Clearing the cache

    git rm -r --cached .

    git add .
    git commit -a -m "Fifth Commit"

# Deleting and Renaming

    Delete from file system
    git status
    git add .
    git commit -a -m "this take so much time add and them commiting"
    git restore .

# Use git rm

    git rm indexDeleteme.html
    git restore -S .
    git restore .

# Rename Files

    use file explore to rename a file
    git status
    git restore .
    manually delete the untracked file
    git status

# use git mv

    git mv indexDeleteme.html indexHome.html

    git mv indexHome.html indexDeleteme.html - restore 
    git status

# Differences

    git diff

    use source controll editor to add files to staging
    git add .
    git commit -a -m "Moved Files"

# Git Log

    git log
    git log --oneline
    git diff 19ed178

    plugin for visual studio code git lense

# Changing History

    Amending
    git commit --amend
    git commit -am "New commit message"
    git commit -amend --no-edit

    git log --oneline

# Rewind

    git log --oneline
    git reset 2784909
    git reset --hard 2784909 - dangerous will delete pervious commits

# Rebasing

# Branches

    git branch
    git switch -c NAME
    git checkout -b NAME

    git switch -c noob-branch-test

# Merging

    git merge <branch>
    git switch master
    git merge noob-branch-test
    git log --oneline

# Deleting a branch

    git branch -d NAME
    git branch -D NAME

    git branch -d noob-branch-test
    git branch

# Git Flow

    Feature/fix branch
    Make changes
    Merge to master
    Delete old branch

    leave the master
    make a branch
    work on it
    merge to master
    delete the branch

# Merge Conflicts

    git restore .
    git stash list
    Stashing Code
    git stash
    git stash list
    git stash apply
    git stash pop

# Git Clean

    git clean -n
    git clean -d
    git clean -f
    git clean -df


# Working with Github

    Set up remote
    Push
    Fetch/Pull

# Set up remote

    github.new
    https://github.com/bertlandh/congenial-train.git
    NAME Aa1 _ - .
    click suggested name
    add description
    set public or private
    click create repository

# Git Remote

    git remote add NAME URL
    git remote remove NAME
    git rename OLDNAME NEWNAME
    git remote -v

    git remote add origin https://github.com/bertlandh/congenial-train.git
    git push --all

# Git Push

    git push REMOTE BRANCH
    git push --set-upstream-to origin main
    git push -u origin main # --set-upstream
    git push --all
    git branch --set-upstream-to <origin/remote-branch>




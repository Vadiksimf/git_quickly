# git_quickly

## Git initializating
Set up user
``` git
git config --global user.name "Vadym H"
git config --global user.email "email@mail.com"
```
In folder:
``` git
git init
```

In file: .gitignore 
> node_modules/           - folder </br>
> *.env                   - all .env files 


``` git
git status              - see not commited files 
git add -A 
git commit -m "Initial" 
```

Connect to remote cloud repository
```
git remote add origin https://github.com/...
git push origin master
```
Deleting info about remout cloud repository in current project (unchain)
Watch of a remote name
```
git remote -v                                 
```
View current remotes:
> origin  https://github.com/OWNER/REPOSITORY.git (fetch) </br>
> origin  https://github.com/OWNER/REPOSITORY.git (push) </br>
> destination  https://github.com/FORKER/REPOSITORY.git (fetch) </br>
> destination  https://github.com/FORKER/REPOSITORY.git (push) </br>

Delete info (unchain)
```
git remote rm origin  
```

Get changes from remote repo
``` git
git pull origin master        
```

## Git coloring
* Coloring git: 
``` git
git status        
```

if not colored: 
``` git
git config --global color.ui auto     
```
## Working with branches
``` git
git branch new_branch  
```
This command will create a new branch but we will still be on the master branch. </br>
The way git keeps track of what branch we are on is by using a cursor called HEAD.

This is the current situation (where A is the first commit you created):
> new_branch  -- A</br>
> master      -- A <- (HEAD)

To switch to new_branch we run:
``` git
git checkout new_branch 
```
> new_branch  -- A <- (HEAD)</br>
> master      -- A 

Show all the commit history as a list
``` git
git log 
```
Revert commits
``` git
git reset --hard ${ID_OF_FIRST_COMMIT}
git revert ${ID_OF_LAST_COMMIT}
```
:wq (:wq!) - выйти из vim с сохранениями

## Merging and rebasing

### Merging

Situation before merging
> new_branch  -- A -- B -- C       </br>
> master      -- A -- D -- E <- (HEAD)

Merge new_branch into master:
``` git
git merge new_branch
```
Situation after merging
> new_branch  -- A -- B -- C  </br>
> master      -- A -- B -- C -- D -- E <- (HEAD) // IN TIME ORDER

### Rebase
> new_branch  -- A -- B -- D     </br>         
> master      -- A -- C <- (HEAD)

When merging into master we would, rightfully, expect B to go before C and D after. </br>
But before merging we can rebase new_branch on top of master:  </br>
``` git
git checkout new_branch
git rebase master
```
Now the situation has changed:
> new_branch  -- A -- C -- B -- D </br>         
> master      -- A -- C <- (HEAD)

If we now merge new_branch into master:
``` git
git checkout master
git merge new_branch
```
The situation will be:
> new_branch  -- A -- C -- B -- D          </br>
> master      -- A -- C -- B -- D <- (HEAD)

## Resolve conflicts
1. git mergetool
``` git
git mergetool
```
2. Use one of the below: 
- Keep the changes in the original branch.
- Overwrite the changes with the new branch.
- Keep both changes (but give more priority to the original branch).
- Keep both changes (but give more priority to the new branch).
- Delete the conflicting lines (almost never what you want).

## Save changes but not commit
``` 
git stash
``` 
## Reset
Reset to a previous commit without touching the files
``` git
git reset --soft ${COMMIT_ID}
```

Reset to a previous commit with touching the files
``` git
git reset --hard ${COMMIT_ID}
```

Clean all the untracked files
``` git
git clean -n         - show files
git clean -f         - remove files
```

Reset a single file to its previous state
``` git
git checkout -- ${PATH_TO_FILE}
```

Retrieve a specific file from a specific branch
``` git
git checkout ${BRANCH} -- ${PATH_TO_FILE}
```

### Deletin DS_Store
Remove existing files from the repository:
```
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```
Add the line
```
.DS_Store
```
to the file .gitignore, which can be found at the top level of your repository (or created if it isn't there already). You can do this easily with this command in the top directory
```
echo .DS_Store >> .gitignore
```
Then
```
git add .gitignore
git commit -m '.DS_Store banished!'
```


https://learngitbranching.js.org/?locale=ru_RU

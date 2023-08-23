# Work with remote repositories

```bash
# show remote repository address
git remote -v

# add remode repository address into git
git remote add origin http://{username}@gitlab.com/{group}/reponame.git

# rename remode repository address into git
git remote rename origin http://{username}@gitlab.com/{group}/reponame.git 

# connect to remote address
ssh -Tv git@gitlab.com
```

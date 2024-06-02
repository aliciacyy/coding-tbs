---
label: Git
---

### Github cheatsheet
- https://training.github.com/downloads/github-git-cheat-sheet/
- https://docs.github.com/en/get-started/quickstart/github-flow
- https://github.blog/2015-01-21-how-to-write-the-perfect-pull-request/
- https://dev.to/chrissiemhrk/git-commit-message-5e21

### Switch Git credentials
!!!
For Windows users only
!!!
1. Open Credential Manager
2. In `Generic Credentials`, edit `git:https://github.com`
3. Set username as the name to be displayed
4. Set password with a personal access token
   1. If token has expired, re-generate at https://github.com/settings/tokens

### Add new changes to previous commit
Commit must not be pushed yet.
```
git commit --amend --no-edit
```

### Reset back to branch
```
git reset --hard origin/main
```

### Rename local branch
```
git branch -m <newname>
```

### Delete local branch
```
git branch -D <branch_name>
```
 
### Update commit author
```
git rebase -i <commit>
git commit --amend --author="<name> <<email>>" --no-edit
git rebase --continue
git push -f
``` 

### Set git config
```
git config --global user.name <name>
git config --global user.email <email>
```
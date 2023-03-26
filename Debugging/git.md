---
label: Git
---

### Permission denied (publickey)

#### Error 
`Permission denied (publickey).`

#### Solution
1. Create SSH key with the following commands
```
cd ~/.ssh && ssh-keygen
cat id_rsa.pub | clip
```
2. Go to Github > Settings > SSH and GPG keys > New SSH keys

**Credit:** <a href="https://stackoverflow.com/a/2643584" target="_blank">https://stackoverflow.com/a/2643584</a>

### Permission to XXX.git denied to github-actions

This happened when trying to use Github Actions to deploy.

#### Error 
`remote: Permission to XXX.git denied to github-actions[bot]. fatal: unable to access 'XXX': The requested URL returned error: 403`

#### Solution
Settings > Actions > General > Workflow Permissions

URL should be: `github.com/{your_github}/{repo}/settings/actions`

Set to "Read and write permissions"

**Credit:** <a href="https://stackoverflow.com/a/63337788" target="_blank">https://stackoverflow.com/a/63337788</a>
---
label: Coding TBS - Retype
---

### Project summary

Documenting solutions to resolving build/code errors and past side projects using <a href="https://retype.com/" target="_blank">Retype</a>.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/coding-tbs/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/coding-tbs)


### Setup guide

The setup and deploy guide is up to date with version `1.11.2`

1. Install Retype:

```
npm install retypeapp --global
```

2. Run Retype:
```
retype watch
```

### Deploy to Github Pages

#### Prerequisites
1. Create `.github/workflows` folder in the project root directory.

2. Add this file `retype.yml` to the folder.

``` .github/workflows/retype.yml
name: Publish Retype powered website to GitHub Pages
on:
  workflow_dispatch:
  push:
    branches:
      - master

jobs:
  publish:
    name: Publish to retype branch

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - uses: retypeapp/action-build@v1

      - uses: retypeapp/action-github-pages@v1
        with:
          update-branch: true
```
!!!
The official guide uses `main` for the branch, but for my repo, my main branch was `master`
!!!

3. In `retype.yml` (the one in root directory), edit the url with the expected url (e.g. `<github_user>.github.io/<repo>/`).
4. Commit and push the changes.
5. Go to Github Pages at `https://github.com/<github_user>/<repo>/settings/pages`.
6. Select `retype` branch with `/(root)` and save.

#### Deployment
Github Pages will be automatically deployed whenever changes are pushed to the branch due to Github Actions.

### Official guides
- <a href="https://retype.com/guides/getting-started/" target="_blank">Installation</a>
- <a href="https://retype.com/guides/github-actions/" target="_blank">Deploying to Github Pages</a>
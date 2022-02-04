---
label: Pigster Churn - Docusaurus 2
---

### Project summary

A website for recording all my recorded video gameplays using <a href="https://docusaurus.io/" target="_blank">Docusaurus</a>.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank" text="Pigster Churn"](https://pigsterchurn.github.io/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/pigsterchurn/pigsterchurn.github.io)


### Setup guide

The setup and deploy guide is up to date with version `2.0.0-beta.8`

1. Initialization:

```
npx create-docusaurus@latest <repo_name> classic
```

2. Run Docusaurus:
```
cd <repo_name>
npm run start
```

### Deploy to Github Pages

#### Prerequisites

1. Go to Github Pages at `https://github.com/<github_user>/<repo>/settings/pages`.
2. Select `gh-pages` branch with `/(root)` and save.
3. Modify `docusaurus.config.js` and add the following params:
   1. organizationName: pigsterchurn
   2. projectName: pigsterchurn.github.io

#### Deployment
```
GIT_USER=pigsterchurn DEPLOYMENT_BRANCH=gh-pages yarn deploy
```

### Official guides
- <a href="https://docusaurus.io/docs/installation" target="_blank">Installation</a>
- <a href="https://docusaurus.io/docs/deployment" target="_blank">Deploying to Github Pages</a>
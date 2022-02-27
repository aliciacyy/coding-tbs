---
label: Mathy Msg - Angular 13
---

### Project summary

A simple mathematics game using <a href="https://angular.io/" target="_blank">Angular 13</a>.

Best viewed on mobile phones.

**How to play:**
- You have 10 seconds to answer each question (timer is on the top left)
- Click the alphabet that corresponds to the correct number
- If an answer is wrong or 10 seconds is up, you lose and need to restart from the beginning
  
#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/mathy-msg/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/mathy-msg)


### Setup guide

The setup and deploy guide is up to date with version `13.0.4`

1. Install Angular:

```
npm install -g @angular/cli

```
2. Initialization:
```
ng new mathy-msg --directory ./
```

The `--directory ./` flag is to initialize the Angular project in the current directory.

3. Run Angular:
```
ng serve
```

### Deploy to Github Pages

#### Prerequisites
1. Go to Github Pages at `https://github.com/<github_user>/<repo>/settings/pages`.
2. Select `gh-pages` branch with `/(root)` and save.
3. Install `angular-cli-pages`
```
npm i angular-cli-ghpages --save-dev
```

#### Deployment
Run these commands:
```
ng build --prod --base-href https://<github_user>.github.io/<repo>/
npx angular-cli-ghpages --dir=dist/<repo>
```

### Official guides
- <a href="https://angular.io/start" target="_blank">Installation</a>
- <a href="https://medium.com/tech-insights/how-to-deploy-angular-apps-to-github-pages-gh-pages-896c4e10f9b4" target="_blank">Deploying Angular apps to Github Pages</a>
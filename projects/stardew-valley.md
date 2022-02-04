---
label: Stardew Valley - Angular 6
---

### Project summary

A quick reference guide on the game <a href="https://www.stardewvalley.net/" target="_blank">Stardew Valley</a> using <a href="https://angular.io/" target="_blank">Angular 6</a>.

**Features:**
- Quick search of villagers with their likes, dislikes, schedule, and birthday
- List of fishes, shops, and calendars

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/stardew-valley/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/stardew-valley)


### Setup guide

The setup and deploy guide is up to date with version `6.2.5`

1. Install Angular:

```
npm install -g @angular/cli

```
2. Initialization:
```
ng new my-app
```

3. Run Angular:
```
ng serve
```

### Deploy to Github Pages

#### Prerequisites
1. Go to Github Pages at `https://github.com/<github_user>/<repo>/settings/pages`.
2. Select `master` branch with `/(root)` and save.
3. Install `angular-cli-pages`
```
npm i angular-cli-ghpages --save-dev
```

#### Deployment
Run these commands:
```
ng build --prod --base-href https://<github_user>.github.io/<repo>/
ngh --branch=master
```

### Official guides
- <a href="https://v6.angular.io/guide/quickstart" target="_blank">Installation</a>
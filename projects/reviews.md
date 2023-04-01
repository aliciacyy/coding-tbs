---
label: Reviews - VuePress
---

### Project summary

A site to consolidate personal hotel experiences (may expand to other areas too) using <a href="https://v2.vuepress.vuejs.org/" target="_blank">VuePress</a>.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/reviews/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/reviews)


### Setup guide

The setup and deploy guide is up to date with version `2.0.0-beta.61`

1. Initialization:

```
npm install -g pnpm 
npm init
pnpm add -D @vuepress/client@next vue
```

2. Run:
```
pnpm run docs:dev
```

### Deploy to Github Pages

#### Prerequisites

1. Set the site and, if needed, base options in `doc/.vuepress/config.js`.
```config.js.
export default {
  base: "/reviews/"
}
```

2. Create `.github/workflows` folder in the project root directory.

3. Create a file `docs.yml` and add it to the folder.

``` .github/workflows/docs.yml
name: docs

on:
  # trigger deployment on every push to main branch
  push:
    branches: [main]
  # trigger deployment manually
  workflow_dispatch:

jobs:
  docs:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
        with:
          # fetch all commits to get last updated time or other git log info
          fetch-depth: 0

      - name: Setup pnpm
        uses: pnpm/action-setup@v2
        with:
          # choose pnpm version to use
          version: 7
          # install deps with pnpm
          run_install: true

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          # choose node.js version to use
          node-version: 18
          # cache deps for pnpm
          cache: pnpm

      # run build script
      - name: Build VuePress site
        run: pnpm docs:build

      # please check out the docs of the workflow for more details
      # @see https://github.com/crazy-max/ghaction-github-pages
      - name: Deploy to GitHub Pages
        uses: crazy-max/ghaction-github-pages@v2
        with:
          # deploy to gh-pages branch
          target_branch: gh-pages
          # deploy the default output dir of VuePress
          build_dir: docs/.vuepress/dist
        env:
          # @see https://docs.github.com/en/actions/reference/authentication-in-a-workflow#about-the-github_token-secret
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

4. Commit the new workflow file and push it to GitHub.

#### Deployment
Github Pages will be automatically deployed whenever changes are pushed to the branch due to Github Actions.

### Troubleshooting

#### No matching version found for vuepress-vite@2.0.0-beta.50-pre.1.

Fix by removing `^` to fix the version

```
"vuepress": "2.0.0-beta.61"
```

#### Adding sidebars
Refer to these:
- https://vuepress.github.io/reference/default-theme/config.html#sidebar
- https://techformist.com/automatic-dynamic-sidebar-vuepress/

### Official guides
- <a href="https://vuepress.github.io/guide/deployment.html" target="_blank">Deployment</a>
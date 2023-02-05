---
label: Personality - Astro
---

### Project summary

A site to document results and explanations of personality related quizzes using <a href="https://astro.build/" target="_blank">Astro</a>.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/personality/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/personality)


### Setup guide

The setup and deploy guide is up to date with version `2.0.6`

1. Initialization:

Using a theme e.g. https://astro.build/themes/details/docs/
```
npm create astro@latest -- --template docs
```

2. Run:
```
npm run dev
```

### Deploy to Github Pages

#### Prerequisites

1. Set the site and, if needed, base options in astro.config.mjs.
```astro.config.mjs.
import { defineConfig } from 'astro/config'

export default defineConfig({
  site: 'https://{your-username}.github.io',
  base: '/my-repo',
})
```

2. Create `.github/workflows` folder in the project root directory.

3. Create a file `deploy.yml` and add it to the folder.

``` .github/workflows/deploy.yml
name: Deploy to GitHub Pages

on:
  # Trigger the workflow every time you push to the `main` branch
  # Using a different branch name? Replace `main` with your branch’s name
  push:
    branches: [ main ]
  # Allows you to run this workflow manually from the Actions tab on GitHub.
  workflow_dispatch:
  
# Allow this job to clone the repo and create a page deployment
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v3
      - name: Install, build, and upload your site
        uses: withastro/action@v0
        # with:
            # path: . # The root location of your Astro project inside the repository. (optional)
            # node-version: 16 # The specific version of Node that should be used to build your site. Defaults to 16. (optional)
            # package-manager: yarn # The Node package manager that should be used to install dependencies and build your site. Automatically detected based on your lockfile. (optional)

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

4. On GitHub, go to your repository’s Settings tab and find the Pages section of the settings.
5. Choose GitHub Actions as the Source of your site.
6. Commit the new workflow file and push it to GitHub.

#### Deployment
Github Pages will be automatically deployed whenever changes are pushed to the branch due to Github Actions.


### Official guides
- <a href="https://docs.astro.build/en/guides/deploy/github/" target="_blank">Deploying to Github Pages</a>
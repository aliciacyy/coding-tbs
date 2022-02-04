---
label: Hiking - Gatsby
---

### Project summary

Recording my hiking adventures in Singapore using <a href="https://www.gatsbyjs.com/" target="_blank">Gatsby</a>.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/hiking/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/hiking)

### Setup guide

The setup and deploy guide is up to date with version `2.25.3`

1. Install Gatsby:

```
npm install -g gatsby-cli
```

2. Initialization:
```
gatsby new <name> https://github.com/gatsbyjs/gatsby-starter-blog
```

3. Run Gatsby:
```
gatsby develop
```

### Deploy to Github Pages

#### Prerequisites
1. Install Github Pages package

```
npm install gh-pages --save-dev
```

2. Add `pathPrefix` to your `gatsby-config.js`.
``` ./gatsby-config.js.
module.exports = {
  pathPrefix: `/<repo>`,
}
```
3. Add `deploy` to `package.json`.
``` ./package.json
{
  "scripts": {
    "deploy": "gatsby build --prefix-paths && gh-pages -d public"
  }
}
```
3. Go to Github Pages at `https://github.com/<github_user>/<repo>/settings/pages`.
4. Select `gh-pages` branch with `/(root)` and save.

#### Deployment
Run the following:
```
npm run deploy
```

### Official guides
- <a href="https://v2.gatsbyjs.com/docs/quick-start/" target="_blank">Installation</a>
- <a href="https://www.gatsbyjs.com/docs/how-to/previews-deploys-hosting/how-gatsby-works-with-github-pages/" target="_blank">Deploying to Github Pages</a>
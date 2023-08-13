---
label: Games Cafe - React 18
---

### Project summary

A simple website designed for an imaginary games cafe company using React 18 and Tailwind.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://aliciacyy.github.io/games-cafe/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/games-cafe)


### Setup guide

Set up using <a href="https://create-react-app.dev/" target="_blank">Create React App</a>.

```
npx create-react-app my-app
```

To run:
```
npm run start
```

### Deploy to Github Pages

Use <a href="https://github.com/gitname/react-gh-pages" target="_blank">react-gh-pages</a>.

#### Pre-requisites
1. Install
```
$ npm install gh-pages --save-dev
```
2. Add a homepage property in this format*: https://{username}.github.io/{repo-name} in `package.json`

```
  "name": "my-app",
  "version": "0.1.0",
+ "homepage": "https://gitname.github.io/react-gh-pages",
  "private": true,
```
3. Add a `predeploy` property and a `deploy` property to the scripts object:
```
"scripts": {
+   "predeploy": "npm run build",
+   "deploy": "gh-pages -d build",
    "start": "react-scripts start",
    "build": "react-scripts build",
```

#### Deployment
```
npm run deploy
```
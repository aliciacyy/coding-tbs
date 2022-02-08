---
label: Angular
---

Running Angular 13 on node version `v16.13.2` and npm version `v8.4.1`

### npm and Node.js version mismatch

Faced this issue where even though I installed Node.js (LTS version 16.13.2) with Windows Installer, my npm version was stuck at v6.9.0.

#### Error 
`npm does not support Node.js 16.13.2`

#### Solution
1. Delete NPM and NPM-Cache folder (found in `C:\Users\<your_user>\AppData\Roaming`)
2. Run command `npm install -g npm@latest`

Checking npm and nodejs versions: <a href="https://nodejs.org/en/download/releases/" target="_blank">https://nodejs.org/en/download/releases/</a>

**Credit:** <a href="https://stackoverflow.com/a/63337788" target="_blank">https://stackoverflow.com/a/63337788</a>

### Angular CLI version mismatch

#### Error
`Your global Angular CLI version (13.0.4) is greater than your local version (6.2.9).`

#### Solution
Run `npm install --save-dev @angular/cli@13.0.4`

**Credit:** <a href="https://stackoverflow.com/a/46664270" target="_blank">https://stackoverflow.com/a/46664270</a>

### ng build error

Got this error when running `ng build --prod --base-href "https://GithubUserName.github.io/GithubRepoName/"`.

#### Error 
```
./src/polyfills.ts - Error: Module build failed (from ./node_modules/@ngtools/webpack/src/ivy/index.js):
Transform failed with 1 error:
error: Invalid version: "15.2-15.3"

./src/styles.css - Error: Module build failed (from ./node_modules/mini-css-extract-plugin/dist/loader.js):
HookWebpackError: Module build failed (from ./node_modules/@ngtools/webpack/src/ivy/index.js):
Transform failed with 1 error:
error: Invalid version: "15.2-15.3"
```

#### Solution
Replace the content of `.browserslistrc` with the following:
``` ./.browserslistrc
# This file is used by the build system to adjust CSS and JS output to support the specified browsers below.
# For additional information regarding the format and rule options, please see:
# https://github.com/browserslist/browserslist#queries

# For the full list of supported browsers by the Angular framework, please see:
# https://angular.io/guide/browser-support

# You can see what browsers were selected by your queries by running:
#   npx browserslist

last 1 Chrome version
last 1 Firefox version
last 2 Edge major versions
last 2 Safari major versions
last 2 iOS major versions
Firefox ESR
not IE 9-10 # Angular support for IE 9-10 has been deprecated and will be removed as of Angular v11. To opt-in, remove the 'not' prefix on this line.
not IE 11 # Angular supports IE 11 only as an opt-in. To opt-in, remove the 'not' prefix on this line.
not ios_saf 15.2-15.3
not safari 15.2-15.3
```

**Credit:** <a href="https://github.com/angular/angular-cli/issues/22606#issuecomment-1025206301" target="_blank">https://github.com/angular/angular-cli/issues/22606#issuecomment-1025206301</a>

### Using Foundation with Angular 13

Faced several errors while trying to use <a href="https://get.foundation/sites/docs/index.html" target="_blank">Foundation</a> JS with Angular.

#### Error
```
Cannot find name '$'. Do you need to install type definitions for jQuery? Try `npm i --save-dev @types/jquery` and then add 'jquery' to the types field in your tsconfig.
Property 'foundation' does not exist on type 'JQuery<Document>'
Cannot find name '$'. Do you need to instae types field in your tsconfig.
```

#### Solution
1. Run the following:
```
npm install foundation-sites
npm i --save-dev @types/jquery

```
2. In `polyfills.ts`, add this line: 
```./src/polyfills.ts
import 'jquery';
```
3. In `angular.json`, add the CSS and JS files:
```./angular.json
"styles": [
  "node_modules/foundation-sites/dist/css/foundation.min.css",
  "src/styles.css"
],
"scripts": [
  "node_modules/jquery/dist/jquery.min.js",
  "node_modules/foundation-sites/dist/js/foundation.min.js"
]
```
4. In `app.component.ts`, add this to make components work:
``` ./src/app/app.component.ts
ngOnInit() {
  (<any>$(document)).foundation();
}
```

**Credit:** 
- <a href="https://stackoverflow.com/a/52228633" target="_blank">Integrating instructions</a>
- <a href="https://stackoverflow.com/a/24984067" target="_blank">Property does not exist</a>

### 'string' can't be used to index type '{}'

#### Error
```
'string' can't be used to index type '{}'
```

#### Solution
Define the type as such:
```
 items: {
   [key: string]: number | string,
  }[]
```

**Credit:**  <a href="https://stackoverflow.com/a/57350191" target="_blank">https://stackoverflow.com/a/57350191</a>
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

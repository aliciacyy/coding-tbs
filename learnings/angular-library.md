---
label: Creating Angular Library
---

### Create an application
Can remove the front part if you do not need a different version from your CLI.

`npx -p @angular/cli@16.2.14 ng new my-shared-workspace --no-create-application`

or

`npx -p @angular/cli@16.2.14 ng new my-shared-workspace --create-application=false`

### Create library
`ng generate library <library-name>`

### Adding scope
Go to project's package.json and edit the name:
```
{
  "name": "@my-company/my-buttons",
  "version": "0.0.1",
  ...
}
```

### Create components
Do `cd` to the library directory first (e.g projects/<library-name>/src/lib/)

`ng g c components/button`

Then add to `public-apis.ts`

`export * from '...'`

### Build library
`ng build <library-name>`

Can add to package.json to make it easier to run the build command

### Package library
`cd` to `dist/<library-name>/` and run `npm pack`

Can also add to package.json - `"pack-lib": "cd dist/<library-name> && npm pack"`

### To install in other apps
- Copy the tgz package over to the root folder of the app
- Run `npm i <library-name>-1.2.3.tgz`
- Add the module in `AppModule`

### Using npm-link

Use this to save the trouble of having to run build and copying the file over every time.

- `cd` to `dist/<library-name>/` and run `npm link`
- In your app, add the dependency in package.json
- Then run `npm link <library-name>`

### Removing link
```
npm unlink <library-name> --no-save
npm rm -g <library-name>
```

### Installing dependencies on library
In the root `package.json`, add this:
```
"workspaces": [
  "projects/*"
]
```

This ensures that `npm install` is only executed at the root level.

When dependencies are installed, add them to `peerDependecies` manually.

Example:

In root package.json:
```
"primeng": "^16.4.4",
```

In library package.json:
```
"peerDependencies": {
  "@angular/common": "^16.2.0",
  "@angular/core": "^16.2.0",
  "primeng": "^16.4.4"
},
```


### Adding Storybook

`npx sb init` on root level.

Remember to do the above, or else Storybook will have this error: `Cannot read property 'selector' of undefined.` if there is `node_modules` folder in the `projects/<lib-name>` level.

### Adding third party CSS in Storybook

In the root `angular.json`, add styles here:
```
"storybook": {
  "builder": "@storybook/angular:start-storybook",
  "options": {
  "styles": [
    "node_modules/primeng/resources/primeng.min.css",
    "node_modules/primeng/resources/themes/lara-light-blue/theme.css"
  ],
  "configDir": "projects/piggy-ui/.storybook",
  "browserTarget": "piggy-ui:build",
  "compodoc": true,
  "compodocArgs": ["-e", "json", "-d", "projects/piggy-ui"],
  "port": 6006
  }
},
```

### Creating own theme in PrimeNg and exporting

1. Download zip file from [here](https://github.com/primefaces/primeng-sass-theme/releases)
2. Copy the `theme-base` and `theme/mytheme` folders
3. Update the import in `theme/mytheme/theme.scss` for this line: `@import '../theme-base/_components';`
4. Run `sass --update themes/pig-ui/theme.scss:projects/piggy-ui/src/themes/pigui.min.css --style compressed`
5. Add this in `ng-package.json`:
```
"assets": [
  { "input": "src/themes", "glob": "**/*.css", "output": "themes" }
]
```

Now the css file will be in the library package.

Add this to the app using the library in `angular.json`

```
"styles": [
  "src/styles.scss",
  "node_modules/piggy-ui/themes/pigui.min.css",
  "node_modules/primeng/resources/primeng.min.css"
],
```

### Adding Tailwind to library

1. Install tailwind at root
```
npm install -D tailwindcss
npx tailwindcss init
```
2. Update `tailwind.config.js`
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./projects/libilb/src/**/*.{html,ts}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
3. Create `input.css`
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
4. Run command
```
npx tailwindcss -i ./css/input.css -o ./css/output.css --watch
```
5. Add to angular.json
```
"styles": [
  "node_modules/primeng/resources/primeng.min.css",
  "projects/libilb/src/themes/libilb.min.css",
  "css/output.css"
],
```
Old instructions, might not be needed?

6. Install storybook dependency in library directory
```
npx storybook@latest add @storybook/addon-styling-webpack
```

### References
- https://www.telerik.com/blogs/angular-component-library-part-1-how-to-build
- https://medium.com/angular-in-depth/step-by-step-guide-to-creating-your-first-library-in-angular-6827276bfc9f
- https://medium.com/@aleksanderkolata/how-to-develop-angular-libraries-locally-ed8e1fd16892
- https://plainenglish.io/blog/create-your-own-angular-component-library-e5f062b902a8
- https://github.com/storybookjs/storybook/issues/14828
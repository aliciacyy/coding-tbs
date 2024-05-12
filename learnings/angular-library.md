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


### References
- https://www.telerik.com/blogs/angular-component-library-part-1-how-to-build
- https://medium.com/angular-in-depth/step-by-step-guide-to-creating-your-first-library-in-angular-6827276bfc9f
- https://medium.com/@aleksanderkolata/how-to-develop-angular-libraries-locally-ed8e1fd16892
- https://plainenglish.io/blog/create-your-own-angular-component-library-e5f062b902a8
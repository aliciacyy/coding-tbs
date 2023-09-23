---
label: Firebase Hosting
---

# Steps

1. Install Firebase CLI
```
npm install firebase
npm install -g firebase-tools
```

2. Login to Firebase
```
firebase login --interactive
```

3. Init firebase
```
firebase init

? Are you ready to proceed? Yes
? Which Firebase features do you want to set up for this directory? Press Space to select features, then Enter to
confirm your choices. Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys

? What do you want to use as your public directory? build
? Configure as a single-page app (rewrite all urls to /index.html)? Yes
? Set up automatic builds and deploys with GitHub? No
? File build/index.html already exists. Overwrite? No
i  Skipping write of build/index.html

i  Writing configuration info to firebase.json...
i  Writing project information to .firebaserc...

+  Firebase initialization complete!
```

4. Deploying
```
npm run build
firebase deploy
```
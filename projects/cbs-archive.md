---
label: CBS Archive- Next.js, Supabase
---

### Project summary

A website to save archive links of past Clues by Sam links and optionally keeping tracking which ones are done if logged in with a user account.

#### :globe_with_meridians: Page

[!ref icon=":globe_with_meridians:" target="blank"](https://cbs-archive.vercel.app/)

#### :icon-mark-github: Github repository

[!ref icon=":rocket:" target="blank"](https://github.com/aliciacyy/cbs-archive)

### Setup guide

#### Running Next.js app

1. Install dependecies:

```
npm install
```

2. Run dev

```
npm run dev
```

#### Running Python script

The script is used to get the link of the archive and saving into Supabase's database.

```
source venv/bin/activate
python main.py
```

### Deployment

Done using Vercel.

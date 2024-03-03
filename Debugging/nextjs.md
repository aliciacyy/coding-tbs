---
label: Next.js
---

### Minified React error

#### Error
![](/static/nextjs1.png)

#### Solution
Remove 'use client' from the main page.

### Deploying to Github Pages

This happened with Next.js version `14.1.1` with the app directory.

#### Error 
On Upload artifact stage during Github Actions:
```
 tar: out: Cannot open: No such file or directory
 tar: Error is not recoverable: exiting now
 Error: Process completed with exit code 2.
```

#### Solution
1. Change `next.config.mjs` to `next.config.js`
2. Change the content to the following:
```
/** @type {import('next').NextConfig} */
const nextConfig = {
  basePath: '/{your repo name}',
  output: 'export',
  images: {
    unoptimized: true,
  }
};

module.exports = nextConfig
```
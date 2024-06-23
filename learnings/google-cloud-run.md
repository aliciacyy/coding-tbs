---
label: Google Cloud Run
---

### Setup

1. Install gcloud client from https://cloud.google.com/sdk/docs/install by downloading the package.
2. Extract the package
3. In the same directory as the unzipped package, run `./google-cloud-sdk/install.sh`
4. Run `gcloud init`

### Artifact Registry
```
gcloud auth configure-docker \
    asia-southeast1-docker.pkg.dev
```

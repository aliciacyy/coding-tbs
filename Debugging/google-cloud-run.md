---
label: Google Cloud Run
---

### textPayload: "terminated: Application failed to start: failed to load /usr/local/bin/docker-entrypoint.sh: exec format error"

Faced this issue when trying to run a Docker image in Google Cloud Run on Macbook Pro M3.

#### Solution
Use this command when building image:
`docker build --platform=linux/amd64 -t pigster/angularssr:0.2.0 .`

**Credit:** <a href="https://stackoverflow.com/questions/73398714/docker-fails-when-building-on-m1-macs-exec-usr-local-bin-docker-entrypoint-sh" target="_blank">https://stackoverflow.com/questions/73398714/docker-fails-when-building-on-m1-macs-exec-usr-local-bin-docker-entrypoint-sh</a>

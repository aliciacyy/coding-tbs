---
label: docker
---

## Running Docker
### Build image
`docker build -t pigster/angularssr:0.2.0 .`

If building with Macbook M1 for Google Cloud Run, use this command instead:
`docker build --platform=linux/amd64 -t pigster/angularssr:0.2.0 .`

### Run on local Docker
`docker run -p 4201:4000 pigster/angularssr:0.2.0`

### Publish

#### Docker Hub
`docker push pigster/angularssr:0.2.0`

#### Google Artifact Registry
![](/static/artifact1.jpg)

`docker tag pigster/angularssr:0.2.0 {copied_path}/pigster/angularssr:0.2.0`

`docker push {copied_path}/pigster/angularssr:0.2.0`


## Dockerfile for Angular

### Usual
```
FROM node:18 as angular

WORKDIR /app

COPY . .
RUN npm install -g @angular/cli
RUN npm install

CMD ["ng", "serve", "--host", "0.0.0.0"]

# Replace above for SSR
# CMD ["npm", "run", "dev:ssr"]

```

### For SSR production
```
FROM node:18 as build

WORKDIR /app

COPY . .
RUN npm install
RUN npm run build:ssr

FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY --from=build /app/dist /app/dist

EXPOSE 4000

CMD ["npm", "run", "serve:ssr"]
```

### For Storybook production
```
FROM node:18 as build

WORKDIR /app

COPY . .
RUN npm install
RUN npm run build-storybook

FROM node:18

RUN npm install -g http-server
# npx http-server ./storybook-static

COPY --from=build /app/storybook-static /storybook-static

EXPOSE 8080

# Serve the static files
CMD ["http-server", "/storybook-static", "-p", "8080"]
```

## .dockerignore
```
node_modules
dist
```
# create-svelte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm init svelte@next

# create a new project in my-app
npm init svelte@next my-app
```

> Note: the `@next` is temporary

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs#adapters) for your target environment.

## Docker (podman)

## Build 

Currently adapter-node is used. In order to build container image following command have to be issued: 

```bash
# in project directory execute 
podman build -f docker/Dockerfile -t kit-demo .
# use --no-cache to build completely dropping previous cache
podman build --no-cache -f docker/Dockerfile -t kit-demo . 

# expected output 
$ podman build --no-cache -f docker/Dockerfile -t kit-demo .
[1/2] STEP 1/7: FROM registry.access.redhat.com/ubi8/nodejs-16:latest AS builder
[1/2] STEP 2/7: RUN npm install -g pnpm
..
Successfully tagged localhost/kit-demo:latest
f4566121228fa59e55e176da24726413b17d26296eeb1fabb2ef6ddc7223a12f
```
### Running 

In order to start named container with newly created image use:

```bash
podman run -d --name kit-demo -p 3000:3000 kit-demo

```


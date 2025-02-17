---
id: 64f0e2d5-2c83-43df-9144-40f2c68935aa
title: Setup Dendron Development Environment
desc: ''
updated: 1631232697632
created: 1598651458825
---

## Build

### Prerequisites

Before you begin, you need to make sure to have the following SDKs and tools:

- [Node.js >= 12.0.0](https://nodejs.org/download/release/latest-v10.x/)
  - We recommend using a version in [Active LTS](https://nodejs.org/en/about/releases/)
- yarn
  - `npm install -g yarn`
- lerna
  - `npm install -g lerna`
- a different instance of VSCode
  - because debugging VSCode by default loads up all extensions that are installed, you'll have issues trying to develop Dendron if you also have VSCode installed . the workaround is to install an alternative flavor of vscode (eg. [insider edition](https://code.visualstudio.com/insiders/)) to use for development 

### Steps

1. Clone ^clone
  ```bash
  git clone https://github.com/dendronhq/dendron.git
  cd dendron
  ```

1. Install dependencies
  ```bash
  # this should install all dependencies
  yarn setup

  # if the above script errors out, you can diagnose the issue and run the following scripts sequentially dependeing on where the error occured
  yarn # install package root dependencies
  yarn bootstrap:bootstrap # install package dependencise
  yarn bootstrap:build  # build package dependencies
  ```
## Run

1. Open the workspace.  At the root of the monorepo, open `dendron-main.code-workspace`. Open this with VSCode to start editing. While its not required to use VSCode, most of the helper scripts in this repository are created with VSCode in mind so using it will make development significantly easier.
2. Debug
  - NOTE: you don't need to do this if you are not directly working on the extension (eg. you're working on the [[server|pkg.dendron-next-server]])

To start an instance of the Dendron with the Debugger, Run `Extension: Local (plugin-core)` from the debug panel in vscode

![debugger](/assets/images/start_debugger.gif)

_Note: Running via Run -> Start Debugging will not work unless you've previously targeted `Extension: Local (plugin-core)`_

_Note: To have the changes reflected as you edit the code you need to run the `./bootstrap/scripts/watch.sh` and restart the `Extension: Local (plugin-core)`)_

## Remote Development 

If you are developing Dendron in a remote environment using VSCode, see additional instructions [[here|dendron.dev.remote]].


## Normal Workflow

1. Checkout a feature branch for your task
1. Work on code
1. Submit a [[pull Request|dendron.dev.pull-request]] 

## Logging

Logs are important for debugging and we should strive to have logs that will give enough information that we can debug any errors from the logs alone. Because we're dealing with users personal notes, we also need to ensure not to log any sensitive information.

If you need to log data, use one of the following loggers depending on what package you are in:
- plugin-core: use [Logger](https://github.com/dendronhq/dendron/blob/master/packages/plugin-core/src/logger.ts#L22:L22)
- react component: use [createLogger](https://github.com/dendronhq/dendron/blob/master/packages/common-frontend/src/utils/logger.ts#L3:L3) in common-frontend
- everything else: use [createLogger](https://github.com/dendronhq/dendron/blob/master/packages/common-server/src/logger.ts#L36:L36) in common-server

Also note that many objects (eg. commands, pods, etc), have an instance of the logger attached to them. You should use them whenever available. They are usually attached as a `.L` or `.logger` property. 
- pods have loggers attached in `this.L`

Some things to keep in mind:
  - Do not use `console.log` to log data
  - Raw note objects contain note content which we never want to log. Instead, use [`NoteUtils.toLogObj`](https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/dnode.ts) which strips out sensitive fields to the logger. 

## Exceptions

When handling a Dendron specific error, use the [DendronError](https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/error.ts) class

Some things to keep in mind:
  - when returning an error from the server, note that you'll need to convert the error to a plain object using [error2PlainObject](https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/error.ts#L110)
  - when displaying an error in a string, you'll need to convert the error using [stringifyError](https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/error.ts#L106:L106)
  - whenever possible, attach a [status](https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/constants.ts#L18:L18) to an error
  - whenever possible, attach a [severity](https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/constants.ts#L45) to an error

## Project Specific Docs
### Working with the API Server

Dendron connects to a local express server which is responsible for indexing your notes. This express server also serves up static files generated by [[Dendron Next Server|pkg.dendron-next-server]]. 

Dendron compiles the static assets from the next server to the express server during publication so that everything is bundled when published. When you are developing, you can launch the next server independently for faster development. You can follow the instructions [[here|pkg.dendron-next-server.quickstart]] to start the next-server.

To start Dendron with the next server active, you can set the following value in `dendron.yml`

```yml
dev:
  nextServerUrl: "http://localhost:3000"
```

### Working with the CLI

Symlink `dendron` 

```sh
cd packages/dendorn-cli
npm link

npm link -g @dendronhq/dendron-cli
```

## Advanced

### Verdaccio

![[dendron.dev.cook.common#verdaccio,1:#*]]

### Linking all Packages

This goes over symlinking all packages locally. This requires that the `meta.json` file be generated. It is created as part of `yarn lerna:bootstrap`.

```sh
node bootstrap/scripts/linkAll.js
```

## Tips

### Watch Monorepo

To continuously compile all dependencies, run the following

```bash
./bootstrap/scripts/watch.sh
```

### Adding dependencies

When you are merging new changes, note that new dependencies and sometimes packages will be installed. 

#### New Dependencies
```sh
# install all new dependencies
lerna bootstrap
```

#### New Package in Dendron Mono Repo
Adding new packages is a rarer event but might require a workspace rebuild

```sh
# clean up old files (this might take a few minutes)
./bootstrap/scripts/cleanup.sh

# install all dependencies
lerna bootstrap

# build all dependencies
./bootstrap/scripts/build.sh
```


## Troubleshooting

### Something went wrong during the build

In case something something goes wrong with a build step or you want to save time by not running everything, `init.sh` is just a thin wrapper around the following scripts, each of which can be run individually

- ./bootstrap/scripts/bootstrap.sh: `lerna bootstrap all packages`
- ./bootstrap/scripts/build.sh: `lerna build all packages`

### Changes not showing up in Dendron

1. Are you using the `Run extension` command on the debugger panel to test dendron? 

2. If you have one vscode instance which you have dendron installed and are also doing dendron development on, you might get a version conflict. in that case, use `Run extension with plugin disabled` in the debugger panel (or use a different version of vscode to run dendron vs develop)

### Husky Hooks not running

Make sure you run `yarn` at the root of your workspace 

## Getting Help

Dendron is actively being developed and it could be quite confusing to start developing for the first time. In this case, we recommend asking for help with whatever blockers you might have with setting up or understanding part of the codebase.

Generally, a member of the Dendron team or the community will chime in for help if you post a specific question in the `#dev` channel in our Discord server.

For more information, check out our handbook entry on `Getting help for development` described [here](https://handbook.dendron.so/notes/bHWjVTtdOCMMRd2_QD0tb.html)

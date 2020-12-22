---
id: 3abd00eb-1c1e-4253-aaf5-dcbe20c21850
title: Early Seed
desc: ''
updated: 1608584127160
created: 1604539200840
---

## 0.20.2

### Features

#### Publishing For Multi Vault

((ref: [[dendron.topic.multi-vault]]#publishing,1))

### Enhancements
- creating engine via cli also initializes meta files ([d72f097](https://github.com/dendronhq/dendron/commit/d72f097e63d1fda065ac7ad50f85bebe99d6da66))([[docs|dendron.pro.dendron-cli#launchengineserver]])
- remove github light theme from dendron bundle ([33d5708](https://github.com/dendronhq/dendron/commit/33d57086510cdaefbb8af8f72c945d6f5e02be5c))
- support [[note refs for multi-vault|dendron.topic.multi-vault#note-references]] 
- support relative links in dendron preview ([[docs|dendron.topic.links#wiki-links]])
- further speed enhancements to publishing using 11ty resulting in another 5x improvement  
- configure [[writeStubs|dendron.topic.publishingv2.configuration#writestubs-optional]] from `dendron.yml`


### Bug Fixes
- refactor hiearchy miss self referential links ([00b385d](https://github.com/dendronhq/dendron/commit/00b385dd0d13e5809da012bbc88388886012b837))
- reduce frequency of `engine not connecting` error when launching dendron preview

### House Cleaning
- [[writeStubs|dendron.topic.publishingv2.configuration#writestubs-optional]] is set to `true` by default (or when not set) when publishing using 11ty


## 0.20.1

### Publishing V2 (preview)

We've re-build publishing for Dendron from the ground up to be faster, better, and easier to use.

Besides for schemas, publishing has consistently been one of the hardest to use features in Dendron. Dendron currently publishes using [jekyll](https://jekyllrb.com/) using our own [template](https://github.com/dendronhq/dendron-jekyll). While this has served as well initially, slow compile times for large sites and difficulty of getting started has made it a growing pain point.

To address this, we've migrated our publishing stack to [11ty](https://www.11ty.dev/), a super fast javascript based static generator. This means much faster, and perhaps more importantly, easier publishing. 

There's still some work left to integrate publishing into the Dendron plugin - meanwhile, you can take the new publishing workflow for a spin using the [[dendron cli|dendron.pro.dendron-cli]]

In order to to use the 11ty based publishing, initialize your workspace with the following commands.

```bash
npm init -y
npm install @dendronhq/dendron-cli@latest
npm install @dendronhq/dendron-11ty@latest
```

After you have your dependencies installed, build your your site using the following command.

```bash
npx dendron-cli buildSiteV2 --wsRoot .  --stage dev --serve
```

This will both compile your site locally and make it available at `localhost:8080` for instant preview. When building your site locally, the pages will be build to `{wsRoot}/build/site`. 


When you are ready to publish to github, make sure to change the stage to `prod`.

```bash
npx dendron-cli buildSiteV2 --wsRoot .  --stage prod 
```

This will build your site to the path specified by [[siteRootDir|dendron.topic.publishing.configuration#siterootdir]] in `dendron.yml`. 

#### Benchmarks

Publishing V2 is ~10x faster than jekyll based publishing for sites with +100 pages. For comparison, below is the compilation difference between building the dendron site using 11ty vs jekyll. 

- 11ty: 24.45s
- jekyll: 220.33s

There are additional optimizations still on the table that will further drive down he compilation time by another order of magnitude for future releases. 

#### Gaps

11ty publishing is currently not at full feature parity with Jekyll publishing. Notably, the following features are missing:
- setting a custom color theme
- `edit on github` links
- `jekyll-seo` functionality
- mathjax

#### Migration

All values that used to be written into `_config.yml` will now be moved into `dendron.yml`. You can see the currently supported configuration values here: `https://github.com/dendronhq/dendron/blob/master/packages/common-all/src/types.ts#L71:L71`

If you currently have a Jekyll based Dendron page, note that the following settings have changed:
- the `url` property from `_config.yml` is now `siteUrl` in `dendron.yml`
- favicon is now controlled by `siteFaviconPath` in `dendron.yml` and is a path relative to your workspace root
- `CNAME` is now controlled by `githubCname` property in `dendron.yml`

#### Sample dendron.yml config
- publishing without a cname
```yml
version: 1
vaults:
    - fsPath: vault
site:
    copyAssets: true
    siteHierarchies:
        - dendron
    siteRootDir: docs
    siteUrl: "kevinslin.github.io/dendron-11ty-test"
    usePrettyRefs: true
```

- using custom cname
```yml
version: 1
vaults:
    - fsPath: vault
site:
    copyAssets: true
    siteHierarchies:
        - dendron
    siteRootDir: docs
    usePrettyRefs: true
    siteUrl: "11ty.dendron.so"
    githubCname: "11ty.dendron.so"
```

#### Sample repo
- [github repo](https://github.com/kevinslin/dendron-11ty-test/deployments/activity_log?environment=github-pages)
- [github page](https://kevinslin.github.io/dendron-11ty-test/)

#### CLI Command Reference

```bash
dendron-cli buildSiteV2

build notes for publication using 11ty

Options:
  --version  Show version number                                       [boolean]
  --help     Show help                                                 [boolean]
  --wsRoot   location of workspace                                    [required]
  --vaults   location of vault                                           [array]
  --serve    serve over local http server             [boolean] [default: false]
  --stage    serve over local http server
```


<!-- https://hacks.mozilla.org/2020/10/to-eleventy-and-beyond/ -->
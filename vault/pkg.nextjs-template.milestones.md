---
id: wnjZiTP1UEW9e0aGz1HT0
title: Milestones
desc: ''
updated: 1632198708756
created: 1629514021198
---

## MVP Milestones

The NextJS Template is currently in Developer Preview. 

See [here](https://handbook.dendron.so/notes/0292b34e-47eb-4499-8f49-d9891accdb3d.html) for explanation of status symbols

### Features
- [x] Handle navigating to home page
- [x] Fixed Header
- [x] SEO options
- [x] Edit on Github Link
- [x] Responsive side bar 
- ***
- w Advanced SEO Options 
- a Custom Theming Support
- w [[Full text search|scratch.2021.09.05.210615.full-text-search]]
-   [[Support live local preview for publishing|dendron.rfc.21-modern-web-client#3-support-live-local-preview-for-publishing]]
- [ ] Support optimized mobile experience

### Enhancements
- [x] Make Lookup change value when navigating
- [x] Make Breadcrumb clickable 
- [x] make naked urls the default for nextjs
- support mvp config settings
  - [x] support [[assetsPrefix|dendron.topic.publishing.configuration#assetsprefix]]
  - [x] support [[copyAssets|dendron.topic.publishing.configuration#copyassets]]
  - [x] support [[customHeaderPath|dendron.topic.publishing.configuration#customheaderpath]] #size.small 
  - [x] support [[duplicateNoteBehavior|dendron.topic.publishing.configuration#duplicatenotebehavior]]
  - [x] @joshi support [[ga_tracking|dendron.topic.publishing.configuration#ga_tracking]] #size.small   ^gUoZRr5ALw4Z 
  - [x] support [[logo|dendron.topic.publishing.configuration#logo]]
  - [x] support [[githubCname|dendron.topic.publishing.configuration#githubcname]] ^MlGtBGkqaWAn
  - d support [[siteFaviconPath|dendron.topic.publishing.configuration#sitefaviconpath]]
  - [x] support [[siteHierarchies|dendron.topic.publishing.configuration#sitehierarchies]]
  - [x] support [[siteIndex|dendron.topic.publishing.configuration#siteindex]]
  - [x] support [[siteUrl|dendron.topic.publishing.configuration#siteurl]]
  - [x] support [[usePrettyRefs|dendron.topic.publishing.configuration#useprettyrefs]] #assigned
  - [x] support [[gh_edit_repository|dendron.topic.publishing.configuration#gh_edit_repository]]
- SEO options
  - see [Introducing next-seo, SEO for Next.js](https://www.garymeehan.ie/blog/seo-in-nextjs-with-next-seo)
  -   support [[author|dendron.topic.publishing.configuration#author]] seo property #size.small
  -   support [[twitter|dendron.topic.publishing.configuration#twitter]] seo property #size.small
  - [x] support [[image|dendron.topic.publishing.configuration#image]]
- Note config
  - [x] support [[canonicalUrl|dendron.topic.publishing.configuration#canonicalurl]] #size.small
  -   support [[published|dendron.topic.publishing.configuration#published]] #size.small
  -   support [[noindex|dendron.topic.publishing.configuration#noindex]] #size.small
  -   support [[gitNoLink|dendron.topic.publishing.configuration#gitnolink]] #size.small
- [x] @hikchoi support [[collection options|dendron.topic.publishing.configuration#collection-options]] #size.small #scope.publish ^lQkPH1vG6gzd
- [x] Support nav order in Single Hiearchy Workspaces
- [x] Set max-width constraints for content 
- [x] Navigate to home page using `nextjs/link` instead of `<a>` 
- [x] integarte nextjs with [[pkg.dendron-cli]] 
- [ ] integarte nextjs with [[pkg.dendron-plugin]]

### Fixes
- [x] Deeply nested tree view items can overflow 
- [x] Backlinks and Children links go to wrong url 
- [x] Internal links go to wrong url  
- [x] Opening one child of tree view should not close existing children

## Phase I Milestones

### Features
- support tab completion for lookup
- support note graph on published site
- support internationalization

### Enhancements
-   support site map using [iamvishnusankar/next-sitemap](https://github.com/iamvishnusankar/next-sitemap#readme) ^cf6Jxkyn3rku
- support all config settings
  -   support [[previewPort|dendron.topic.publishing.configuration#previewport]]

## Future Milestones
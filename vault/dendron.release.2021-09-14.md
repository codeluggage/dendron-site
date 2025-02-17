---
id: aURuqCucZegsCpJSb5m90
title: Release Notes (version 0.59)
desc: ''
updated: 1631679038644
created: 1631659388102
---

Dendron 0.59 has sprouted  🌱

### Highlights
- feat(publish): publish using next and github pages ([[docs|dendron.topic.images#extended-images]])
- feat(markdown): custom css for images ([[docs|dendron.topic.publishing-next.cook.github#summary]])
- enhance(pods) markdown import to update asset links

### Everything Else
- enhance(publish) support `assetPrefix` option with nextjs publishing
- enhance(publish) initialize nextjs template with `https` protocol 
- enhance(publish) autoset sane defaults for nextjs publishing
- enhance(publish) unpublished notes replaced with link to [[unpublished pages|dendron.ref.unpublished-pages]]
- enhance(publish) support attach option for CLI ([[docs|dendron.topic.publishing-next.cli#^bfvLB8BY4nLb]])
- enhance(lookup) "Create New" will be first result if no exact match
- enhance(lookup) Disallow toggle of vault selector when using "Move Note" command
- enhance(workspace) Use sentry to track errors  ([[docs|dendron.dev.errors.reporting]])
- fix(lookup) direct children query not filterting all results
- fix(lookup) ignore lookupConfirm if dailyVault is set
- fix(lookup) running move note highlights non-current note
- fix(lookup) running [[directChildOnly|dendron.topic.lookup.modifiers#directchildonly]] filter on root will still show all results
- fix(workspace) stop calendar from auto expanding when the last note is closed 
- fix(workspace) correctly render cross-vault note references in preview v2 
- fix(publish) exclude private vault backlinks when publishing
- fix(markdown) highlight same file wikilinks, wildcard references, links with anchors 
- fix(publish) backlinks respect assetPrefix

### Ongoing 

#### RFCs

We've had quite a number of [[Rfc|dendron.rfc]] in flight. This is a highlight of things that are currently being worked on. Click through the RFCs for more details and link to the github discussion page.

- [[22 Queries|dendron.rfc.22-queries]]
- [[23 Consolidate Configurations|dendron.rfc.23-config-consolidation]]
- [[24 Custom Theming|dendron.rfc.24-custom-theming]]
- [[25 Bdd Light|dendron.rfc.25-bdd-light]]
- [[26 Full Text Search for Publishing|dendron.rfc.26-full-text-search-for-publishing]]
- [[27 Move Header Cmd|dendron.rfc.27-move-header-cmd]]
- [[28 Notifications|dendron.rfc.28-notifications]]
- [[29 Contextual UI|dendron.rfc.29-contextual-ui]]

### Community
#### Office Hours

You can find notes from our latest office hours [[here|dendron.community.office-hours.2021.09.12]]

#### Thank You's

A big **thanks** to the following gardeners that brought up issues, contributions, and fixes to this release :man_farmer: :woman_farmer: 
You can see an overview of all roles [[here|dendron.community.roles]]

- [kzilla](https://github.com/dendronhq/dendron/issues/1312) `@kzilla#8818`
    - #dendron.bugcatcher
    - ['Extension host terminated unexpectedly' - Argdown · Issue #1312 · dendronhq/dendron](https://github.com/dendronhq/dendron/issues/1312)
- [Aleksey Rowan](https://github.com/aleksey-rowan) `@aleksey#5276`
    - [Frontmatter Variable Substitution doesn't work in V2 Preview/Publishing · Issue #1322 · dendronhq/dendron](https://github.com/dendronhq/dendron/issues/1322)
- [Parth Shah](https://github.com/parthmshah1302)
    - [Cannot build site due to dependency error (11ty)  · Issue #1324 · dendronhq/dendron](https://github.com/dendronhq/dendron/issues/1324)


### Changelog
![[dendron.release.changelog#059,1:#058]]



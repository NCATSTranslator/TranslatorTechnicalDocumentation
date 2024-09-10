For contributing to these docs, it is recommended that you clone the repository and then edit the content directory in [Obsidian](https://obsidian/) as a vault.

Setting up the repo for local preview:

```bash
git clone #TODO repo here
cd #TODO folder here
npm i # Install dependencies
npx quartz create # Run a local instance for previewing
```
## Style Guide
### General Formatting

Don't include a top-level `# Title`, instead use either the filename or the frontmatter to contain the title, as Quartz will render the title from either of those. Example frontmatter:

```yaml
---
title: My Fancy Title with the Disallowed '/' character
```


## Notes & Workarounds

- Until https://github.com/jackyzha0/quartz/issues/593 is resolved, to escape tags use `<label>#</label>`

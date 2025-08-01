### 🛠️ To **edit** a tag page

Quartz lets you override the default tag listing by creating a file for each tag inside your `/content/tags/` folder.

For example, to customize the page for `#plugin`:

```markdown
/content/tags/plugin.md
---
title: Plugin Tag
description: Notes related to plugins and extensions
tags: []
---

This page collects all notes tagged with `#plugin`. You can add context, links, or even embed Dataview queries here.
```

> The `tags: []` field ensures this page doesn’t get tagged itself and show up in its own listing.
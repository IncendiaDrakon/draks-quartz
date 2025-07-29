---
title: Renders
---
```dataviewjs
dv.table(
  ["Preview", "Title", "Date", "Universe", "Characters"],
  dv.pages('#render')
    .filter(p => p.image && p.title && p.date && p.universe && p.characters)
    .sort(p => p.date, "desc")
    .map(p => [
      `![|100](${p.image})`, // Thumbnail preview (100px wide)
      p.file.link,
      p.date,
      p.universe,
      Array.isArray(p.characters) ? p.characters.join(", ") : p.characters
    ])
);
```

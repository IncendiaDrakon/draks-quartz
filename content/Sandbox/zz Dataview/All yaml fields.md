```dataviewjs
// Build a map of field → [files]
const fieldMap = {};
for (let page of dv.pages("")) {
  const fm = page.file.frontmatter;
  if (!fm) continue;
  for (let key of Object.keys(fm)) {
    if (!fieldMap[key]) fieldMap[key] = [];
    fieldMap[key].push(page.file.link);
  }
}
// Render as table: one row per field, files joined inline
dv.table(
  ["YAML Field", "Files"],
  Object.entries(fieldMap)
    .sort((a, b) => a[0].localeCompare(b[0]))
    .map(([key, files]) => [ key, files.join(" • ") ])
);
```
```dataviewjs
let rows = [];

for (let page of dv.pages().where(p => Object.keys(p).length > 0)) {
  for (let [key, value] of Object.entries(page)) {
    if (["file", "position", "tags", "length"].includes(key)) continue;
    rows.push([dv.fileLink(page.file.path), key, value]);
  }
}

// Sort rows by the field name (second column)
rows.sort((a, b) => a[1].localeCompare(b[1]));

dv.table(["File", "Field", "Value"], rows);

```





```dataviewjs
const files = app.vault.getFiles();
files.sort((a, b) => a.extension.localeCompare(b.extension)); // Sort by file extension
dv.table(["File", "Path", "Extension"], files.map(file => [
    dv.fileLink(file.path),
    file.path,
    file.extension
]));
```

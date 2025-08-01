```dataviewjs
// Helper to get the word count from file content
async function getWordCount(filePath) {
  const file = app.vault.getAbstractFileByPath(filePath);
  if (!file || file.extension !== 'md') return 0;

  const text = await app.vault.read(file);
  return text.split(/\s+/).filter(w => w.length).length;  // count words by splitting on spaces
}

const pages = dv.pages("")                      // all pages
  .filter(p => p.file.tags && p.file.tags.length);  // only files with tags

// Build rows asynchronously
const rows = [];
for (let p of pages) {
  const wc = await getWordCount(p.file.path); // Get dynamic word count
  rows.push([
    dv.fileLink(p.file.path),  // Restores the filename column
    p.date,
    p.universe,
    p.status,
    wc,  // Word count
    p.file.tags, 
    p.characters
  ]);
}

// Render the table sorted by date descending
dv.table(
  ["📁File", "📅Date", "🌎Universe", "🔄Status", "✍️WC", "🏷️Tags", "🎭Characters"],
  rows.sort((a,b) => b[1] - a[1])  // Sort by date descending
);
```

<%*
// 1. Bootstrap the Dataview API
const dvPlugin = this.app.plugins.plugins["dataview"];
if (!dvPlugin) throw new Error("Dataview plugin not enabled");
const dv = dvPlugin.api;

// 2. Query and sort your #render pages
const pages = dv
  .pages('#render')
  .filter(p => p.image && p.title && p.date && p.universe && p.characters)
  .sort(p => p.date, "desc")
  .values;

// 3. Build the Markdown table header
let table = 
  "| Preview | Title | Date | Universe | Characters |\n" +
  "| ------- | ----- | ---- | -------- | ---------- |\n";

// 4. Append one row per page
for (const p of pages) {
  const preview = `![|100](${p.image})`;
  const title   = p.file.link;
  const date    = p.date;
  const uni     = p.universe;
  const chars   = Array.isArray(p.characters)
    ? p.characters.join(", ")
    : p.characters;

  table += `| ${preview} | ${title} | ${date} | ${uni} | ${chars} |\n`;
}

// 5. Set Templater’s result variable
tR = table;
%>

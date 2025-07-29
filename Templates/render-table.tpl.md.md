<%*
// Fetch, filter, sort, and map your pages
const rows = dv.pages('#render')
  .filter(p => p.image && p.title && p.date && p.universe && p.characters)
  .sort(p => p.date, 'desc')
  .map(p => [
    `![|100](${p.image})`,                       // 100px-wide thumbnail
    p.file.link,                                 // internal link
    p.date,                                      // date
    p.universe,                                  // universe tag or field
    Array.isArray(p.characters)
      ? p.characters.join(', ')
      : p.characters                             // characters list
  ]);

// Render the static Markdown table
tR += dv.table(
  ['Preview', 'Title', 'Date', 'Universe', 'Characters'],
  rows
);
%>

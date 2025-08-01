
https://gemini.google.com/app/4eff327c0f25a937

You've provided your `quartz.layout.ts` file, which is exactly where you need to make the change. Your current configuration uses the default `Component.Explorer()` without any custom options.

To make the Explorer sort pages by their modification date (newest on top) while still keeping folders on top, you need to add a custom `sortFn` to the `Component.Explorer` in both `defaultContentPageLayout` and `defaultListPageLayout`.

Here's how to modify your `quartz.layout.ts` file to achieve that.

TypeScript

```
import { PageLayout, SharedLayout } from "./quartz/cfg"
import * as Component from "./quartz/components"
import { FileNode } from "./quartz/components/Explorer" // Import the FileNode type

// Custom sorting function
const sortByModified: (a: FileNode, b: FileNode) => number = (a, b) => {
  // Sort folders first
  if (a.isFolder && !b.isFolder) return -1
  if (!a.isFolder && b.isFolder) return 1

  // If both are files, sort by modified date (newest on top)
  if (!a.isFolder && !b.isFolder) {
    // Access the modified date. The '?? 0' handles cases where a date might be missing.
    const aDate = a.fileData?.dates?.modified ?? 0
    const bDate = b.fileData?.dates?.modified ?? 0

    // Compare the dates in descending order.
    // The `.getTime()` is used to get a number representation of the date for easy subtraction.
    const aTime = aDate instanceof Date ? aDate.getTime() : aDate
    const bTime = bDate instanceof Date ? bDate.getTime() : bDate

    return bTime - aTime
  }

  // If both are folders, use the default alphabetical sort
  return a.displayName.localeCompare(b.displayName, undefined, { numeric: true, sensitivity: "base" })
}

// components shared across all pages
export const sharedPageComponents: SharedLayout = {
  head: Component.Head(),
  header: [],
  afterBody: [],
  footer: Component.Footer({
    links: {
      GitHub: "https://github.com/jackyzha0/quartz",
      "Discord Community": "https://discord.gg/cRFFHYye7t",
    },
  }),
}

// components for pages that display a single page (e.g. a single note)
export const defaultContentPageLayout: PageLayout = {
  beforeBody: [
    Component.ConditionalRender({
      component: Component.Breadcrumbs(),
      condition: (page) => page.fileData.slug !== "index",
    }),
    Component.ArticleTitle(),
    Component.ContentMeta(),
    Component.TagList(),
  ],
  left: [
    Component.PageTitle(),
    Component.MobileOnly(Component.Spacer()),
    Component.Flex({
      components: [
        {
          Component: Component.Search(),
          grow: true,
        },
        { Component: Component.Darkmode() },
        { Component: Component.ReaderMode() },
      ],
    }),
    // Apply the custom sortFn here
    Component.Explorer({
      sortFn: sortByModified,
    }),
  ],
  right: [
    Component.Graph(),
    Component.DesktopOnly(Component.TableOfContents()),
    Component.Backlinks(),
  ],
}

// components for pages that display lists of pages  (e.g. tags or folders)
export const defaultListPageLayout: PageLayout = {
  beforeBody: [Component.Breadcrumbs(), Component.ArticleTitle(), Component.ContentMeta()],
  left: [
    Component.PageTitle(),
    Component.MobileOnly(Component.Spacer()),
    Component.Flex({
      components: [
        {
          Component: Component.Search(),
          grow: true,
        },
        { Component: Component.Darkmode() },
      ],
    }),
    // Apply the custom sortFn here as well
    Component.Explorer({
      sortFn: sortByModified,
    }),
  ],
  right: [],
}
```

### Explanation of the changes:

1. **Import `FileNode`:** I added `import { FileNode } from "./quartz/components/Explorer"`. This is important for TypeScript to understand the type of the objects being sorted.
    
2. **Create `sortByModified` function:** I've defined a new function `sortByModified` that takes two `FileNode` objects, `a` and `b`, and returns a number.
    
    - **Folder-First Logic:** The first part of the function `if (a.isFolder && !b.isFolder) return -1` and the next line keeps the original behavior of always showing folders at the top.
        
    - **Date-Based Sorting:** The core of the new logic is in the `if (!a.isFolder && !b.isFolder)` block. It checks if both `a` and `b` are files (not folders).
        
        - It then accesses the `modified` date from `a.fileData?.dates?.modified` and `b.fileData?.dates?.modified`.
            
        - The `?? 0` is a nullish coalescing operator that provides a fallback value of `0` if a date is missing, which prevents the function from crashing.
            
        - `bTime - aTime` is the key to sorting. If `b`'s modified time is a larger number (more recent) than `a`'s, the result is positive, which puts `b` first in the sort order. This achieves the "newest on top" requirement.
            
3. **Apply `sortFn`:** In both `defaultContentPageLayout` and `defaultListPageLayout`, I've replaced `Component.Explorer()` with `Component.Explorer({ sortFn: sortByModified })`. This passes your new custom sorting function to the Explorer component, overriding the default alphabetical sort.
    

After saving this file, your Quartz site will re-build, and the explorer in the sidebar will now sort your pages from newest to oldest within each folder, while still listing folders first.
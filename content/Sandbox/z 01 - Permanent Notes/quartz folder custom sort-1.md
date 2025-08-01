
```quartz.layout.ts
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
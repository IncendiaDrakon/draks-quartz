# Vault Style Guide

A living document for maintaining consistent, query-friendly metadata and folder structure across your markdown vault.

---

## 1. Frontmatter Overview

Every note begins with a YAML frontmatter block. Keep it minimal, ordered, and self-documenting.

```yaml
---
title:                # Human-readable note title
date: YYYY-MM-DD      # ISO 8601 format
project:              # Parent project or collection
universe:             # Fictional world or context
characters:           # List of involved characters
  - Name1
  - Name2
tags:                 # Unordered list of keywords
  - tag1
  - tag2
is_nsfw: false        # Boolean flag; true if NSFW, false or omit if SFW
---
```

---

## 2. Field Definitions

|Field|Type|Required|Description|
|---|---|---|---|
|title|string|yes|Descriptive, sentence-case title|
|date|date|yes|Publication or creation date|
|project|string|no|Parent project name|
|universe|string|no|Setting or world|
|characters|list|no|Key individuals featured|
|tags|list|no|Keywords for filtering by medium, software, theme, etc.|
|is_nsfw|boolean|no|true = NSFW, false = SFW (or omitted for SFW)|

---

## 3. Content Rating

Use `is_nsfw` to distinguish SFW from NSFW.

- Set `is_nsfw: true` for any erotic or explicit assets.
- Omit or set `is_nsfw: false` for all other content.

Your Dataview queries should treat missing as `false`:

```dataview
TABLE title, date
FROM "renders/"
WHERE choice(is_nsfw, false) = false
```

---

## 4. Tagging Conventions

- Use lowercase, kebab-case or slash-separated hierarchies.
- Prefix with category if helpful:
    - `software/blender`
    - `medium/3d-render`
    - `theme/wedding`

Avoid mixing metadata into `tags`; reserve `tags` for free-form filters.

---

## 5. File Naming

Adopt a clear, sortable filename convention:

`YYYY-MM-DD — Short Title — project-slug.ext`

Example:

```
2025-03-01 — Eternal-Bonding-VI — ffxiv-wedding.blend
```

- ISO date prefix ensures chronological sort.
- Em-dashes separate elements.
- Project slug ties back to `project` field.

---

## 6. Dataview Query Patterns

List all NSFW entries

```dataview
TABLE title, date 
FROM "renders/" 
WHERE is_nsfw = true
```

Count SFW vs NSFW

```dataview
TABLE 
  sum(choice(is_nsfw, false) = false ? 1 : 0) AS SFW,
  sum(choice(is_nsfw, false) = true  ? 1 : 0) AS NSFW
FROM "renders/"
```

Find notes missing `is_nsfw`

```dataview
TABLE file.name AS File 
FROM "renders/" 
WHERE !contains(file.frontmatter, "is_nsfw")
```

---

## 7. Auditing and Hydration

1. Run the “missing flag” query to locate uncategorized notes.
2. Manually add `is_nsfw: false` or confirm true where needed.
3. Tag and link each note to its parent project index for index-first navigation.

---

## 8. Future Extensions

- Add `is_suggestive: true` for mild content gradations.
- Replace booleans with `content_rating: [sfw|suggestive|nsfw]` if tiers multiply.
- Introduce `age_rating` for audience maturity levels.

Maintain a changelog at the bottom of this guide for schema updates.

---

## 9. Revision History

|Date|Change|
|---|---|
|2025-07-27|Initial style guide draft|

---

With this style guide in place, your vault remains consistent, queries stay robust, and collaborators know exactly how to contribute.
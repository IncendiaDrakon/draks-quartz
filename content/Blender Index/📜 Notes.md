---
{"publish":true,"created":"2025-07-29T17:30:32.262-04:00","modified":"2025-07-29T17:40:59.045-04:00","cssclasses":""}
---

# Not a formal "Readme", mostly just a dump of ideas and stuff regarding this Obsidian catalogue for renders/etc.

# Initial Concept

* Creating an "index" for Telegram file dumps.
  Basically, I offload files I want to keep onto Telegram because it offers "unlimited 2gb file uploads".
  I can't edit some aspects regarding the files and messages once they're uploaded. Organization and structure can quickly become confusing or bloated on Telegram.
  An idea I came up with yesterday was to create local index.md and file.md entries locally in my Obsidian vault. I can hotlink to files hosted on Telegram from inside these file.md entries. I can edit the .md at any time, add tags and metdata/yaml for organization. Everything is searchable via Obsidian search.
  My primary focus is retaining all my Blender work. Organizing my .blend archive on Telegram with local .md files referencing them.
  The general structure proposed was:
  index.md: dataview parses all file.md entries and lists them in a table by date for quick and easy reference
  file.md:
  relevant yaml frontmatter
  inline embed of online hosted render (preferably from a bluesky account. saves local space by not storing previews locally)
  link to locally stored high fidelity render
  inline embed of any social media posts (Twitter, Blogger, Bluesky)
  link to Render Archive Telegram channel post (each post contains a dump of raw .exr .png .webp .psd associated with the final render)
  link to relevant post in Blender Telegram archive channel (each message in the channel is a dump of each .blend .blend1 .blend 2 etc in addition to any descriptions
  direct link to relevant final .blend file in Blender Telegram archive
  followed by a blurb/etc and any personal notes about the project

---

# 📇 Index.md: Dataview Table


|Title0|Date|Universe|Characters|
|---|---|---|---|

Dataview: No results to show for table query.

---


- Keeps all your file.md entries in one sortable, filterable table
- Automatically updates whenever you add a new file.md

---

## 3. file.md Template

Place this in `/TelegramFiles/_templates/telegram-file-template.md` and duplicate per project:

```markdown
---
title: {{title}}                  # e.g. “Nebula V4”
date: {{date}}                    # YYYY-MM-DD
tags: [blender, render, telegram-archive, {{additional_tags}}]
telegram:
  render_post: "https://t.me/c/{{render_channel_id}}/{{render_message_id}}"
  blend_post:  "https://t.me/c/{{blend_channel_id}}/{{blend_message_id}}"
  direct_blend: "https://t.me/c/{{blend_channel_id}}/{{blend_message_id}}?download=1"
render:
  preview_online:   "https://bluesky.app/.../media/..."
  high_res_local:   "/BlenderRenders/{{title}}.png"
social:
  - type: bluesky
    url: "{{bluesky_url}}"
  - type: twitter
    url: "{{twitter_url}}"
---

![Preview]({{render.preview_online}})

[Download high-res local render]({{render.high_res_local}})

---

## Telegram Links

- [Render post]({{telegram.render_post}})
- [Blend post]({{telegram.blend_post}})
- [Direct .blend download]({{telegram.direct_blend}})

---

## Social Embeds

- Bluesky: ![]({{social[0].url}})
- Twitter: ![]({{social[1].url}})

---

## Notes

{{personal_blurb}}
```

Render preview repo: https://whtwnd.com/drakon.bsky.social/3lux7ljvhny2o

---
---
---

# Different dataview table versions for Index.md

---

|Title0|Date|Universe|Characters|
|---|---|---|---|

Dataview: No results to show for table query.

| File                                                                                                                  | characters                                             |
| --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| [[Blender Index/Renders/2024-11-14 - Drakon's Birthday 2024\|2024-11-14 - Drakon's Birthday 2024]]                 | <ul><li>Vallia</li><li>Iriali</li><li>Marina</li></ul> |
| [[Blender Index/Renders/2025-03-01 - FFXIV 2025 Wedding Anniversary\|2025-03-01 - FFXIV 2025 Wedding Anniversary]] | <ul><li>Vallia</li><li>Iriali</li></ul>                |


Obsidian property search example: ["characters":Iriali]

[Find Vallia](obsidian://search?v=Vallia)

[Characters: Vallia](obsidian://search?v=%5B%22characters%22%3AVallia%5D)


|Preview0|Title|Date|Universe|Characters|
|---|---|---|---|---|

Dataview: No results to show for table query.
|Preview2|Title|Date|Universe|Characters|
|---|---|---|---|---|
|![](https://shiitake.us-east.host.bsky.network/xrpc/com.atproto.sync.getBlob?did=did%3Aplc%3Avigxa24owwfxyoe5nnweh7i4&cid=bafkreidyxzlortntwyeawnu6qmmxssv3h2bw7lgybrff6mzvrjhte5m22e)|[[Blender Index/Renders/2025-03-01 - FFXIV 2025 Wedding Anniversary\|2025-03-01 - FFXIV 2025 Wedding Anniversary]]|March 01, 2025|Final Fantasy XIV|Vallia, Iriali|
|![](https://shiitake.us-east.host.bsky.network/xrpc/com.atproto.sync.getBlob?did=did%3Aplc%3Avigxa24owwfxyoe5nnweh7i4&cid=bafkreibq64mpmtzxrpc6m2ly353h4glpajais7q2ogrph4s5bf6a4zg5tq)|[[Blender Index/Renders/2024-11-14 - Drakon's Birthday 2024\|2024-11-14 - Drakon's Birthday 2024]]|November 16, 2024|Final Fantasy XIV|Vallia, Iriali, Marina|

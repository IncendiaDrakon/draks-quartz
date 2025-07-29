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
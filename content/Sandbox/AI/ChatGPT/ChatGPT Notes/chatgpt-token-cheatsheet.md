---
title: "ChatGPT Token + Scene Preservation Guide"
summary: Best practices for managing token limits and preserving narrative in longform writing with ChatGPT
tags: [workflow, tokens, memory, writing]
---

# 🧠 ChatGPT Token + Scene Preservation Guide

## 📏 Approximate Token-to-Word Conversion

| Tokens | Approx. Words | Notes |
|--------|---------------|-------|
| 1,000  | ~750 words    | A few paragraphs of prose |
| 4,000  | ~3,000 words  | Short story or long scene |
| 8,000  | ~6,000 words  | GPT-4o free tier token window (input + output) |

> ⚠️ Anything older than ~8,000 tokens **falls out of ChatGPT’s active attention**, even if it’s still visible in your UI.

---

## ✅ How to Preserve Narrative Scenes

### Before Editing or Moving On
- “**Reprint the full scene**”  
- “**Save this as scene.txt**”  
- “**Export this version**”  
- “**Create a checkpoint here**”

### Before Zipping or Exporting
- “**Ensure scene.txt includes the final revision**”  
- “**Include V1 version in the archive**”

### To Restore Memory After Loss
- Paste the full scene back in manually  
- Say: “**Use this as the current draft**”  
- Optionally ask for a re-export (`scene.txt`, `readme.md`, etc.)

---

## 📦 Best Export Practices

| Format        | Use Case                          |
|---------------|-----------------------------------|
| `.txt`        | Clean prose, copy/paste friendly  |
| `.md`         | Obsidian/blog/structured writing  |
| `.zip`        | Full archive (scene + metadata)   |
| `scene.json`  | Internal tracking or syncing      |

---

## 💡 Pro Tip

If you revise a scene more than once, always ask for:
> “**Full reprint before we continue.**”

That locks the revision into visible context and avoids drift.

---


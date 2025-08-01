# 🧠 Creative Writing Workflow Summary

## ✍️ Overview

- The user is a professional writer of adult erotic fiction.
- Workflow is **scene-driven and character-focused**, blending structured drafting with improvisation.
- Combines elements of:
  - **Workflow A**: Chat-driven drafting with structured prompts
  - **Workflow C**: Worldbuilding and character evolution
- Prefers **random prompting** and **improvisational generation** for inspiration.
- Internally reimagines and mentally revises scenes after generation.

---

## 🗂️ File Structure & Organization

Each scene is stored in its own folder: `/scenes/<title>/`

### Default Contents:
- `scene.txt`: Full narrative (validated for completeness)
- `readme.md`: Human-readable scene overview
- `scene.json`: Scene metadata (flat structured)
- `tags.json`: Scene-specific tags
- `scene-index.json`: Local index file for lookup or navigation
- `universe.json`: Global universe data if relevant

### Character Files:
- `<char-id>.json`: Full character sheet
- `<char-id>-evolution.json`: Tracks development over time (aging, anatomy, personality, changes)

### Notes:
- Scene folders always include a `readme.md` by default
- Optional `scene-notes.md` tracks global drafting or world continuity
- Avoids `scene-index.jsonl` — not useful for the user’s workflow

---

## 🧑‍🤝‍🧑 Characters & Evolution Tracking

- Character data is stored as standalone `.json` files.
- Details include:
  - Appearance, anatomy, personality, background
- Character evolution is tracked using timestamped changes across scenes (`<name>-evolution.json`)
- Used to ensure long-term continuity, growth, or transformation

---

## 📝 Drafting Style & Vocabulary

- Prefers **manual regeneration** and **selective branching**
- Uses strict, **correct literary terminology**:
  - ✅ Draft: Preliminary version
  - ✅ Version: Alternate take on a prompt or concept
  - ✅ Branch: Divergent narrative direction
  - ✅ Revision: Edited/improved version of an existing draft
  - ❌ Avoids “iteration” — not a valid term in creative writing
- Scene structure prioritizes physicality, tone, and emotional arcs
- Dialogue is kept minimal early when characters are unfamiliar

---

## 📑 Metadata Structure

### Required per Scene:
- Title
- Summary
- Character IDs
- Tone and themes
- Location
- Tags (optional but supported)

### Markdown Usage:
- `readme.md` gives scene-level overview
- `scene-notes.md` logs broader narrative or worldbuilding notes
- Simple, flat `.json` files support tooling or search

---

## ⚠️ Token Management

- Token usage is monitored **passively**
- Assistant provides a warning when within **~1000 tokens** of the safe limit to avoid token drift
- Drafting is structured to avoid session-based data loss

---

## 🛠️ Tools & Platform

- Uses **Obsidian** on desktop and Android
- Markdown syntax is kept **basic** for maximum compatibility
- Avoids `.jsonl` or tools that increase token overhead or platform lock-in
- Syncs Obsidian vaults across devices using cloud or file transfer

---

## 🔁 Regeneration Commands & Version Control

- Commands include:
  - “Regenerate that response”
  - “Try a new version with more [X]”
  - “Branch this at the moment they touch”
- Regenerated scenes are referred to as:
  - **Versions** (different takes)
  - **Drafts** (refinements)
  - **Branches** (narrative forks)

---
[[symlinks in obsidian vault root]]

Nice—this is the kind of elegant workaround that fits your modular style perfectly. Symlinked folders let you blend external assets into your vault's semantic mesh without compromising structure, portability, or Git hygiene. Here's a quick extension that complements your note and could live in `workflow.lore` or a dedicated `vault_symlink_strategy.md`:

## 🔗 Symlink Strategy for Vault Hygiene

**Purpose:** Integrate large or external asset folders into Obsidian without physically nesting them, preserving vault clarity and enabling native linking.

---

### 🧠 Benefits
- Native embed/link support (`![[image.png]]`) from symlinked folders
- Keeps vault folder lightweight and backup-friendly
- Avoids bloating GitHub repos with bulky media
- Enables parallel project foldering without note duplication

---

### 🛠️ Setup Guidelines
1. **Create Symlink**  
   Use command line or a tool to symlink external folder into vault root:  
   - macOS/Linux: `ln -s /path/to/assets ~/Vault/assets_link`
   - Windows: `mklink /D "C:\Vault\assets_link" "D:\Media\Assets"`

2. **Reference Assets**  
   Use standard markdown embeds/links as if assets were native:  
   - `![[assets_link/image01.png]]`

3. **Git Ignore External Assets**  
   In `.gitignore`, exclude symlinked content to prevent bulk commits:
      assets_link/

4. **Audit for Plugin Awareness**  
    Some plugins may ignore symlinks or misindex files—track compatibility in `plugin-quirks.md`

---

### 🧼 Maintenance Notes

- Periodically verify symlink integrity (especially after vault moves)
- Use Dataview to surface unlinked symlinked assets for archival audits
- Keep `assets_link` naming consistent across vaults for portability

**Tags:** `#symlink-strategy` `#vault-hygiene` `#git-friendly`



You might also explore dynamically mounting folders based on context—e.g., symlinking `screenshots/` when doing image-heavy work, then unlinking to declutter. Want help setting up a Dataview query that tracks embedded vs orphaned symlink assets?

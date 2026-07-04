# Skills Install Guide (for the laptop)

Hand this file to Claude Code on the laptop and say:
**"Read INSTALL-GUIDE.md and install the skills accordingly."**

It covers three groups:
1. **File skills** — the 12 folders in this bundle (just copy them). ✅ portable
2. **ui-ux-pro-max suite** — has an official npm installer (different method). ⚙️
3. **Plugin / environment skills + built-ins** — NOT files; can't be copied. Read notes. ⚠️

---

## 0. Prerequisites / what you'll need

- **Claude Code** installed on the laptop.
- **Node.js + npm** (only for the ui-ux-pro-max CLI in Section 2). Check with `node -v` and `npm -v`. If missing, install Node LTS from https://nodejs.org.
- This **`All Skills`** folder copied onto the laptop (e.g. via USB / cloud). Note where you put it; the commands below assume you're `cd`'d into it.
- Skills install location:
  - **Global (all projects):** `~/.claude/skills/` — Windows: `C:\Users\<you>\.claude\skills\`
  - **Per-project:** `<project>\.claude\skills\`

---

## 1. File skills — copy the 12 folders (simplest, no internet)

These 12 are fully self-contained in this bundle (symlinks already dereferenced):

`ui-ux-pro-max`, `design`, `design-system`, `ui-styling`, `banner-design`, `brand`,
`slides`, `design-motion-principles`, `frontend-design`, `impeccable`,
`design-taste-frontend`, `emil-design-eng`

**Windows (PowerShell)** — from inside the `All Skills` folder:
```powershell
$dest = "$env:USERPROFILE\.claude\skills"
New-Item -ItemType Directory -Force $dest | Out-Null
Get-ChildItem -Directory | ForEach-Object { Copy-Item $_.FullName $dest -Recurse -Force }
```

**macOS / Linux (bash):**
```bash
mkdir -p ~/.claude/skills
cp -r */ ~/.claude/skills/
```

Then restart Claude Code. Done — all 12 are active.

> Note: `README.md`, `INSTALL-GUIDE.md`, and any `.zip` in this folder are docs, not skills — don't copy those into `skills/`.

---

## 2. ui-ux-pro-max suite — official npm installer (recommended for updates)

The `ui-ux-pro-max` family (7 skills: `ui-ux-pro-max`, `design`, `design-system`,
`ui-styling`, `banner-design`, `brand`, `slides`) can also be installed via its CLI,
which is better because you get updates with `uipro update`.

These 7 **overlap** with Section 1. Pick ONE approach for them:
- **Easiest:** just use the Section 1 copy (no npm needed), OR
- **Best for updates:** use the CLI below instead, and from Section 1 only copy the
  other 5 (`design-motion-principles`, `frontend-design`, `impeccable`,
  `design-taste-frontend`, `emil-design-eng`).

CLI install (global, for Claude Code):
```bash
npm install -g ui-ux-pro-max-cli
uipro init --ai claude --global --offline --force
```
- Installs into `~/.claude/skills/`.
- `--offline` uses bundled assets (avoids GitHub API rate limits).
- Source: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill · docs: https://ui-ux-pro-max-skill.nextlevelbuilder.io/
- Manage later: `uipro update`, `uipro versions`, `uipro uninstall --global`.

---

## 3. Plugin & environment skills — CANNOT be copied as files

The following show up in Claude but are **not stored as skill folders**, so there's
nothing in this bundle to copy. Here's how to get each group:

### 3a. Environment-bundled skills (`anthropic-skills:*`, `design:*`, `cowork-plugin-management:*`)
Examples: `anthropic-skills:docx / pdf / pptx / xlsx / meta-ads-* / prompt-master /
skill-creator / dailynotes / …`, `design:design-critique / accessibility-review /
ux-copy / user-research / …`, `cowork-plugin-management:create-cowork-plugin`.

- These are provided **automatically by the Claude environment (Cowork / managed Claude)**,
  not by a public marketplace you add manually. On the source machine they were not in
  any marketplace catalog or on disk.
- **What to do on the laptop:** if the laptop uses the **same Cowork / Claude environment
  and is signed into the same account**, these appear on their own — no install needed.
  If they're missing, they aren't separately installable as files; they come with that
  environment. Run `/plugin` in interactive Claude Code to see what's available/enabled.

### 3b. General marketplace plugins (if you want to add OTHER plugin skills)
Claude Code can add public plugin marketplaces. General pattern (run in **interactive**
Claude Code, not this file):
```
/plugin marketplace add <owner>/<repo>
/plugin install <plugin-name>@<marketplace-name>
```
Browse everything available with the `/plugin` command. (These are interactive terminal
commands — a non-interactive agent can't run them for you.)

---

## 4. Built-in commands — nothing to install

These ship inside Claude Code itself and are always present once Claude Code is installed:
`code-review`, `simplify`, `verify`, `run`, `security-review`, `review`, `init`,
`claude-api`, `loop`, `schedule`, `update-config`, `keybindings-help`,
`fewer-permission-prompts`.

No action required.

---

## 5. Verify the install

**PowerShell:**
```powershell
Get-ChildItem "$env:USERPROFILE\.claude\skills" | Select-Object Name
```
**bash:**
```bash
ls ~/.claude/skills
```
You should see the 12 folders from Section 1 (and/or the 7 from the CLI). Restart Claude
Code, then in a session confirm they load (they'll be listed as available skills).

---

## Summary

| Group | Method | Internet? |
|-------|--------|-----------|
| 12 file skills (this bundle) | Copy folders → `~/.claude/skills/` | No |
| ui-ux-pro-max suite (7) | `npm i -g ui-ux-pro-max-cli` → `uipro init --ai claude --global` | Yes (once) |
| anthropic-skills / design / cowork | Come with the Cowork/Claude environment | n/a |
| Built-in commands | Come with Claude Code | n/a |

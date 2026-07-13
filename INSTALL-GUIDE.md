# Skills Install Guide (for the laptop)

Hand this file to Claude Code on the laptop and say:
**"Read INSTALL-GUIDE.md and install the skills accordingly."**

It covers:
1. **File skills** — the 40 folders in this repo (just copy them). ✅ portable
2. **The `function-analyzer` agent** — one file, copy into `~/.claude/agents/`. ✅ portable
3. **ui-ux-pro-max suite** — also has an official npm installer (optional, for updates). ⚙️
4. **Plugin / environment skills + built-ins** — NOT files; can't be copied. Read notes. ⚠️

---

## 0. Prerequisites / what you'll need

- **Claude Code** installed on the laptop.
- **Node.js + npm** — only for the optional `ui-ux-pro-max` CLI (§3) and to *run*
  `superdesign` (§2 notes). Check with `node -v` / `npm -v`; install Node LTS from
  https://nodejs.org if missing.
- This repo copied onto the laptop (USB / cloud / `git clone`). The commands below assume
  you're `cd`'d into the repo root.
- Install locations:
  - **Skills — global (all projects):** `~/.claude/skills/` — Windows: `C:\Users\<you>\.claude\skills\`
  - **Skills — per-project:** `<project>\.claude\skills\`
  - **Agents — global:** `~/.claude/agents/`

---

## 1. File skills — copy the 40 folders (simplest, no internet)

All 40 are fully self-contained (each is a folder with a `SKILL.md`). They fall into five
groups:

- **Design & frontend (12):** `ui-ux-pro-max`, `design`, `design-system`, `ui-styling`,
  `banner-design`, `brand`, `slides`, `design-motion-principles`, `frontend-design`,
  `impeccable`, `design-taste-frontend`, `emil-design-eng`
- **Superpowers dev workflow (14):** `brainstorming`, `writing-plans`, `executing-plans`,
  `subagent-driven-development`, `dispatching-parallel-agents`, `test-driven-development`,
  `systematic-debugging`, `requesting-code-review`, `receiving-code-review`,
  `verification-before-completion`, `using-git-worktrees`, `finishing-a-development-branch`,
  `writing-skills`, `using-superpowers`
- **Trail of Bits security audit (12):** `audit-context-building`, `audit-prep-assistant`,
  `code-maturity-assessor`, `guidelines-advisor`, `secure-workflow-guide`,
  `token-integration-analyzer`, `algorand-vulnerability-scanner`,
  `cairo-vulnerability-scanner`, `cosmos-vulnerability-scanner`,
  `solana-vulnerability-scanner`, `substrate-vulnerability-scanner`,
  `ton-vulnerability-scanner`
- **Superdesign (1):** `superdesign`
- **Karpathy (1):** `karpathy-guidelines`

Copy every top-level folder **except `agents/`** (that goes to a different place — §2).

**Windows (PowerShell)** — from the repo root:
```powershell
$dest = "$env:USERPROFILE\.claude\skills"
New-Item -ItemType Directory -Force $dest | Out-Null
Get-ChildItem -Directory -Exclude agents | ForEach-Object { Copy-Item $_.FullName $dest -Recurse -Force }
```

**macOS / Linux (bash):**
```bash
mkdir -p ~/.claude/skills
for d in */; do [ "$d" = "agents/" ] && continue; cp -r "$d" ~/.claude/skills/; done
```

Then start a new Claude Code session — all 40 are active.

> Note: `README.md`, `INSTALL-GUIDE.md`, and any `.zip` are docs, not skills — don't copy
> those into `skills/`.

### Group-specific caveats
- **superdesign** files install fine, but *running* it needs
  `npm install -g @superdesign/cli@latest` **plus a browser login** — it's a cloud/account
  service, not offline.
- **superpowers** works on demand as loose skills, but its always-on session-start hook
  won't fire from a folder copy. Want the auto behavior? Install it as a plugin instead:
  `/plugin marketplace add obra/superpowers`.
- **audit-context-building** ships an optional `/audit-context` slash command that is not
  in this repo; only the skill + its `function-analyzer` agent are (see §2).

---

## 2. The `function-analyzer` agent — copy into `~/.claude/agents/`

`audit-context-building` spawns a `function-analyzer` subagent for per-function deep
analysis. It lives in `agents/` here and must go to the **agents** dir, not `skills/`.

**PowerShell:**
```powershell
$adest = "$env:USERPROFILE\.claude\agents"
New-Item -ItemType Directory -Force $adest | Out-Null
Copy-Item "agents\*" $adest -Recurse -Force
```
**bash:**
```bash
mkdir -p ~/.claude/agents
cp -r agents/* ~/.claude/agents/
```

---

## 3. ui-ux-pro-max suite — official npm installer (optional, for updates)

The `ui-ux-pro-max` family (7 skills: `ui-ux-pro-max`, `design`, `design-system`,
`ui-styling`, `banner-design`, `brand`, `slides`) can also be installed via its CLI, which
gives you updates with `uipro update`.

These 7 **overlap** with §1 — pick ONE approach for them:
- **Easiest:** just use the §1 copy (no npm needed), OR
- **Best for updates:** use the CLI below, and from §1 copy only the other 33 folders.

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

## 4. Plugin & environment skills — CANNOT be copied as files

These show up in Claude but are **not stored as skill folders**, so there's nothing here
to copy.

### 4a. Environment-bundled skills (`anthropic-skills:*`, `design:*`, `cowork-plugin-management:*`)
Provided automatically by the Claude environment (Cowork / managed Claude), not by a public
marketplace. If the laptop uses the **same environment and account**, they appear on their
own. If missing, they aren't separately installable as files. Run `/plugin` in interactive
Claude Code to see what's available/enabled.

### 4b. General marketplace plugins (to add OTHER plugin skills)
Claude Code can add public plugin marketplaces. Run in **interactive** Claude Code (not this
file):
```
/plugin marketplace add <owner>/<repo>
/plugin install <plugin-name>@<marketplace-name>
```
Example — the full Trail of Bits security marketplace (~45 plugins, only 2 are copied into
this repo):
```
/plugin marketplace add trailofbits/skills
/plugin install <plugin>@trailofbits
```

---

## 5. Built-in commands — nothing to install

These ship inside Claude Code itself and are always present: `code-review`, `simplify`,
`verify`, `run`, `security-review`, `review`, `init`, `claude-api`, `loop`, `schedule`,
`update-config`, `keybindings-help`, `fewer-permission-prompts`. No action required.

---

## 6. Verify the install

**PowerShell:**
```powershell
Get-ChildItem "$env:USERPROFILE\.claude\skills" | Select-Object Name
Get-ChildItem "$env:USERPROFILE\.claude\agents" | Select-Object Name
```
**bash:**
```bash
ls ~/.claude/skills ~/.claude/agents
```
You should see the 40 skill folders and `function-analyzer.md`. Restart Claude Code, then
confirm they load in a session's available-skills list.

---

## Summary

| Group | Method | Internet? |
|-------|--------|-----------|
| 40 file skills (this repo) | Copy folders → `~/.claude/skills/` (exclude `agents/`) | No |
| function-analyzer agent | Copy `agents/*` → `~/.claude/agents/` | No |
| ui-ux-pro-max suite (7, optional CLI) | `npm i -g ui-ux-pro-max-cli` → `uipro init --ai claude --global` | Yes (once) |
| superdesign (to run it) | `npm i -g @superdesign/cli@latest` + browser login | Yes |
| anthropic-skills / design / cowork | Come with the Cowork/Claude environment | n/a |
| Built-in commands | Come with Claude Code | n/a |

# Claude Skills

Portable, self-contained copies of the file-based Claude Code skills installed on this
machine, plus one supporting agent. Every skill is a top-level folder containing a
`SKILL.md`. To install, copy the folders into your Claude Code skills directory — no
build step, and no internet except for the couple of cases flagged below.

- **Global (all projects):** `~/.claude/skills/` — Windows: `C:\Users\<you>\.claude\skills\`
- **Per-project:** `<project>\.claude\skills\`

> For a longer, step-by-step walkthrough (including the `ui-ux-pro-max` CLI, marketplace
> plugins, and built-in commands), see [INSTALL-GUIDE.md](INSTALL-GUIDE.md).

## What's here — 40 skills + 1 agent

### Design & frontend (12)
| Skill | Purpose |
|-------|---------|
| ui-ux-pro-max | Core design-intelligence engine: 67 styles, 161 palettes, 57 font pairings, 21 stacks |
| design | All-in-one brand/design generator: logos, corporate identity, icons, banners, social images |
| design-system | Token architecture, component specs, and brand-compliant slides |
| ui-styling | Accessible UIs with shadcn/ui + Tailwind and visual designs |
| banner-design | Banners for social, ads, web heroes, and print |
| brand | Brand voice, visual identity, and messaging frameworks |
| slides | Strategic HTML presentations with Chart.js |
| design-motion-principles | Build or audit UI motion against AI-slop patterns |
| frontend-design | Distinctive, non-templated visual design direction |
| impeccable | Deep frontend UI/UX audit and polish |
| design-taste-frontend | Anti-slop landing pages, portfolios, and redesigns |
| emil-design-eng | Emil Kowalski's UI polish and animation philosophy |

### Superpowers — dev workflow (14)
Jesse Vincent's core skills library, from [obra/superpowers](https://github.com/obra/superpowers).

`brainstorming`, `writing-plans`, `executing-plans`, `subagent-driven-development`,
`dispatching-parallel-agents`, `test-driven-development`, `systematic-debugging`,
`requesting-code-review`, `receiving-code-review`, `verification-before-completion`,
`using-git-worktrees`, `finishing-a-development-branch`, `writing-skills`, `using-superpowers`

### Trail of Bits — security audit (12)
From [trailofbits/skills](https://github.com/trailofbits/skills) (only the two audit
plugins picked, not the full ~45-plugin marketplace).

- **audit-context-building** — ultra-granular, line-by-line code analysis to build deep
  architectural context before hunting vulnerabilities. Uses the `function-analyzer`
  agent (see `agents/`).
- **building-secure-contracts** — smart-contract audit toolkit (11 skills):
  `audit-prep-assistant`, `code-maturity-assessor`, `guidelines-advisor`,
  `secure-workflow-guide`, `token-integration-analyzer`, and vulnerability scanners for
  `algorand`, `cairo`, `cosmos`, `solana`, `substrate`, `ton`.

### Superdesign (1)
Frontend UI/UX design agent, from
[superdesigndev/superdesign-skill](https://github.com/superdesigndev/superdesign-skill).
⚠️ Needs an extra CLI + login to actually run — see [Notes](#per-source-notes).

### Karpathy guidelines (1)
`karpathy-guidelines` — behavioral guidelines to reduce common LLM coding mistakes
(surgical changes, surface assumptions, verifiable success criteria). From
[forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills).

### agents/ (1)
`function-analyzer` — per-function deep-analysis subagent used by `audit-context-building`.
Install it into `~/.claude/agents/` (not `skills/`).

## Install

### 1. Skills → `~/.claude/skills/`
Copy every top-level folder **except `agents/`** (and skip the docs/`.zip`).

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

### 2. Agent → `~/.claude/agents/`
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

Start a new Claude Code session and the skills/agent are picked up automatically.

## Per-source notes

- **superdesign needs a CLI + login.** The skill files here are the complete, supported
  install, but running its commands requires `npm install -g @superdesign/cli@latest`
  plus a browser login — it's a **cloud/account service**, not offline.
- **superpowers is installed as loose skills, not as the plugin.** All 14 are invocable
  on demand. The plugin's always-on session-start hook (which auto-activates
  `using-superpowers` each session) does **not** run from a bare folder copy. For that
  auto behavior, install it as a plugin instead: `/plugin marketplace add obra/superpowers`.
- **audit-context-building** also ships an optional `/audit-context` slash command that is
  **not** included here; only the skill and its `function-analyzer` agent are.
- **Trail of Bits:** only `audit-context-building` and `building-secure-contracts` are
  included. The marketplace has ~45 more (static analysis, fuzzing, language-specific
  reviews, etc.) — add them from [trailofbits/skills](https://github.com/trailofbits/skills).

## Not included (can't be copied as files)

- **Plugin/environment skills** (`anthropic-skills:*`, `design:*`,
  `cowork-plugin-management:*`) are provided by installed plugins / the Claude
  environment, not stored as loose files. See [INSTALL-GUIDE.md](INSTALL-GUIDE.md) §3.
- **Built-in commands** (`code-review`, `verify`, `run`, `security-review`, `init`,
  `claude-api`, `loop`, `schedule`, …) ship with Claude Code itself.

## Verify

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
confirm they appear in the session's available-skills list.

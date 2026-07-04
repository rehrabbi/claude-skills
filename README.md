# All Skills (portable copy)

Real, self-contained copies of every file-based Claude skill from this machine,
with all symlinks dereferenced so they work on another computer.

## Contents (12 skills)

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

## How to install on the laptop

Copy the skill folders into either:

- **Global (all projects):** `~/.claude/skills/`  (Windows: `C:\Users\<you>\.claude\skills\`)
- **Per-project:** `<project>/.claude/skills/`

Example (global):

```
cp -r "All Skills/"* ~/.claude/skills/
```

Restart Claude Code (or start a new session) and the skills will be picked up.

## Not included (can't be copied as files)

- **Plugin skills** (`anthropic-skills:*`, `design:*`, `cowork-plugin-management:*`)
  are provided by installed plugins, not stored as loose files. On the laptop,
  install the same plugins to get them.
- **Built-in commands** (`code-review`, `verify`, `run`, `security-review`,
  `init`, `claude-api`, `loop`, `schedule`, etc.) ship with Claude Code itself.
- **ui-ux-pro-max** was installed via `npm i -g ui-ux-pro-max-cli` then
  `uipro init --ai claude --global`. This folder copy works too, but you can
  also reinstall it that way on the laptop to get updates via `uipro update`.

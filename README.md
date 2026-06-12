# shadcn_daisyui Design System — Claude plugin

A Claude [skill](https://code.claude.com/docs/en/skills) that keeps AI-written
UI inside the [shadcn_daisyui](https://github.com/N00nDay/shadcn_daisyui) design
system — spacing, layout, navigation, typography, color, shape, motion,
interaction, and accessibility, for **web (mobile-first responsive)** and
**native iOS/iPadOS (SwiftUI)**.

It auto-loads whenever you ask Claude to build, style, or review UI, so the
guardrails apply without anyone remembering to attach a doc. The same rules are
browsable for humans on the [docs site](https://n00nday.github.io/shadcn_daisyui/)
under Foundations and Styles.

## Install (as a plugin)

```text
/plugin marketplace add N00nDay/shadcn_daisyui_design
/plugin install shadcn-daisyui-design-system@shadcn-daisyui
```

That's it — one install in any project, on any Claude surface (Claude Code,
claude.ai, the Agent SDK). All reference files are bundled; nothing else to
download. Update later with `/plugin marketplace update shadcn-daisyui`.

## Use without the plugin

Copy the skill folder into a project (or `~/.claude/skills/` for all projects):

```sh
cp -r skills/design-system <your-project>/.claude/skills/
```

Or, for a non-Claude context, drop the single-file bundle into the repo:

```sh
curl https://n00nday.github.io/shadcn_daisyui/design-guidelines.md > DESIGN.md
```

## What's inside

```
.claude-plugin/{plugin,marketplace}.json   plugin + self-hosted marketplace
skills/design-system/
  SKILL.md                                 always-loaded core rules + index
  references/*.md                          10 detail files, loaded on demand
```

## Source of truth

The reference files are **generated**, not authored here. The canonical source
is `usage-rules/*.md` in the
[shadcn_daisyui](https://github.com/N00nDay/shadcn_daisyui) repo, which also
feeds the docs site, the Phoenix `usage_rules` sync, and the Swift package's
bundled guidelines. After editing the canonical files, run
`scripts/sync_design_consumers.sh` in that repo to propagate the change here and
to the Swift bundle — one edit, everywhere. Do not edit `references/` by hand.

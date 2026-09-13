# apple-design

**English** | [简体中文](README.zh-CN.md)

A [Claude Code](https://claude.com/claude-code) skill/plugin that turns Apple's official [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) into ready-to-use reference material for designing and reviewing user interfaces on iOS, iPadOS, macOS, watchOS, and visionOS (with tvOS notes where relevant).

> This is an independent, community-maintained project. It is not affiliated with, endorsed by, or sponsored by Apple Inc. "Apple," "iOS," "macOS," and the other platform/technology names used here are trademarks of Apple Inc., used only to describe the subject matter of this content.

## Why this exists

Apple's design guidance shifts almost every year around WWDC — most notably the 2025 introduction of the **Liquid Glass** design language, which rebuilt materials, icons, and control appearance across iOS/iPadOS/macOS. An LLM's training data can easily be stale or mix up specs across platforms. This skill gives Claude a curated, paraphrased, cross-linked summary of the HIG's most load-bearing content, plus a full sitemap of official URLs to fetch live when a precise number, component name, or the latest wording is needed — so answers stay grounded instead of guessed.

## What's inside

```
apple-design/
├── SKILL.md                          # Entry point: triggers, navigation, quick references
├── .claude-plugin/
│   ├── plugin.json                   # Plugin manifest (name: apple-design)
│   └── marketplace.json              # Marketplace manifest (name: tzzs)
└── references/
    ├── principles.md                 # The eight design principles
    ├── platforms.md                  # iOS / iPadOS / macOS / watchOS / visionOS characteristics
    ├── materials-color.md            # Materials, Liquid Glass, Color system
    ├── typography-symbols.md         # Fonts, Dynamic Type, SF Symbols
    ├── layout.md                     # Visual hierarchy, size classes, safe areas
    ├── accessibility.md              # Vision / hearing / mobility / speech / cognitive
    ├── components.md                 # Buttons, Tab bars, Sidebars, Lists, Toolbars
    ├── app-icons.md                  # Layered icon design, Icon Composer
    ├── patterns-gestures.md          # Gesture design and common interaction patterns
    ├── resources.md                  # Official UI Kits, fonts, SF Symbols, Icon Composer
    └── hig-sitemap.md                # Full HIG URL index for live lookups
```

The content follows a progressive-disclosure structure: `SKILL.md` stays short and routes to the right `references/*.md` file for the topic at hand, and `hig-sitemap.md` gives Claude the exact URL to fetch live whenever a summary isn't enough.

## Install

### As a Claude Code plugin (recommended)

```bash
claude plugin marketplace add tzzs/apple-design-skill
claude plugin install apple-design@tzzs
```

Verify it's active:

```bash
claude plugin list
```

### As a personal skill (symlink, no plugin system)

```bash
git clone https://github.com/tzzs/apple-design-skill.git
ln -s "$(pwd)/apple-design-skill" ~/.claude/skills/apple-design
```

Personal skills load at session start, so open a new Claude Code session afterward.

## Usage

Once installed, the skill triggers automatically on Apple-platform UI design questions — you don't need to name it explicitly. For example:

- "How should I handle a Liquid Glass tab bar over a colorful gradient background?"
- "Does this onboarding flow follow Apple's guidelines?"
- "Which SF Symbol rendering mode should I use for a status indicator?"
- "What's the minimum tap target size on visionOS?"

You can also invoke it directly with `/apple-design` if your client supports slash-command skill invocation.

## Updating

```bash
cd apple-design-skill
git pull
claude plugin marketplace update tzzs
claude plugin update apple-design@tzzs
```

## Content and licensing notes

- The prose in `references/` paraphrases and summarizes Apple's official documentation in the authors' own words — it is not a verbatim copy, and each file cites its official source URL for anyone who needs exact wording.
- Numeric specs (point sizes, contrast ratios, hit target sizes, etc.) are facts, not creative expression, and are reproduced directly from Apple's documentation for accuracy — but they change over time, so always spot-check precision-critical values against the live HIG page linked from [references/hig-sitemap.md](references/hig-sitemap.md).
- This repository's own content (the Markdown files, manifests, and this README) is offered under the [MIT License](LICENSE) unless noted otherwise. Apple's underlying documentation remains Apple's copyright.

## Contributing

Issues and pull requests are welcome — especially reports of stale specs after a WWDC update, or gaps in coverage. Since the HIG has 100+ pages, this skill intentionally covers the most frequently needed ones in depth and relies on [references/hig-sitemap.md](references/hig-sitemap.md) for everything else; PRs that add a missing summary file following the existing structure are appreciated.

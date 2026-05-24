# Buddhist Method — a Claude Code plugin

A Claude Code plugin that packages a skill encoding six Buddhist epistemic and decision-making principles as practical work disciplines for Claude (or any LLM-driven workflow). Each principle targets a specific failure mode that LLMs routinely exhibit: pattern-matching instead of verifying, patching symptoms instead of removing causes, capitulating under social pressure instead of holding to evidence.

> 🇹🇭 อ่าน [README.th.md](README.th.md) สำหรับเวอร์ชันภาษาไทย

## What's in here

A Claude Code plugin that bundles one skill (`SKILL.md` plus `references/`) giving Claude a checklist for:

| Principle | What it catches |
|-----------|-----------------|
| **Kalāma** (กาลามสูตร) | Stating facts from pattern memory without verifying |
| **Yoniso Manasikāra** (โยนิโสมนสิการ) | Treating symptoms instead of finding root causes |
| **Sati-Sampajañña** (สติ-สัมปชัญญะ) | Acting on stale or remembered state |
| **Anatta** (อนัตตา) | Patching a fundamentally wrong draft instead of rewriting |
| **Pahāna** (ปหานะ) | Workarounds that hide bugs instead of removing them |
| **Upekkhā** (อุเบกขา) | Capitulating under user pressure or thrashing under tool failures |

Plus deeper references for harder situations:
- The **Four Noble Truths** as a debugging frame (`references/ariyasacca-debug.md`)
- **Apāyakosalla** — recognizing decline / anti sunk-cost
- **Appamāda** — heedfulness across long tasks
- **Sappurisadhamma (3 of 7)** — knowing self / time / audience
- **Atthatraya** — short-term vs long-term benefit trade-offs
- **Majjhimā Paṭipadā** — the middle way for solution sizing

## Why keep the Pali / Thai names

The Pali names are kept on purpose. They are mnemonic keys — each name retrieves a complete, well-developed pattern that a paragraph of plain English does not retrieve as cleanly. *Yoniso manasikāra* pulls in the whole discipline of attention to causes; "root cause analysis" loses the framing of attention itself.

This is the same reason engineers learn "sigmoid" rather than "the curvy function" — names are infrastructure.

The skill is **not** a religious framework. It does not require belief, ritual, or commitment to any tradition. It is a checklist with cultural roots, presented honestly. For the principles in their full traditional depth, read the suttas — this skill makes no claim to teach them.

## How to use

### Install as a Claude Code plugin (recommended)

From inside Claude Code, run these two slash commands:

```
/plugin marketplace add snilli/buddhist-method
/plugin install buddhist-method@buddhist-method
```

The first command registers this repo as a one-plugin marketplace. The second installs the plugin from it. After install, Claude Code auto-discovers the skill — the description in `SKILL.md` is enough for Claude to know when to load the full body, so there is nothing to wire up by hand.

To remove later: `/plugin uninstall buddhist-method@buddhist-method`.

### Install locally without the marketplace

If you want to hack on the plugin or pin it to a specific clone:

```bash
git clone https://github.com/snilli/buddhist-method ~/path/to/buddhist-method
```

Then launch Claude Code with the plugin directory pointed at it:

```bash
claude --plugin-dir ~/path/to/buddhist-method
```

### With other Claude products

Anywhere skills are supported, drop the `skills/buddhist-method/` directory in. The structure is standard (a `SKILL.md` with YAML frontmatter, plus `references/`).

### As a reference for yourself

The `skills/buddhist-method/SKILL.md` and accompanying `references/` are readable on their own. Each principle has a **trigger** (when it fires) and an **action** (what to do). You can use them as a personal checklist without involving an LLM.

### Make it always active (optional)

By default, Claude loads the skill on demand — it sees the description from the plugin manifest and decides whether to read the full `SKILL.md` based on the task at hand. That is fine for most uses, and it keeps your context budget free for everything else.

If you want the skill to be a persistent reminder regardless of task, add a small pointer to your `CLAUDE.md`:

```markdown
## Working method
For tasks involving factual claims, debugging, user pushback,
or long multi-step work, consult the buddhist-method skill
before responding.
```

Two places you can put this:

- **Project root `CLAUDE.md`** — applies only when working in that project.
- **`~/.claude/CLAUDE.md`** — applies globally across all your Claude Code sessions.

The pointer is only a few lines, so it doesn't bloat your context. Claude still loads the body of the skill progressively when triggers fire — you are just guaranteeing that the skill stays on Claude's radar.

## Structure

```
buddhist-method/
├── .claude-plugin/
│   ├── plugin.json                      # plugin manifest
│   └── marketplace.json                 # marketplace catalog (single-plugin repo)
├── skills/
│   └── buddhist-method/
│       ├── SKILL.md                     # six core principles + dispatch
│       └── references/
│           ├── ariyasacca-debug.md      # Four Noble Truths as debug frame
│           └── extended-principles.md   # five secondary principles
├── README.md                            # this file
├── README.th.md                         # Thai version
└── LICENSE                              # MIT
```

## License

MIT. Use, modify, and redistribute freely. See [LICENSE](LICENSE).

## Contributing

Issues and pull requests welcome. Particularly interested in:
- Failure modes the current principles don't catch.
- Better triggers (more specific situations that should fire each principle).
- Translations into other languages where the source tradition is alive.

If proposing a new principle, please show:
1. The specific failure mode it catches.
2. A concrete trigger and action.
3. Why an existing principle doesn't already cover it.

The bar is keeping the skill tight. New principles are easy to add; what's hard is keeping the set small enough to actually be used.

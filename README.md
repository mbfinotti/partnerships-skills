# Skills for Partnership teams

> Partner ecosystem operations, from channel program design to creator payouts.

A collection of agent skills covering the full **partnerships** surface: channel and alliance strategy, co-selling policy, affiliate program mechanics, referral incentives, and influencer deals.

Built for **partner managers, BD leads, affiliate managers, and ecosystem heads** who own partner revenue.

Every skill produces a **decision-ready artifact**: a scorecard, a policy, a rate card, a signed-off spec, not a generic checklist.

## Install

Install every skill in this repo, not just one. Skills here are atomic by design and reference each other freely — picking a single skill leaves its sibling skills uninstalled, so cross-references and routed handoffs go nowhere.

**skills.sh (universal)** — works with any Agent Skills-compatible tool:

```bash
npx skills add mbfinotti/partnerships-skills
```

**Claude Code** — install the plugin:

```bash
/plugin marketplace add mbfinotti/mbfinotti
/plugin install partnerships-skills@mbfinotti
```

**Codex (OpenAI)** — install via the Codex CLI:

```bash
codex plugin add github:mbfinotti/partnerships-skills
```

**Cursor** — copy into Cursor's skills directory:

```bash
git clone https://github.com/mbfinotti/partnerships-skills.git ~/.cursor/skills/partnerships-skills
```

Cursor auto-discovers skills from `.agents/skills/` and `.cursor/skills/`.

**Gemini CLI** — install as a Gemini extension:

```bash
gemini extensions install https://github.com/mbfinotti/partnerships-skills
```

Update with `gemini extensions update partnerships-skills`.

## Skills

This collection covers the full partnerships surface. Start here:

- [`partnerships-kickoff`](./partnerships-kickoff) — Routes a partnerships task to exactly one sibling skill and bootstraps the shared project context file so the next session starts warm.

Browse all skills and their descriptions in [`references/skill-catalog.md`](./references/skill-catalog.md).

## Related Collections

Other Nativa Labs skill repositories:

- [`advertising-skills`](https://github.com/mbfinotti/advertising-skills) — Ad platform mastery — _for performance marketers, paid media managers, growth leads_
- [`revops-skills`](https://github.com/mbfinotti/revops-skills) — Revenue operations — _for RevOps managers, sales ops, marketing ops, CRM admins_
- [`sales-skills`](https://github.com/mbfinotti/sales-skills) — Sales execution — _for SDRs, AEs, sales managers, heads of sales_

## License

MIT © 2026 Maya-Beth Finotti

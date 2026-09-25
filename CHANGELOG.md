# Changelog

Version is tracked in `SKILL.md` under `metadata.mystilink.version` and in this file.

## 0.1.0

- Agent Skill for western natal charting and reading
- `scripts/astro_chart_calculate.py` emits planets, houses, and aspects from birth time and place
- `references/overview.md` maps chart fields to Mystilink Wiki theory pages (`wiki.mystilink.com`)
- `examples/profile.json` and `examples/profile.v0.json` give runnable chart input
- Runtime: `python3` with the `pyswisseph` package; the Wiki lookup is optional
- Install by copying this directory into a host skills path that reads `SKILL.md`

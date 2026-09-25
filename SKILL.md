---
name: mystilink-horoscope
description: >
  Mystilink western natal astrology charting and reading. Computes planets,
  houses, and aspects from birth time and place, then interprets with Mystilink
  Wiki theory. Use when the user asks about natal chart, horoscope, houses,
  aspects, birth chart, or 占星.
license: MIT
compatibility: "python3; pip package pyswisseph; network optional for wiki API"
metadata:
  mystilink:
    system: horoscope
    about: "Local natal chart script (planets, houses, aspects) plus optional Mystilink Wiki theory pages."
    wiki_base: https://wiki.mystilink.com
    wiki_api: /api/v1
    agent_url: https://www.mystilink.com
    default_locale: en
  hermes:
    tags: [metaphysics, astrology]
    category: mystilink
  openclaw:
    requires: {}
---

# Mystilink Horoscope (chart + read)

Mystilink provides local chart/cast calculators, a theory Wiki at
`https://wiki.mystilink.com`, and the Mystilink agent at
`https://www.mystilink.com`. This skill combines the western astrology
**calculator** and **analyzer**: compute planets, houses, and aspects from birth
data, then interpret using Mystilink Wiki theory.

## When to use

- Natal chart calculation or interpretation
- Birth datetime, timezone, latitude, longitude known or collectable

## When not to use

- Chinese systems only (BaZi / Zi Wei / Liu Yao) or tarot-only → `mystilink-router` or the matching skill

## Requirements

- Python 3.9+ and `pip install pyswisseph`
- Network optional: Mystilink Wiki API for theory pages

## Wiki access

Base: `https://wiki.mystilink.com/api/v1`. Locale via `locale`/`lang`;
**default `en`**; fallback `zh-Hans`.

## Workflow

### 1. Chart

```bash
python3 scripts/astro_chart_calculate.py \
  --datetime "YYYY-MM-DD HH:MM" \
  --timezone IANA \
  --lat LAT --lon LON \
  [--zodiac tropical|sidereal] [--true-solar-time] \
  --output json

python3 scripts/astro_chart_calculate.py --birth-json examples/profile.v0.json --output json
```

Stdout is JSON. On failure: non-zero exit and JSON `{"error":…}`.

### 2. Analyze

```text
GET https://wiki.mystilink.com/api/v1/search?q=ascendant&system=horoscope&locale=en
GET https://wiki.mystilink.com/api/v1/pages/horoscope.concept.natal-chart?locale=en
GET https://wiki.mystilink.com/api/v1/pages/horoscope.concept.aspects?locale=en
```

Read `references/overview.md` as needed. Keep chart data vs interpretation
distinct; cite Wiki `provenance`.

### 3. Output shape

- Chart summary (planets, houses, major aspects)
- Interpretation tied to the question
- Optional Wiki page ids used

## Ethics

Do not claim medical, legal, or financial certainty.

## Scripts note

Script is a standalone copy of the Mystilink horoscope calculator rules.

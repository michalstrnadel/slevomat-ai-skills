# Contributing — Slevomat AI Skills

Krátký guide jak přidat nový skill do této kolekce.

## Struktura skillu

Každý skill je ve své složce s následující strukturou:

```
<skill-name>/
├── README.md                  ← Popis pro lidi: kdy použít, jak instalovat, příklady
├── SKILL.md                   ← Skill instrukce ve formátu pro Claude Code / Claude.ai
├── <reference>.md             ← Volitelně: zdrojový dokument, který skill čte
│                                (např. design-principles.md, DESIGN.md)
├── PROMPT.md                  ← Volitelně: single-file portable prompt
│                                (skill + reference v jednom, ready-to-paste)
└── <skill-name>.zip           ← Předbalený ZIP pro Claude.ai upload
                                 (obsahuje SKILL.md + reference soubory ve složce)
```

## SKILL.md frontmatter

Drž frontmatter **minimální** — jen `name` a `description`. Jinak Claude.ai parser odmítne nahrání.

```yaml
---
name: skill-name
description: Krátký popis (1–3 věty), který obsahuje účel skillu, kdy se použít, a klíčové trigger fráze.
---
```

**Špatně** (Claude.ai to nesnese):

```yaml
---
name: "skill-name"
owner: "..."
version: "0.1.0"
triggers:
  - "trigger 1"
  - "trigger 2"
---
```

Triggery zmiň v textu `description:`. Owner / version / metadata můžeš dát do HTML komentářů pod frontmatter.

## Pravidla obsahu

- **Jazyk:** SKILL.md česky (uživatelská logika), ale `description` v frontmatteru anglicky (parser ho čte do system promptu).
- **Délka:** Cíl ~250–400 řádků SKILL.md. Pokud potřebuješ víc, vytáhni reference do separátního `.md` souboru.
- **Příklady:** 2–3 reálné příklady (Happy path / Edge case / Vágní vstup). Žádné lorem ipsum.
- **Anti-patterns:** Sekce "NEDĚLEJ" s explicitním seznamem chyb, které skill nesmí udělat.
- **Word budget:** Pokud skill generuje text output, urči explicitní word budget per sekce (např. "pozorování max 25 slov, doporučení max 20 slov").

## ZIP

Předbalený ZIP umožní lidem nahrát skill do Claude.ai bez Git znalostí.

```bash
# z root mono-repa
mkdir -p /tmp/zip-build/<skill-name>
cp <skill-name>/SKILL.md <skill-name>/*.md /tmp/zip-build/<skill-name>/
cd /tmp/zip-build && zip -r <skill-name>.zip <skill-name>/
mv <skill-name>.zip ../slevomat-ai-skills/<skill-name>/
```

## Test

Před PR otestuj skill na **3 vstupech**:

1. **Happy path** — typický use case, skill by měl vrátit kvalitní output
2. **Edge case** — vágní / minimální vstup, skill by měl klást clarify otázky
3. **Adversarial** — vstup mimo rozsah, skill by měl odmítnout / přesměrovat

## PR

1. Fork repa
2. Vytvoř větev `add-<skill-name>`
3. Přidej skill složku se všemi soubory výše
4. Aktualizuj `README.md` (top-level) — přidej řádek do tabulky **Skilly**
5. Otevři PR s krátkým popisem: kdo skill bude používat, jaký problém řeší, vzorek output

Owner kolekce (Michal Strnadel) PR review — typicky během pár dnů.

## Existující skilly jako vzor

- **[design-check](./design-check/)** — text + image input, multi-section structured output, citace ze zdrojového dokumentu
- **[slevomat-rapid-prototype](./slevomat-rapid-prototype/)** — text input, single-file artifact output (HTML), čte design primer

## Kontakt

Otázky / nápady na nové skilly: michal.strnadel@slevomat.cz nebo přes GitHub issues v tomto repu.

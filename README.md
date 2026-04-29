# Slevomat AI Skills

> Curated kolekce AI skillů pro produktové, designové a research workflow ve Slevomatu.
> Inspirováno [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) a [awesome-design-md](https://github.com/VoltAgent/awesome-design-md).

**Status:** Aktivně rozvíjeno · **Owner:** Michal Strnadel (Design Lead) — michal.strnadel@slevomat.cz

---

## Skilly

| Skill | Pro koho | Co dělá | Status |
|---|---|---|---|
| [**design-check**](./design-check/) | PM, designer, exec | Posuzuje featuru, screen nebo screenshot mockupu proti **7 designovým principům Slevomatu**. Vrací kompaktní strukturovaný feedback (Hit / Concern / Violation / Cannot tell) + Top 3 akce + verdikt. | v0.1 |
| [**slevomat-rapid-prototype**](./slevomat-rapid-prototype/) | Kdokoli | Z volného popisu vyrobí **single-file HTML prototyp** ve Slevomat stylu. Žádné dependencies, žádný build, otevřitelné dvojklikem. Komplementární k Mini*S Design System pro 30sekundovou ideaci. | v0.1 |

---

## Jak skill používat

### A) Claude Code desktop app (nejvíc komfortní)

1. Naklonuj repo nebo stáhni jeho ZIP
2. Zkopíruj požadovaný skill do `~/.claude/skills/<skill-name>/`
3. Otevři Claude Code v projektu, který chceš touchnout
4. Napiš trigger frázi (viz README v každé skill složce)

### B) Claude.ai (přes Skills upload)

Každý skill má v složce předbalený `*.zip` soubor. V Claude.ai:

1. Skills panel → **+** → **Create skill** → **Upload a skill**
2. Vyber `<skill-name>.zip` z této kolekce
3. Skill se aktivuje napsáním trigger fráze

### C) Bez uploadu (paste prompt)

Některé skilly mají `PROMPT.md` (single-file portable). Otevři ho v Raw view, copy → paste do první zprávy v chatu (Claude / Gemini / GPT).

---

## Roadmap

Plánované skilly (kontribuce vítány — viz [CONTRIBUTING.md](./CONTRIBUTING.md)):

- [ ] **heuristic-analysis** — Nielsen 10 + Octalysis 8 + dark patterns audit pro feature/screen
- [ ] **product-critique** — VVFR (Value-Viability-Feasibility-Risk) kritika produktového nápadu
- [ ] **decision-memo** — Strukturovaný 1-page decision memo z volných poznámek
- [ ] **exec-summary** — 1-page sumarizace dlouhého dokumentu pro management
- [ ] **opportunity-scoring** — RICE/ICE scoring nápadů pro backlog
- [ ] **user-stories-invest** — User stories v INVEST formátu + acceptance criteria

---

## Kontext: kde žije Slevomat AI

| Vrstva | Repo | Účel |
|---|---|---|
| **Hub (interní)** | [slevomat-ai-hub](https://github.com/slevomat/design-slevomat-context) | Centralizovaná knowledge base + všechny skilly + brand context. Pro lidi co mají přístup. |
| **Public skills** (tady) | slevomat-ai-skills | Veřejně sdílené skilly pro tým + design komunitu. Standalone, bez závislosti na hubu. |
| **Mini*S Design System** | [minis-design-system](https://github.com/slevomat/minis-design-system) | Real produkční design system (Lit web components, tokeny, Storybook). |

---

## Licence

© Slevomat Group, s.r.o. Sdíleno jako open reference pro design komunitu — můžeš číst, citovat, inspirovat se. Pokud skill přebíráš pro vlastní projekt, prosím odkazuj zpět a uveď zdroj. Pro komerční přepoužití kontaktuj michal.strnadel@slevomat.cz.

---

## Přispívání

Viz [CONTRIBUTING.md](./CONTRIBUTING.md) — krátký guide jak přidat nový skill.

---

*Sestaveno společně s Claude Code (Opus 4.7), 2026-04-29.*

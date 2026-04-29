# Slevomat AI Skills

> Curated kolekce AI skillů pro produktové, designové a research workflow ve Slevomatu.
> Inspirováno [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) a [awesome-design-md](https://github.com/VoltAgent/awesome-design-md).

**Status:** Aktivně rozvíjeno · **Owner:** Michal Strnadel (Design Lead) — michal.strnadel@slevomat.cz

---

## ⚡ Rychlá instalace (Claude Code, Mac/Linux)

> ⚠️ **Tyhle příkazy se spouští v Terminal.app, NE v Claude Code chatu!**
> Claude Code chat čeká na pokyny v přirozeném jazyce, ne shell commands.

### Cesta 1: Terminal.app (3 kroky)

1. Otevři **Terminal.app** (Cmd+Space → napiš "Terminal" → enter)
2. Zkopíruj příkaz dole, paste do Terminálu, enter
3. Restart Claude Code (Cmd+Q + znovu otevři)

```bash
git clone https://github.com/michalstrnadel/slevomat-ai-skills.git /tmp/sas && cp -r /tmp/sas/{design-check,slevomat-rapid-prototype} ~/.claude/skills/ && rm -rf /tmp/sas
```

### Cesta 2: Nech Claude Code, ať skilly nainstaluje sám

Otevři Claude Code v jakékoliv složce a v chatu napiš:

> Stáhni Slevomat AI skills z `https://github.com/michalstrnadel/slevomat-ai-skills` a nainstaluj `design-check` a `slevomat-rapid-prototype` do `~/.claude/skills/`.

Claude tě požádá o povolení Bash příkazů → klikni Allow → hotovo.

### Ověření

V Claude Code napiš `/skill list` — měl bys vidět oba skilly v "Personal skills".

**Jen jeden skill?** Klikni na řádek v tabulce dole — README skillu má install one-liner pro něj samotný.
Jiné cesty (Claude.ai upload, paste prompt, symlink pro auto-update) → [sekce Instalace](#instalace) níže.

---

## Skilly

| Skill | Pro koho | Co dělá | Status |
|---|---|---|---|
| [**design-check**](./design-check/) | PM, designer, exec | Posuzuje featuru, screen nebo screenshot mockupu proti **7 designovým principům Slevomatu**. Vrací kompaktní strukturovaný feedback (Hit / Concern / Violation / Cannot tell) + Top 3 akce + verdikt. | v0.1 |
| [**slevomat-rapid-prototype**](./slevomat-rapid-prototype/) | Kdokoli | Z volného popisu vyrobí **single-file HTML prototyp** ve Slevomat stylu. Žádné dependencies, žádný build, otevřitelné dvojklikem. Komplementární k Mini*S Design System pro 30sekundovou ideaci. | v0.1 |

---

## Instalace

### A) Claude Code (desktop app nebo CLI) — doporučeno

**Jednorázová instalace všech skillů (Mac/Linux):**

```bash
# 1. Naklonuj repo do dočasné složky
git clone https://github.com/michalstrnadel/slevomat-ai-skills.git /tmp/sas

# 2. Zkopíruj skilly do ~/.claude/skills/
mkdir -p ~/.claude/skills
cp -r /tmp/sas/design-check ~/.claude/skills/
cp -r /tmp/sas/slevomat-rapid-prototype ~/.claude/skills/

# 3. Úklid
rm -rf /tmp/sas
```

**Updaty (když přidáme nový skill nebo opravíme existující):**

```bash
git clone https://github.com/michalstrnadel/slevomat-ai-skills.git /tmp/sas && \
cp -rf /tmp/sas/design-check ~/.claude/skills/ && \
cp -rf /tmp/sas/slevomat-rapid-prototype ~/.claude/skills/ && \
rm -rf /tmp/sas
```

**Alternativa — symlink (auto-updates s `git pull`):**

```bash
git clone https://github.com/michalstrnadel/slevomat-ai-skills.git ~/slevomat-ai-skills
mkdir -p ~/.claude/skills
ln -s ~/slevomat-ai-skills/design-check ~/.claude/skills/design-check
ln -s ~/slevomat-ai-skills/slevomat-rapid-prototype ~/.claude/skills/slevomat-rapid-prototype
# Update kdykoliv:  cd ~/slevomat-ai-skills && git pull
```

**Po instalaci:** restart Claude Code session (zavři a otevři okno). Skill se aktivuje napsáním trigger fráze v chatu (viz README každého skillu).

### B) Claude.ai (web) — přes Skills upload

Každý skill má v složce předbalený `*.zip` soubor. V Claude.ai:

1. Skills panel → **+** → **Create skill** → **Upload a skill**
2. Stáhni ZIP z GitHubu:
   - design-check: [slevomat-design-check.zip](./design-check/slevomat-design-check.zip)
   - rapid-prototype: [slevomat-rapid-prototype.zip](./slevomat-rapid-prototype/slevomat-rapid-prototype.zip)
3. Vyber stažený ZIP, klikni Upload
4. Skill se aktivuje napsáním trigger fráze v konverzaci

### C) Bez instalace (paste prompt do chatu)

Některé skilly mají `PROMPT.md` (single-file portable). Otevři ho v GitHub Raw view, copy → paste do první zprávy v chatu (Claude / Gemini / GPT). Druhá zpráva = vstup pro skill.

design-check má [PROMPT.md](./design-check/PROMPT.md) připravený pro tenhle režim.

### Ověření instalace (Claude Code)

V Claude Code chatu napiš:

```
/skill list
```

(nebo otevři Skills panel v desktop app — Slevomat skilly by měly být v sekci "Personal skills".)

Pokud skilly nevidíš:
- Zkontroluj, že jsi je zkopíroval do `~/.claude/skills/` (ne `~/.claude/Skills/` nebo jinam — case sensitive)
- Restartuj Claude Code
- Ověř, že každý skill má `SKILL.md` v root své složky (ne v podsložce)

---

## Roadmap

Plánované skilly (kontribuce vítány — viz [CONTRIBUTING.md](./CONTRIBUTING.md)):

- [ ] **heuristic-analysis** — Nielsen 10 + Octalysis 8 + dark patterns audit pro feature/screen
- [ ] **product-critique** — VVFR (Value-Viability-Feasibility-Risk) kritika produktového nápadu
- [ ] **decision-memo** — Strukturovaný 1-page decision memo z volných poznámek
- [ ] **exec-summary** — 1-page sumarizace dlouhého dokumentu pro management
- [ ] **opportunity-scoring** — RICE/ICE scoring nápadů pro backlog

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

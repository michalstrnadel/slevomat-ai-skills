# Slevomat Rapid Prototype

> AI skill, který z volného popisu udělá **single-file HTML prototyp** ve Slevomat stylu.
> Žádné `pnpm`, žádný build, žádný terminál — jen popis → soubor → otevřít dvojklikem v prohlížeči.

**Status:** v0.2.0 (2026-04-29)
**Visibility:** Public — open reference pro Slevomat tým a design komunitu.
**Owner:** Michal Strnadel — michal.strnadel@slevomat.cz

---

## ⚡ Rychlá instalace

**Claude Code (Mac/Linux):**

```bash
git clone https://github.com/michalstrnadel/slevomat-ai-skills.git /tmp/sas && cp -r /tmp/sas/slevomat-rapid-prototype ~/.claude/skills/ && rm -rf /tmp/sas
```

Po instalaci: restart Claude Code, napiš `rapid prototype` + popis featury.

**Claude.ai (web):**

Stáhni [`slevomat-rapid-prototype.zip`](./slevomat-rapid-prototype.zip) → Skills panel → **+** → **Upload a skill** → vyber ZIP.

---

## Proč to existuje

Slevomat má skvělý [Mini*S Design System](https://slevomat.github.io/minis-design-system/) s [vibe-coding workflow](https://slevomat.github.io/minis-design-system/?path=/story/introduction--vibe-coding-guide) — Node.js + pnpm + dev server + real Lit web components. Pro **plné prototypy** je to top.

**Tento skill je pro něco jiného:** **30sekundovou ideaci.**

- Produkťák / researcher / designer dostane nápad během schůzky
- Otevře Claude Code desktop app, napíše "udělej prototyp X"
- Za chvíli má hotový `.html` soubor, otevřitelný dvojklikem
- Iteruje hlasem: "udělej tmavší", "přidej druhý variant", "přesuň hero nahoru"
- Když je nápad ověřený → přejdou na plný Mini*S workflow nebo Figmu

**Klíčový rozdíl od Mini*S:**

| | Mini*S workflow | Tento skill |
|---|---|---|
| Setup | Node.js + pnpm + build | Žádný |
| Output | Real working web components | Plain HTML+CSS, jen vizuálně podobné |
| Komponenty | `<minis-button>` etc. (Lit) | `<button class="btn">` (CSS classes) |
| Výchozí scénář | 15–60 min (full prototype) | 30 sec (sketch) |
| Cílová skupina | Designeři + frontend devs | Kdokoli (PM, research, exec) |
| Iterace | Edit projektu v editoru | "Udělej tmavší" v chatu |

---

## Co je uvnitř

| Soubor | Co obsahuje |
|---|---|
| [`SKILL.md`](./SKILL.md) | AI skill: instrukce, workflow, anti-patterns, příklady. Frontmatter kompatibilní s Claude.ai i Claude Code. |
| [`DESIGN.md`](./DESIGN.md) | **Slevomat design primer** — 9 sekcí (Visual Theme, Color Palette, Typography, Components, Layout, Elevation, Do's/Don'ts, Responsive, Agent Prompt Guide). Tokeny převzaté z reálného Mini*S `tokens.rgb.json`. Inspirováno [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) formátem. |
| [`slevomat-rapid-prototype.zip`](./slevomat-rapid-prototype.zip) | Předbalený ZIP pro upload do Claude.ai (Skills → + → Upload a skill). |

---

## Použití

### A) Claude Code desktop app (doporučeno)

1. Stáhni `slevomat-rapid-prototype.zip` (nebo `git clone` celý repo)
2. Rozbal do `~/.claude/skills/slevomat-rapid-prototype/` (nebo do skill složky tvého projektu)
3. Otevři Claude Code desktop app
4. V chatu napiš:
   > "Použij rapid prototype skill — udělej landing page pro novou kategorii Wellness Tipy"
5. Skill se aktivuje, eventuálně se zeptá na 1–2 otázky, pak vyrobí `prototype-{slug}.html` v aktuální složce
6. Otevři soubor dvojklikem ve Finderu / Průzkumníkovi
7. Iteruj v chatu: "udělej tmavší", "přidej druhý variant", "přesuň CTA dolů"

### B) Claude.ai (přes Skills upload)

1. Stáhni `slevomat-rapid-prototype.zip`
2. V Claude.ai → Skills panel → **+** → **Create skill** → **Upload a skill**
3. Vyber ZIP, klikni Upload
4. V konverzaci napiš trigger phrase (např. "rapid prototype" + popis)
5. Pozn.: Claude.ai ti soubor nemůže uložit na disk — vrátí HTML kód, který si musíš sám zkopírovat do `.html` souboru a otevřít

### C) Bez uploadu, paste prompt do chatu

1. Otevři raw verzi [`SKILL.md`](./SKILL.md) a [`DESIGN.md`](./DESIGN.md)
2. Paste obsah obou do první zprávy v chatu (Claude / Gemini / GPT)
3. Druhá zpráva: "Použij to a udělej prototyp X"

---

## Triggery

Skill se aktivuje, když napíšeš v chatu jednu z těchto frází:

- `rapid prototype`
- `slevomat-rapid-prototype`
- `udělej prototyp` / `udělej mockup`
- `rychlý prototyp`
- `slevomat sketch`
- `vytvoř mockup`

Příklad full prompt:
> Udělej rychlý prototyp homepage hero sekce pro novou kategorii Wellness Tipy — featured deal + 3 karty + tlačítko "Zobrazit všechno".

---

## Co dostaneš

**Single `.html` soubor** s:
- Inter font (CDN)
- Reálné Slevomat tokeny (color, type, spacing) jako CSS custom properties
- Embedded CSS — žádné externí stylesheets
- Sémantické HTML (header, main, nav, article)
- Mobile-first responsive (1 desktop breakpoint)
- WCAG AA kontrast
- Plausible Slevomat content (CZ destinace, reálné ceny v Kč, reálné kategorie)
- Unsplash placeholder fotky (CDN, žádné lokální assety)

**Co nedostaneš:**
- Funkční JavaScript (jen CSS hover/focus stavy)
- Real Mini*S web components — to vyžaduje plný setup
- Více souborů (vždy jeden `.html`)

---

## Klíčová pravidla

> **Single file. No dependencies. No build.**
>
> Cíl je, aby kdokoli ve firmě mohl prototyp poslat e-mailem nebo přetáhnout do Slacku, příjemce dvojklikne a vidí to v prohlížeči.

> **Plain HTML, ne Mini*S web components.**
>
> Skill píše `<button class="btn btn-primary">`, ne `<minis-button variant="primary">`. Druhé vyžaduje pnpm setup, čemuž se vyhýbáme. Vizuálně to ale vypadá stejně — tokeny jsou stejné.

> **Reálná data, ne lorem ipsum.**
>
> Plausible Slevomat content: Krkonoše, Saské Švýcarsko, Vysoké Tatry, ceny v Kč, kategorie Wellness/Pobyty/Adrenalin. Žádné "Card title 1".

---

## Pending / co můžeš přidat

- **Chybějící komponenty z Mini*S** — DESIGN.md zatím pokrývá Topbar, Category nav, Container, Button, Card, Tag, Alert, Card grid. Mini*S má víc (pill-counter, message, icon library, hero variants). Doplnit z `docs/ai-prompts/components/`.
- **Dark mode** — Mini*S má dark tokeny, ale tento skill je default light only. Dark mode přidat jako variant.
- **Více layoutů** — checkout flow, account dashboard, partner portal — pokud je potřeba.
- **Page templates** — místo čistě komponent dát i hotové templates (deal detail, listing, checkout step) jako copy-paste výchozí body.
- **Real fonts hosting** — pokud máte legal omezení na Google Fonts CDN, přepnout na self-hosted.
- **Logo asset** — nyní text "slevomat.cz", ideálně inline SVG logo z brand booku.

---

## Vztah k Mini*S

Tenhle skill **není náhradou** za Mini*S. Mini*S je production-grade, real komponenty s focus states, accessibility, atd.

Tenhle skill je **rychlá rampa**:

1. **Ideace** (tento skill, 30 sec) → "vypadá to dobře, jdeme dál"
2. **Plný prototyp** (Mini*S vibe-coding, 15 min) → "real komponenty, předáme devs"
3. **Implementace** (vývoj proti Mini*S) → "production"

Pokud uživatel rovnou potřebuje real komponenty, skill ho odkáže na vibe-coding-guide.

---

## Bezpečnost

- Skill negeneruje real Slevomat data — pouze fiktivní plausible obsah (žádná real partnerská jména, žádné real ID).
- Repo neobsahuje žádné firemní citlivé údaje (jen brand styling a designové patterny).

---

## Licence

© Slevomat Group, s.r.o. Sdíleno jako open reference pro design komunitu — můžeš číst, citovat, inspirovat se. Pokud skill přebíráš pro vlastní projekt, prosím odkazuj zpět na tento repo a uveď zdroj. Pro komerční přepoužití kontaktuj michal.strnadel@slevomat.cz.

Tokeny v `DESIGN.md` pochází z [Mini*S Design System](https://slevomat.github.io/minis-design-system/) — tamtéž platí jejich licenční podmínky.

---

*Sestaveno společně s Claude Code (Opus 4.7), 2026-04-29.*

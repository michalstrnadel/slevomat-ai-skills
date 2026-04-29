---
name: slevomat-rapid-prototype
description: Generates a single-file HTML prototype in the Slevomat visual style by adapting the bundled EXAMPLE.html template. Output is one self-contained .html file with embedded CSS — no build, no npm, no dependencies. The skill takes the working example, swaps in user-specific content, and saves to cwd. Use when a PM, researcher, or designer wants a fast Slevomat-flavored mockup. Triggers on "rapid prototype", "udělej prototyp", "rychlý prototyp", "slevomat sketch".
---

<!-- owner: michal.strnadel@slevomat.cz -->
<!-- version: 0.2.0 -->

## Co skill dělá

Bere hotový `EXAMPLE.html` (working Slevomat wellness listing) a přepisuje ho podle uživatelova zadání. Output: jeden `.html` soubor v cwd, otevíratelný dvojklikem v prohlížeči.

**Kritické: skill template UPRAVUJE, NEGENERUJE od nuly.** Tím se eliminuje "prázdná karta" failure mode.

## Workflow

### 1. Read templates
Přečti **VŠECHNY 3 SOUBORY** vedle SKILL.md:
- `EXAMPLE.html` — kompletní pracovní prototyp (topbar, nav, hero, card grid). **Toto je tvoje výchozí kostra.**
- `DESIGN.md` — tokeny + skeleton template + curated Unsplash URLs per kategorie
- (volitelně) `design-principles.md` pokud existuje vedle skillu

### 2. (Volitelné) Fetch real data
Pokud user explicitně chce reálná data ze slevomat.cz, zkus `WebFetch` na příslušnou kategorii (`/cestovani`, `/wellness`, `/restaurace`, `/adrenalin-zazitky`, `/zbozi`). Vytáhni 3–6 reálných dealů. Pokud fetch selže (rate limit, network egress block), **graceful skip** — pokračuj s Unsplash URLs z DESIGN.md.

### 3. Adapt EXAMPLE.html
Vezmi kompletní HTML z `EXAMPLE.html` jako základ a uprav:
- **Title + H1** podle zadání
- **Category nav active state** podle kategorie
- **Karty** — ponech strukturu, vyměň: titulek, lokalita, cena (current + original), tag, foto URL
- **Počet karet** — default 6, jinak co user řekne
- **Případně přidej** — alert, jiný hero text

**NIKDY** nezačínej z prázdné stránky. **VŽDY** kopíruj z EXAMPLE.html.

### 4. Save & deliver
- Soubor: `prototype-{slug}.html` v cwd (`{slug}` = kebab-case z hlavního tématu)
- Report: cesta + 3 bullety co je v prototypu + "otevři dvojklikem"

## Kritická pravidla

1. **🚫 NIKDY emoji jako fotku** (🏔️ 💆 🍷 atd.) — vždy real Unsplash URL z DESIGN.md tabulky, fetched URL ze slevomatu, nebo šedý placeholder. Emoji OK jen pro malé ikony (♡ ★ 🛒).
2. **Vyplň každou kartu** plausible CZ obsahem — žádné prázdné karty, žádné "Card title 1". Pokud nevíš jméno hotelu, vymysli plausible (Hotel Horizont, Penzion Krkonoše, Lázeňský dům Smetana…).
3. **Single file** — vše v jednom `.html`. Embedded CSS v `<style>`. Žádný JS.
4. **Neotvírej soubor** (`open ...`) bez explicitní žádosti.
5. **Iterace** = edit existing file, ne nový. "Udělej tmavší" → load + edit + save přes stejný soubor.

## Jeden příklad

**User:** "Rapid prototype — wellness listing pro Vysoké Tatry, 6 karet."

**Skill:**
1. Read EXAMPLE.html (wellness template).
2. Skip fetch (user neřekl).
3. Adapt:
   - Title → "Wellness Vysoké Tatry — Slevomat"
   - H1 → "Wellness ve Vysokých Tatrách"
   - Category nav: Wellness active (už je v template)
   - 6 karet — vyměň hotely za TATRY-flavored (Hotel Tatra, Vila Lomnica, Spa Štrbské Pleso, …), foto URL na "Vysoké Tatry" Unsplash z DESIGN.md, ceny 3–8k Kč, lokality (Štrbské Pleso, Tatranská Lomnica, …)
4. Save `prototype-wellness-tatry.html`.
5. Report: cesta + obsah.

## Anti-patterns

- ❌ Generování od nuly bez použití EXAMPLE.html (vyústí v prázdné karty)
- ❌ Emoji jako card-image
- ❌ "Lorem ipsum", "Card 1", "Description here"
- ❌ JS knihovny (Bootstrap, Tailwind, Alpine, React)
- ❌ Více souborů (vždy jeden `.html`)
- ❌ Nezohlednění anti-patternů z DESIGN.md (4+ akcentových barev, blikající banners)

## Reference

- `EXAMPLE.html` — pracovní template (mandatory startovní bod)
- `DESIGN.md` — tokeny + Unsplash URL tabulka + skeleton
- [Mini*S Design System](https://slevomat.github.io/minis-design-system/) — pro plné prototypy s real komponenty

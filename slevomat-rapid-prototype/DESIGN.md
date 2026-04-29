# Slevomat Rapid Prototype — DESIGN.md

> Design primer pro single-file HTML prototypy ve Slevomat stylu. Žádné dependencies, žádný build, otevřitelné dvojklikem v prohlížeči.
> Inspirováno [awesome-design-md formátem](https://github.com/VoltAgent/awesome-design-md). Tokeny pochází z reálného [Mini*S Design System](https://slevomat.github.io/minis-design-system/) (`tokens.rgb.json`).

---

## 1. Visual Theme & Atmosphere

**Mood:** Důvěryhodný, kultivovaný, autentický — ne marketingový. Slevomat ukazuje, že "i bohatá nabídka může vypadat přehledně". Není to strohý minimalismus, ale ani blikající leták. Prototyp by měl působit jako reálný produkt, ne jako wireframe.

**Atmosféra:**
- Klidná, čitelná, přívětivá
- Akcent výhody bez křiku (badge, ne pulzující červený banner)
- Reálné fotky lifestyle / zážitek (Unsplash placeholder), ne stock vektory
- Mobile-first, ale ne na úkor desktop layoutu

**Co se vyhnout:** Stockové marketingové ilustrace, gradienty na CTA, blikající animace, přeplácaná layouty se 4+ barevnými akcenty.

---

## 2. Color Palette & Roles

Vlož tyhle tokeny do `<style>` na začátku `:root` v každém prototypu:

```css
:root {
  /* Primary brand */
  --color-primary: #006eb9;            /* Slevomat blue, hlavní interaction */
  --color-primary-hover: #005685;
  --color-primary-focus: #00b2e5;

  /* CTA buy (green — kupní akce, "Koupit") */
  --color-cta-buy: #088107;
  --color-cta-buy-hover: #066506;

  /* Feedback */
  --color-success: #088107;
  --color-success-light: #e9fce9;
  --color-error: #d2381d;
  --color-error-light: #ffefec;
  --color-warning: #ffa400;
  --color-info: #006eb9;
  --color-info-light: #e6f3fb;

  /* Text */
  --color-text-primary: #000000;
  --color-text-secondary: #6b6b70;
  --color-text-on-primary: #ffffff;
  --color-text-link: #006eb9;

  /* Surface / Background */
  --color-background: #fcfdff;
  --color-surface: #ffffff;
  --color-surface-faded: #f1f3f5;

  /* Borders */
  --color-border: #cbccce;
  --color-border-subtle: #e3e4e6;
  --color-border-strong: #616266;

  /* Special — pricing/discount accent */
  --color-discount: #d2381d;        /* červená pro slevu, ale střídmě */
  --color-original-price: #6b6b70;  /* přeškrtnutá cena */
}
```

**Pravidla použití:**
- **Primary blue** je pro odkazy, primary buttons, focus states. Ne pro disclosure / urgency.
- **CTA-buy zelená** výhradně pro "Koupit" / "Objednat" / "Rezervovat" tlačítka. Ne pro "Zobrazit detail".
- **Discount červená** pro slevové prvky, nikdy jako primární akce. Per princip #3: "nemusí křičet".
- **Max 1 akcentová barva per slide / sekce.** Nemíchej zelenou CTA a červenou slevu vedle sebe ve stejné vizuální vrstvě.

---

## 3. Typography Rules

**Font stack:** Inter (Google Fonts CDN).

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap">
```

```css
:root {
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

  /* Size scale */
  --text-xs: 12px;
  --text-sm: 14px;
  --text-base: 16px;
  --text-lg: 18px;
  --text-xl: 20px;
  --text-2xl: 24px;
  --text-3xl: 32px;
  --text-4xl: 40px;
  --text-display: 48px;

  /* Weights */
  --weight-regular: 400;
  --weight-medium: 500;
  --weight-semibold: 600;
  --weight-bold: 700;
  --weight-black: 900;

  /* Line heights */
  --leading-tight: 1.2;
  --leading-normal: 1.5;
  --leading-relaxed: 1.6;
}
```

**Hierarchie:**
- **H1 / Page title:** `--text-3xl` až `--text-display`, `--weight-bold` nebo `--weight-black`, `--leading-tight`
- **H2 / Section:** `--text-2xl`, `--weight-bold`
- **H3 / Card title:** `--text-lg`, `--weight-semibold`
- **Body:** `--text-base`, `--weight-regular`, `--leading-normal`
- **Caption / Meta:** `--text-sm`, `--color-text-secondary`
- **Button label:** `--text-base`, `--weight-semibold`

---

## 4. Component Stylings

> Prototypy používají **plain HTML + CSS**. Žádné `<minis-button>` web components, žádný JS framework. Třídy reprezentují komponenty z Mini*S.

### Button

```html
<button class="btn btn-primary">Pokračovat</button>
<button class="btn btn-cta-buy">Koupit za 2 153 Kč</button>
<button class="btn btn-secondary">Zrušit</button>
<button class="btn btn-tertiary">Zobrazit více</button>
```

```css
.btn {
  display: inline-flex; align-items: center; gap: 8px;
  font-family: var(--font-sans); font-size: var(--text-base);
  font-weight: var(--weight-semibold); line-height: 1;
  padding: 12px 20px; border-radius: 8px; border: 1px solid transparent;
  cursor: pointer; transition: background 120ms ease, border 120ms ease;
}
.btn-primary { background: var(--color-primary); color: var(--color-text-on-primary); }
.btn-primary:hover { background: var(--color-primary-hover); }
.btn-cta-buy { background: var(--color-cta-buy); color: var(--color-text-on-primary); }
.btn-cta-buy:hover { background: var(--color-cta-buy-hover); }
.btn-secondary { background: var(--color-surface); color: var(--color-text-primary); border-color: var(--color-border); }
.btn-secondary:hover { background: var(--color-surface-faded); }
.btn-tertiary { background: transparent; color: var(--color-primary); padding: 8px 12px; }
.btn-tertiary:hover { background: var(--color-info-light); }
```

### Topbar (page header)

```html
<header class="topbar">
  <div class="topbar-inner">
    <a class="logo" href="/">slevomat<span>.cz</span></a>
    <nav class="topbar-actions">
      <button class="btn btn-tertiary">♡ Oblíbené</button>
      <button class="btn btn-primary">🛒 Košík</button>
    </nav>
  </div>
</header>
```

```css
.topbar { background: var(--color-surface); border-bottom: 1px solid var(--color-border-subtle); padding: 12px 0; }
.topbar-inner { max-width: 1200px; margin: 0 auto; padding: 0 24px;
  display: flex; justify-content: space-between; align-items: center; }
.logo { font-size: 22px; font-weight: var(--weight-bold); color: var(--color-primary); text-decoration: none; }
.logo span { color: var(--color-text-primary); }
.topbar-actions { display: flex; gap: 12px; align-items: center; }
```

### Category navigation (under topbar)

```html
<nav class="category-nav">
  <div class="container">
    <a class="cat-link active" href="#">Extra slevy</a>
    <a class="cat-link" href="#">Cestování</a>
    <a class="cat-link" href="#">Wellness</a>
    <a class="cat-link" href="#">Restaurace</a>
    <a class="cat-link" href="#">Zboží</a>
  </div>
</nav>
```

```css
.category-nav { background: var(--color-surface); border-bottom: 1px solid var(--color-border-subtle); }
.category-nav .container { display: flex; gap: 4px; overflow-x: auto; padding: 0 24px; }
.cat-link { padding: 16px 16px; color: var(--color-text-primary); text-decoration: none;
  font-weight: var(--weight-medium); border-bottom: 2px solid transparent; white-space: nowrap; }
.cat-link.active { color: var(--color-primary); border-bottom-color: var(--color-primary); }
.cat-link:hover { color: var(--color-primary); }
```

### Container

```html
<main class="container">…content…</main>
```

```css
.container { max-width: 1200px; margin: 0 auto; padding: 24px; }
.container-narrow { max-width: 720px; margin: 0 auto; padding: 24px; }
```

### Product card (typical Slevomat listing tile)

```html
<article class="card">
  <div class="card-image" style="background-image: url('https://images.unsplash.com/photo-…?w=600')">
    <button class="card-fav" aria-label="Oblíbené">♡</button>
  </div>
  <div class="card-pricing">
    <div class="price-current">2 153 Kč</div>
    <div class="price-original">2 825 Kč</div>
  </div>
  <div class="card-tag">First minute až 15 %</div>
  <h3 class="card-title">Saské Švýcarsko: 3* hotel s polopenzí</h3>
  <p class="card-meta">AHORN Waldhotel Altenberg · Německo · 2 dny</p>
</article>
```

```css
.card { background: var(--color-surface); border: 1px solid var(--color-border-subtle);
  border-radius: 12px; overflow: hidden; transition: box-shadow 120ms ease; }
.card:hover { box-shadow: 0 4px 12px rgba(0,0,0,0.08); }
.card-image { height: 200px; background-size: cover; background-position: center; position: relative; }
.card-fav { position: absolute; top: 12px; right: 12px; width: 36px; height: 36px;
  border-radius: 50%; border: none; background: rgba(255,255,255,0.9);
  font-size: 18px; cursor: pointer; }
.card-pricing { display: flex; gap: 8px; align-items: baseline; padding: 12px 16px 4px; }
.price-current { font-size: var(--text-xl); font-weight: var(--weight-bold); color: var(--color-text-primary); }
.price-original { font-size: var(--text-sm); color: var(--color-original-price); text-decoration: line-through; }
.card-tag { display: inline-block; padding: 4px 8px; background: var(--color-error-light);
  color: var(--color-discount); font-size: var(--text-xs); font-weight: var(--weight-semibold);
  border-radius: 4px; margin: 0 16px; }
.card-title { font-size: var(--text-lg); font-weight: var(--weight-semibold); margin: 8px 16px 4px; line-height: var(--leading-tight); }
.card-meta { font-size: var(--text-sm); color: var(--color-text-secondary); margin: 0 16px 16px; }
```

### Tag / Pill

```html
<span class="tag">Wellness</span>
<span class="tag tag-success">Volné termíny</span>
<span class="tag tag-warning">Posledních 5 ks</span>
```

```css
.tag { display: inline-block; padding: 4px 10px; border-radius: 9999px;
  background: var(--color-surface-faded); color: var(--color-text-primary);
  font-size: var(--text-xs); font-weight: var(--weight-medium); }
.tag-success { background: var(--color-success-light); color: var(--color-success); }
.tag-warning { background: rgba(255,164,0,0.15); color: #b87800; }
.tag-error { background: var(--color-error-light); color: var(--color-discount); }
```

### Alert

```html
<div class="alert alert-info">ℹ️ Akce platí do 31. 5. 2026.</div>
<div class="alert alert-success">✓ Vaše rezervace byla úspěšně odeslána.</div>
```

```css
.alert { padding: 12px 16px; border-radius: 8px; border-left: 4px solid;
  font-size: var(--text-sm); margin: 16px 0; }
.alert-info { background: var(--color-info-light); border-color: var(--color-info); color: var(--color-text-primary); }
.alert-success { background: var(--color-success-light); border-color: var(--color-success); color: var(--color-text-primary); }
.alert-error { background: var(--color-error-light); border-color: var(--color-error); color: var(--color-text-primary); }
```

### Grid (card listing)

```html
<section class="card-grid">
  <article class="card">…</article>
  <article class="card">…</article>
  <article class="card">…</article>
</section>
```

```css
.card-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 24px; }
```

---

## 5. Layout Principles

- **Container max-width:** 1200px (default), 720px (narrow — checkout/forms)
- **Side padding:** 24px desktop, 16px mobile
- **Section spacing:** 48–64px mezi sekcemi (`margin-top: 48px`)
- **Element spacing scale:** 4 / 8 / 12 / 16 / 20 / 24 / 32 / 40 / 48 / 64 px
- **1 myšlenka = 1 sekce** — nepřeplňuj viewport více než 2 hlavními bloky najednou

**Page structure (typical):**
```
┌─ Topbar (logo + actions) ─────────────────────┐
├─ Category nav ─────────────────────────────── ┤
├─ Container ──────────────────────────────────┤
│   Hero / page title                          │
│   Main content (cards / sections / forms)    │
│   CTA section                                │
├─ Footer (volitelné) ──────────────────────────┤
└──────────────────────────────────────────────┘
```

---

## 6. Depth & Elevation

Slevomat používá decentní stíny — žádné dramatické 3D efekty.

```css
:root {
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.08);
  --shadow-lg: 0 8px 24px rgba(0, 0, 0, 0.12);
}
```

**Použití:**
- `--shadow-sm` — subtle separation (sticky topbar)
- `--shadow-md` — card hover, modal default
- `--shadow-lg` — modal active, dropdown

---

## 7. Do's and Don'ts

| ✅ Do | ❌ Don't |
|---|---|
| 1 hlavní akcent per sekce | 4 barevné akcenty soupeřící (red box + green box + coral text + heart) |
| Tichá deadline ("Akce končí 31. 5.") | Animovaný odpočet + blikající "Kupte teď!" |
| Reálné lifestyle fotky (Unsplash) | Stock vektory / marketingové ilustrace |
| Konkrétní čísla ("12 % sleva", "Ušetříte 380 Kč") | "Až 50 %" hedge + dvě přeškrtnuté ceny |
| Inter font, čistá typografie | Comic Sans, multiple font families v jedné stránce |
| Mobile-first layout (default 1 column → grid při ≥768px) | Desktop-only fixní šířky |
| Decentní stíny (`shadow-sm/md`) | Dramatické 3D tlačítka s gradientem |
| WCAG AA kontrast (text 4.5:1, UI 3:1) | Bílý text na světle modrém pozadí |
| Logické tab order, klávesnicová navigace | Mouse-only interakce, custom click handlers |

---

## 8. Responsive Behavior

**Breakpointy:**
```css
/* mobile-first — default styles platí <768px */
@media (min-width: 768px) { /* tablet */ }
@media (min-width: 1008px) { /* desktop */ }
@media (min-width: 1480px) { /* wide */ }
```

**Pravidla:**
- **Touch target min 44×44 px** (button, link, ikon)
- **Card grid:** 1 sloupec mobile, 2 tablet, 3-4 desktop (`auto-fill, minmax(280px, 1fr)` to dělá automaticky)
- **Topbar actions:** plné na desktop, `icon-only` na mobile (skryj label, ukaž ikonku)
- **Container padding:** 16px mobile, 24px tablet+
- **Type scale:** display/h1 menší na mobile (32px) než desktop (48px)

---

## 9. Agent Prompt Guide

Když píšeš HTML, drž se těchto pravidel:

1. **Single-file output.** Veškeré CSS v `<style>` v `<head>`. Žádné `<link rel="stylesheet" href="local.css">`.
2. **Pouze tyhle externí dependencies:**
   - Google Fonts (`fonts.googleapis.com/css2?family=Inter:…`)
   - Reálné fotky (viz pravidlo 6 níže — buď ze slevomat.cz nebo z Unsplash s přesnými URL)
   - Pro malé ikony (heart ♡, košík 🛒, hvězdičky ★) je OK Unicode emoji NEBO inline SVG, NIKDY emoji jako hlavní fotka karty / hero / banner
3. **Použij CSS custom properties** z této DESIGN.md, ne magic values. Pokud hodnota chybí, použij nejbližší token.
4. **Sémantické HTML** — `<header>`, `<main>`, `<article>`, `<nav>`, `<section>`, `<button>` (ne `<div onclick>`).
5. **Czech jazyk** — všechny labely, tlačítka, nadpisy. Žádné "Submit", "Cancel" — vždy "Odeslat", "Zrušit".
6. **🚫 ABSOLUTNÍ ZÁKAZ EMOJI JAKO FOTKY.** Žádný 🏔️, 💆, 🍷, 🏖️, 🍝, 🏨 v `card-image`, hero pozadí, nebo jakémkoli místě, kde má být fotka. Vždy použij **reálnou fotku** — buď:
   - **(a) Reálný produkt ze slevomat.cz** (preferred, viz pravidlo 11) s odkazem na real obrázek z `slevomat-cdn.akamaized.net/...`
   - **(b) Unsplash URL podle kategorie** (z curated tabulky níže)
   - **(c) Šedý placeholder** `<div style="background: var(--color-surface-faded); ...">` — pokud opravdu žádnou fotku nemáš
7. **Žádný JavaScript** ledaže si uživatel explicitně vyžádá — prototyp má vypadat funkčně, ale nemusí být funkční (klikací stavy = `:hover`, `:focus` v CSS).
8. **Kontrast a přístupnost** — WCAG AA min, `aria-label` na icon-only tlačítka, `alt` na obrázky.
9. **Mobile-first CSS** — defaultní styly pro mobile, `@media (min-width: 768px)` pro desktop overrides.

### 9a. Curated Unsplash URLs per kategorie

Pokud nepoužíváš real slevomat.cz fotky (pravidlo 11), vyber z této tabulky podle obsahu karty:

| Kategorie / téma | Unsplash URL (fixní photo ID) |
|---|---|
| Hotel / pobyt obecně | `https://images.unsplash.com/photo-1542314831-068cd1dbfeeb?w=600&h=400&fit=crop` |
| Krkonoše / hory ČR | `https://images.unsplash.com/photo-1601999094016-7f0fda3b1eed?w=600&h=400&fit=crop` |
| Wellness / sauna | `https://images.unsplash.com/photo-1540555700478-4be289fbecef?w=600&h=400&fit=crop` |
| Lázně / spa | `https://images.unsplash.com/photo-1571902943202-507ec2618e8f?w=600&h=400&fit=crop` |
| Moře / pláž | `https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=600&h=400&fit=crop` |
| Restaurace / jídlo | `https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=600&h=400&fit=crop` |
| Víno / degustace | `https://images.unsplash.com/photo-1510812431401-41d2bd2722f3?w=600&h=400&fit=crop` |
| Vysoké Tatry | `https://images.unsplash.com/photo-1502786129293-79981df4e689?w=600&h=400&fit=crop` |
| Adrenalin / hory v zimě | `https://images.unsplash.com/photo-1551698618-1dfe5d97d256?w=600&h=400&fit=crop` |
| Saské Švýcarsko / Německo | `https://images.unsplash.com/photo-1505765050516-f72dcac9c60e?w=600&h=400&fit=crop` |
| Chorvatsko / Středomoří | `https://images.unsplash.com/photo-1555990538-32202a08a8ec?w=600&h=400&fit=crop` |
| Praha / město | `https://images.unsplash.com/photo-1541849546-216549ae216d?w=600&h=400&fit=crop` |
| Český Krumlov | `https://images.unsplash.com/photo-1610016302534-6f67f1c968d8?w=600&h=400&fit=crop` |
| Beauty / kosmetika | `https://images.unsplash.com/photo-1487412947147-5cebf100ffc2?w=600&h=400&fit=crop` |
| Dárkový voucher | `https://images.unsplash.com/photo-1513885535751-8b9238bd345a?w=600&h=400&fit=crop` |

**Použití v HTML:**
```html
<div class="card-image" style="background-image: url('https://images.unsplash.com/photo-1601999094016-7f0fda3b1eed?w=600&h=400&fit=crop')"></div>
```

### 9b. Default behaviors (zmenšuje počet iterací)

Když user neřekne jinak, default to:

- **Layout:** Topbar → Category nav → Container → 1 hero/H1 sekce → 1 hlavní obsah (grid karet nebo form) → optional sekundární CTA. Žádné footers (zaberou screenshot space, většinou nedávají hodnotu).
- **Card grid:** 3 karty per row na desktop (`auto-fill, minmax(280px, 1fr)`), 1 column mobile.
- **Karta = obrázek + cena (current + původní strikethrough) + tag (volitelně) + titulek + meta (lokalita + délka)**. Tlačítko na karte ne — celá karta klikací (cursor: pointer).
- **Primary CTA = 1 per page** (ne na každé kartě). Listing → CTA "Zobrazit všechny [kategorie]" pod gridem.
- **Hero:** plná šířka, max-height 400px, fotka + overlay + 1 nadpis + 1 podtitulek + 1 CTA. Žádný carousel, žádné multiple slides.
- **Hodnocení na kartě:** ⭐ + číslo + počet ("⭐ 4.8 · 86 hodnocení"). Ne 5 ikonek hvězdiček.
- **Cena formát:** `2 153 Kč` (mezera tisícovek, "Kč" nezalomené), original price `2 825 Kč` v `--color-original-price`, strikethrough.

### 9c. Anti-patterns (časté chyby)

- ❌ Emoji v card-image (🏔️, 💆, atd.)
- ❌ "Card title 1", "Description here", "Lorem ipsum"
- ❌ Tabbed interface bez JS (uživatel klikne, nic se nestane)
- ❌ 3+ akcentové barvy v jedné sekci
- ❌ Animace odpočtu, blikající banner, "Kupte teď!"
- ❌ Modal/popup bez close handle
- ❌ `<img>` bez `alt`
- ❌ Stock vektorové ilustrace (Unsplash je real photo, ne ilustrace)

**Kostra každého prototypu:**

```html
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{{ Název stránky }} — Slevomat</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap">
  <style>
    :root {
      /* tokens — color, type, spacing per sekce 2-3 nahoře */
    }
    *, *::before, *::after { box-sizing: border-box; }
    body { margin: 0; font-family: var(--font-sans); background: var(--color-background); color: var(--color-text-primary); }
    /* component styles */
  </style>
</head>
<body>
  <header class="topbar">…</header>
  <nav class="category-nav">…</nav>
  <main class="container">
    {{ tady je obsah prototypu }}
  </main>
</body>
</html>
```

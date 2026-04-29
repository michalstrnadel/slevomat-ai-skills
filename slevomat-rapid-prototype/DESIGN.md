# Slevomat Design Tokens — Rapid Prototype Reference

> Kompaktní reference: barvy, typo, spacing, key komponenty + Unsplash URLs.
> Tokeny z reálného [Mini*S Design System](https://slevomat.github.io/minis-design-system/).
> **Hlavní zdroj prototypu = `EXAMPLE.html`. Tento soubor je jen reference, když potřebuješ token nebo URL.**

## Tokens (CSS custom properties)

```css
:root {
  /* Brand */
  --color-primary: #006eb9;       /* Slevomat blue */
  --color-primary-hover: #005685;
  --color-cta-buy: #088107;       /* zelená "Vybrat termín / Koupit" */
  --color-cta-buy-hover: #066506;

  /* Feedback */
  --color-success: #088107; --color-success-light: #e9fce9;
  --color-error: #d2381d;   --color-error-light: #ffefec;
  --color-info: #006eb9;    --color-info-light: #e6f3fb;
  --color-warning: #ffa400;

  /* Text + Surface */
  --color-text-primary: #000;       --color-text-secondary: #6b6b70;
  --color-text-on-primary: #fff;    --color-text-link: #006eb9;
  --color-background: #fcfdff;      --color-surface: #fff;
  --color-surface-faded: #f1f3f5;
  --color-border: #cbccce;          --color-border-subtle: #e3e4e6;
  --color-discount: #d2381d;        --color-original-price: #6b6b70;

  /* Typography */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --text-xs: 12px; --text-sm: 14px; --text-base: 16px; --text-lg: 18px;
  --text-xl: 20px; --text-2xl: 24px; --text-3xl: 32px; --text-4xl: 40px;
  --weight-regular: 400; --weight-medium: 500; --weight-semibold: 600;
  --weight-bold: 700; --weight-black: 900;

  /* Spacing scale (4-8-12-16-20-24-32-40-48-64) */
  --sp-1: 4px; --sp-2: 8px; --sp-3: 12px; --sp-4: 16px; --sp-5: 20px;
  --sp-6: 24px; --sp-8: 32px; --sp-10: 40px; --sp-12: 48px; --sp-16: 64px;

  /* Radius */
  --radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px; --radius-full: 9999px;

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.08);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.12);
}
```

## Curated Unsplash URLs per kategorie

Vždy `?w=600&h=400&fit=crop` na konec.

| Kategorie | URL |
|---|---|
| Hotel obecně | `https://images.unsplash.com/photo-1542314831-068cd1dbfeeb` |
| Krkonoše / hory ČR | `https://images.unsplash.com/photo-1601999094016-7f0fda3b1eed` |
| Wellness / sauna | `https://images.unsplash.com/photo-1540555700478-4be289fbecef` |
| Lázně / spa | `https://images.unsplash.com/photo-1571902943202-507ec2618e8f` |
| Moře / pláž | `https://images.unsplash.com/photo-1507525428034-b723cf961d3e` |
| Restaurace / jídlo | `https://images.unsplash.com/photo-1414235077428-338989a2e8c0` |
| Víno / degustace | `https://images.unsplash.com/photo-1510812431401-41d2bd2722f3` |
| Vysoké Tatry | `https://images.unsplash.com/photo-1502786129293-79981df4e689` |
| Adrenalin / hory zima | `https://images.unsplash.com/photo-1551698618-1dfe5d97d256` |
| Saské Švýcarsko / DE | `https://images.unsplash.com/photo-1505765050516-f72dcac9c60e` |
| Chorvatsko / Středomoří | `https://images.unsplash.com/photo-1555990538-32202a08a8ec` |
| Praha / město | `https://images.unsplash.com/photo-1541849546-216549ae216d` |
| Český Krumlov | `https://images.unsplash.com/photo-1610016302534-6f67f1c968d8` |
| Beauty / kosmetika | `https://images.unsplash.com/photo-1487412947147-5cebf100ffc2` |
| Voucher / dárek | `https://images.unsplash.com/photo-1513885535751-8b9238bd345a` |

## Typický page pattern

```
Topbar (logo + Oblíbené + Košík)
  ↓
Category nav (Extra slevy / Cestování / Wellness / Restaurace / Adrenalin / Zboží)
  ↓
Container (max-width 1200px)
  ↓
Hero NEBO H1 + lead
  ↓
Filter chips (volitelně)
  ↓
Card grid (3 cols desktop, 1 col mobile, 280px min)
  ↓
Sekundární CTA
```

## Hard rules

1. **🚫 ŽÁDNÉ EMOJI** v `card-image` / hero / banner. Real Unsplash URL nebo šedý `<div>` placeholder.
2. **Inter font** přes Google Fonts CDN (preconnect + stylesheet v `<head>`).
3. **Mobile-first CSS** s 1 desktop breakpointem (`@media (min-width: 768px)`).
4. **Vyplň každou kartu real-feeling obsahem** — CZ destinace, ceny v Kč, plausible jména hotelů. Žádné prázdné karty.
5. **1 hlavní akcent per sekce** — buď zelená CTA-buy, nebo červený discount badge, ne obojí najednou.
6. **WCAG AA kontrast** — bílý text na primary blue OK; nepoužívej světlé na světlém.

## Když potřebuješ víc komponent

`EXAMPLE.html` má: topbar, category nav, breadcrumb, page-header, filter chips, info alert, card grid, card s tagem/cenou/strikethrough/hodnocením/CTA, footer.

Pro extra komponenty (modal, form, tabs, accordion) — píšeš sám podle tokenů výše. Drž patternům z `EXAMPLE.html` (radius, shadows, spacing).

# Typografie — průvodce

> Pomocný materiál pro fázi 3 (Vizuální identita) ve skillu `design-system`.

## Základní pravidlo

**Maximálně 2 fonty.** Jeden pro nadpisy, jeden pro běžný text. Třetí font = chaos.

Někdy stačí **jeden font**, jen v různých vahách (např. Inter Bold pro nadpisy, Inter Regular pro text).

## Volba fontu — co určuje styl značky

| Typ fontu | Charakter | Hodí se pro |
|-----------|-----------|-------------|
| **Serif (patkové)** — *Playfair, Merriweather, Lora* | Klasický, důvěryhodný, sofistikovaný | Luxus, vzdělávání, redakční |
| **Sans-serif (bezpatkové)** — *Inter, Manrope, DM Sans* | Moderní, čistý, jasný | Tech, B2B, většina webů |
| **Display (výrazné)** — *Bebas Neue, Anton, Archivo Black* | Silný, energický, reklamní | Headers, kampaně, akce |
| **Handwritten / script** — *Caveat, Pacifico* | Osobní, autentický | Citace, podpisy (ne pro body text!) |
| **Monospace** — *JetBrains Mono, Fira Code* | Technický, kódový | Tech blogy, dokumentace |

## Doporučení podle stylu značky

### Klid, hloubka, sebepoznání
- Nadpisy: **Playfair Display** (serif) nebo **Cormorant Garamond**
- Text: **Inter** nebo **Source Sans 3**

### Moderní, tech, profesionalita
- Nadpisy: **Manrope** Bold nebo **Inter** Bold
- Text: **Inter** Regular

### Hravost, lifestyle
- Nadpisy: **DM Serif Display** nebo **Fraunces**
- Text: **DM Sans** nebo **Nunito**

### Prémium, luxus
- Nadpisy: **Cormorant Garamond** nebo **Libre Bodoni**
- Text: **Lato** nebo **Inter**

### Energie, podnikání, akce
- Nadpisy: **Bebas Neue** nebo **Anton**
- Text: **Inter** nebo **Roboto**

### Zemitý, autentický, řemeslo
- Nadpisy: **Lora** nebo **Merriweather**
- Text: **Source Sans 3** nebo **Lato**

## Velikosti — hierarchie

Drž **konzistentní poměr** mezi úrovněmi. Doporučení (modular scale 1.25x - 1.5x):

### Desktop

| Element | Velikost | Line-height | Weight |
|---------|----------|-------------|--------|
| H1 | 48-64 px | 1.1 | 700 (Bold) |
| H2 | 36-48 px | 1.2 | 700 |
| H3 | 24-32 px | 1.3 | 600 (SemiBold) |
| H4 | 20-24 px | 1.4 | 600 |
| Body Large | 18-20 px | 1.6 | 400 |
| Body | 16-17 px | 1.6 | 400 |
| Small | 14-15 px | 1.5 | 400 |

### Mobil

| Element | Velikost |
|---------|----------|
| H1 | 32-40 px |
| H2 | 26-32 px |
| H3 | 20-24 px |
| Body | **16 px (nikdy méně!)** |
| Small | 14 px |

**Body text minimálně 16 px na mobilu** — jinak iOS automaticky přibližuje formuláře, což ruší layout.

## Line-height (řádkování)

- **Nadpisy:** 1.1 - 1.3 (těsně)
- **Body text:** **1.5 - 1.7** (pro pohodlné čtení)
- **Krátké popisky:** 1.4

Web s line-height 1.0 nebo 1.2 u body textu je nečitelný — písmena se "lepí".

## Šířka řádku (line length)

**Optimálně 50-75 znaků na řádek** (s mezerami). Kolem 600-700 px šířky textového bloku.

- Příliš úzký (méně než 40 znaků) → oči poskakují
- Příliš široký (víc než 90 znaků) → ztratíš se na konci řádku

I když web má full-width pozadí, **textový obsah omeziš na 600-700 px** a vycentruješ.

## Weight (váha) — kdy co

| Weight | Hodnota | Použití |
|--------|---------|---------|
| Thin / Light | 100-300 | Velké display nadpisy, ne pro body text! |
| Regular | 400 | Body text — default |
| Medium | 500 | Mírné zvýraznění (jména, čísla) |
| SemiBold | 600 | Podnadpisy, mírnější nadpisy |
| Bold | 700 | Hlavní nadpisy, klíčová slova v textu |
| Black / Heavy | 800-900 | Display, hero nadpisy, ne pro běžné použití |

## Pravidla pro psaní textu

### Krátké odstavce
- Max 4-5 řádků
- Mezi odstavci 1.5x line-height jako mezera
- Web není kniha — lidé skenují

### Zarovnání
- ✅ **Zarovnání doleva** — default pro body text
- ❌ **Zarovnání na střed** — jen pro nadpisy a krátké úvodní věty, NIKDY ne pro odstavce delší než 1 řádek
- ❌ **Justify (do bloku)** — vytváří nepříjemné mezery, používá se v tisku, ne na webu

### Zvýrazňování
- ✅ **Tučně** — hlavní zvýraznění
- ✅ Odlišná barva (zřídka, max 2-3 slova v odstavci)
- ❌ **Podtržení** — patří odkazům, jinde mate
- ❌ **KAPITÁLKY V CELÝCH ODSTAVCÍCH** — působí jako křik a hůř se čte

## Google Fonts — jak je použít

V kořeni HTML přidej:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
```

Načítej **jen ty váhy, které opravdu používáš** — každá váha = další stažení.

V CSS:
```css
body { font-family: 'Inter', system-ui, sans-serif; }
h1, h2, h3 { font-family: 'Playfair Display', serif; }
```

`system-ui, sans-serif` jako fallback — než se Google Font stáhne, zobrazí se systémový font.

## Časté chyby

- ❌ **3+ různé fonty** — vizuální chaos
- ❌ **Body text 14 px** — nečitelné
- ❌ **Černý text na bílé** — moc tvrdé, použij `#1A1A1A` nebo `#2C2C2C`
- ❌ **Žádná hierarchie** — H1 a body stejně velké, čtenář nevidí strukturu
- ❌ **Justify text** — nepravidelné mezery
- ❌ **Velké odstavce bez mezer** — zeď textu, lidi to přeskočí

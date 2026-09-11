# Barvy — průvodce

> Pomocný materiál pro fázi 3 (Vizuální identita) ve skillu `design-system`.

## Role barev v paletě

Každá barva má **jednu konkrétní práci**. Když má barva dvě role, vznikne chaos.

| Role | Co dělá | Kolik různých barev |
|------|---------|---------------------|
| **Primary** | Identita značky — co si lidi zapamatují | 1 |
| **Secondary** | Doplněk, jemné pozadí | 1 |
| **Accent / CTA** | Tlačítka *Koupit*, *Kliknout* — musí vyskočit | 1 |
| **Text** | Hlavní text | 1 (typicky tmavá šedá, ne čistá černá) |
| **Text Muted** | Poznámky, méně důležitý text | 1 (jasně světlejší než hlavní text) |
| **Background** | Pozadí stránky | 1 (typicky bílá nebo světle šedá) |
| **Surface** | Pozadí karet, sekcí | 1 |
| **Border** | Oddělovače, ohraničení polí | 1 |

**Celkem typicky 6-8 barev.** Méně je víc.

## Pravidlo 60-30-10

Klasické designové pravidlo:
- **60 % plochy** = neutrální (pozadí, bílá)
- **30 % plochy** = primary nebo secondary
- **10 % plochy** = accent (CTA tlačítka, klíčové akcenty)

Když je accent barva na 50 % plochy, ztratí svůj efekt — tlačítko nevyskočí.

## Psychologie barev (krátký přehled)

| Barva | Asociace | Hodí se pro |
|-------|----------|-------------|
| **Modrá** | Důvěra, klid, profesionalita | Tech, finance, zdraví, B2B |
| **Zelená** | Růst, příroda, zdraví, peníze | Wellness, eco, finance, vzdělávání |
| **Žlutá / oranžová** | Energie, pozornost, optimismus | CTA tlačítka, akce, dětská oblast |
| **Červená** | Naléhavost, vášeň, riziko | Slevy, urgence (pozor na přehánění) |
| **Fialová** | Luxus, kreativita, spirituální | Luxusní značky, kreativní obory, esoterika |
| **Černá / tmavé tóny** | Prémiový dojem, hloubka | Luxus, móda, sofistikované B2B |
| **Bílá / béžová** | Čistota, prostor, jednoduchost | Minimalistické značky, wellness |
| **Růžová** | Jemnost, ženskost, hravost | Beauty, lifestyle, pro ženy |
| **Hnědá / zemité** | Zemitost, autenticita, řemeslo | Bio, řemeslné značky, kavárny |

**Pozor:** kulturní rozdíly. Bílá = svatba (západ) vs. smutek (Asie). Pro česko-slovenský trh platí tyto asociace dobře.

## Kontrast — kritické pravidlo

CTA tlačítko musí mít **vysoký kontrast** vůči zbytku stránky. Pokud má web modré pozadí a tlačítko je tmavě modré, nikdo ho neuvidí.

**Standard čitelnosti (WCAG AA):**
- Body text na pozadí: kontrast min. **4.5:1**
- Velký text (18+ px): min. **3:1**
- CTA tlačítko vůči pozadí: ideálně **7:1+**

**Nástroj na kontrast:** https://webaim.org/resources/contrastchecker/ (zdarma, drž v záložkách)

## Konkrétní paletové kombinace (pro inspiraci)

### Klid, hloubka, sebepoznání
- Primary: tmavá modrofialová `#1A1F3A`
- Secondary: krémová `#F5EFE6`
- CTA: zlatá `#D4A857`
- Text: tmavě šedá `#2C2C2C`

### Energie, růst, podnikání
- Primary: tmavě zelená `#0F4C3A`
- Secondary: světle zelená `#E8F4EE`
- CTA: oranžová `#FF6B35`
- Text: tmavě šedá `#1F1F1F`

### Prémium, luxus, expert
- Primary: černá `#0A0A0A`
- Secondary: tmavě šedá `#1F1F1F`
- CTA: zlatá `#C9A961`
- Text: světlá šedá `#E5E5E5` (na tmavém pozadí)

### Lehký, vzdušný, wellness
- Primary: pastelová modrá `#A8C8E8`
- Secondary: krémová `#FAF7F2`
- CTA: korálová `#FF7B7B`
- Text: tmavě modrá `#2A4A6B`

## Nástroje pro tvorbu palety

- **Coolors** (https://coolors.co) — generátor palet, hodí se pro inspiraci
- **Adobe Color** (https://color.adobe.com) — color wheel, harmonie
- **Realtime Colors** (https://realtimecolors.com) — vidíš paletu rovnou na ukázce webu
- **Tailwind palette generator** — pokud používáš Tailwind, vygeneruje 50-950 odstíny

## Časté chyby

- ❌ **Příliš mnoho barev** — 4 různé barvy v jedné sekci, web vypadá jako cirkus
- ❌ **Nízký kontrast** — světle šedý text na bílém pozadí, nečitelné
- ❌ **CTA bez kontrastu** — tlačítko ve stejné barvě jako zbytek = nikdo neklikne
- ❌ **Čistá černá** — `#000000` na bílé je pro oči moc tvrdé. Použij `#1A1A1A` nebo `#2C2C2C`
- ❌ **Sytá červená všude** — vyvolává stres. Použij ji jen jako akcent (varování, sleva)

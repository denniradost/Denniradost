# Šablona výstupního souboru `design-system.md`

> Tohle je šablona pro finální výstup skillu `design-system`. Vyplň všechny sekce daty ze všech 4 fází
> a ulož jako `design-system.md` v kořeni projektu uživatele.

---

```markdown
# Design System — [název značky]

> **Jediný zdroj pravdy** pro vizuální a verbální identitu značky [název].
> Všechny weby, prodejní stránky, reklamy a materiály se drží tohoto dokumentu.
>
> **Vytvořeno:** [datum ISO]
> **Poslední update:** [datum ISO]

---

## 1. Značka

### Co děláme
[Jednou větou — produkt nebo služba.]

### Pro koho
[Cílovka — kdo to je, co řeší, kde se nachází.]

### Mise / příběh
[Proč to dělám. Co mě k tomu přivedlo.]

### Charakter značky (3-5 slov)
- [slovo 1] — [co znamená pro značku]
- [slovo 2] — [...]
- [slovo 3] — [...]

### Hodnoty (co NIKDY)
- ❌ [hodnota 1, kterou neporušuju]
- ❌ [hodnota 2]

### Inspirace
- [odkaz / značka 1] — [co se mi na ní líbí]
- [odkaz / značka 2]

---

## 2. Tone of voice

### Charakter hlasu
[3-5 přídavných jmen: např. "klidný, lidský, přímý, hloubkový, hravý"]

### Oslovení
- **Tykání / vykání:** [tykám / vykám]
- **Pohlaví:** [ženský / mužský / oboje s lomítkem / neutrální]

### Klíčová slova (často používaná)
- [slovo 1]
- [slovo 2]
- [slovo 3]
- [slovo 4]
- [slovo 5]

### Slova, kterým se vyhýbám
- ❌ [slovo 1]
- ❌ [slovo 2]
- ❌ [slovo 3]

### Příklad věty v duchu značky
> "[Konkrétní věta nebo krátký odstavec, kterým se prezentuje styl značky.]"

### Anti-příklad (tak NE)
> "[Věta, která zní cize nebo nesedí značce.]"

---

## 3. Vizuální identita

### Logo
- **Soubor:** [cesta nebo URL k logu]
- **Použití na světlém pozadí:** [popis]
- **Použití na tmavém pozadí:** [popis nebo varianta]
- **Minimální velikost:** [např. 24 px výška]

### Barevná paleta

| Role | Název | HEX | Použití |
|------|-------|-----|---------|
| **Primary** (hlavní) | [např. Tmavá modř] | `#XXXXXX` | Nadpisy, akcenty, klíčové prvky |
| **Secondary** (doplňková) | [název] | `#XXXXXX` | Pozadí sekcí, jemné prvky |
| **Accent** (CTA) | [název] | `#XXXXXX` | Tlačítka *Koupit*, *Zaregistrovat* |
| **Text** | [název] | `#XXXXXX` | Hlavní text |
| **Text Muted** | [název] | `#XXXXXX` | Podtitulky, méně důležitý text |
| **Background** | [název] | `#XXXXXX` | Pozadí stránky |
| **Surface** | [název] | `#XXXXXX` | Pozadí karet, sekcí |
| **Border** | [název] | `#XXXXXX` | Oddělovače, ohraničení |

### Typografie

**Font nadpisů:** [např. Playfair Display (Google Fonts)]
- H1: [velikost px / line-height / weight] — *použít pro hlavní nadpis stránky, jednou*
- H2: [px / line-height / weight] — *sekce*
- H3: [px / line-height / weight] — *podsekce*
- H4: [px / line-height / weight] — *menší nadpisy*

**Font body textu:** [např. Inter (Google Fonts)]
- Body: [px / line-height / weight] — *běžný text*
- Body Large: [px / line-height / weight] — *úvodní odstavec, perex*
- Small: [px / line-height / weight] — *poznámky pod čarou*

**Pravidla:**
- Body text minimálně 16-17 px na desktopu, 16 px na mobilu
- Krátké odstavce (max 4-5 řádků)
- Text zarovnaný doleva (nikdy na střed u delších textů)
- Důležité části tučně, ne podtrženě (podtržené patří odkazům)

### Fotografie a obrazový styl
- **Atmosféra:** [světlé/tmavé, teplé/chladné, lifestyle/produktové]
- **Lidé:** [autentické fotky / stock / oboje / žádné]
- **Ilustrace:** [styl: plochý / 3D / čárový / žádné]
- **Ikony:** [knihovna: Heroicons / Phosphor / Feather / vlastní]

### Mood / atmosféra
[3-5 slov + 1 věta popisující celkový dojem.]

---

## 4. Komponenty

### Tlačítka

**Primary CTA**
- Pozadí: [HEX]
- Text: [HEX]
- Hover: [HEX nebo efekt]
- Zaoblení: [px]
- Padding: [px vertical / horizontal]
- Velikost textu: [px]

**Secondary**
- Pozadí: [HEX nebo transparent]
- Text: [HEX]
- Ohraničení: [HEX, šířka]
- Hover: [efekt]

**Text Link**
- Barva: [HEX]
- Hover: [efekt — typicky podtržení]

### Sekce a layout
- **Max šířka obsahu:** [např. 1200 px]
- **Max šířka textového bloku:** [např. 680 px]
- **Spacing mezi sekcemi (desktop):** [px]
- **Spacing mezi sekcemi (mobil):** [px]
- **Tmavé sekce:** [kde se používají, pokud vůbec]

### Karty
- Pozadí: [HEX]
- Stín: [např. `0 4px 12px rgba(0,0,0,0.08)` nebo "žádný"]
- Zaoblení: [px]
- Padding: [px]
- Hover: [efekt: posun nahoru, zvýraznění stínu, atd.]

### Formuláře

**Input pole**
- Pozadí: [HEX]
- Ohraničení: [HEX, šířka]
- Zaoblení: [px]
- Focus: [HEX okraje]
- Padding: [px]

**Tlačítko submit:** stejné jako Primary CTA

### Responsive breakpointy
- Mobil: do 640 px
- Tablet: 641-1024 px
- Desktop: 1025+ px

---

## 5. Použití v dalších skillech

Když používáš skill `sales-page`, `presentation-web` nebo jiný web skill:

1. Skill nejdřív načte tento soubor
2. Drží se barev, fontů, tone of voice odsud
3. Pokud potřebuje něco, co tu není definované, zeptá se uživatele a doplní sem

**Tento soubor neměň ručně bez rozmyšlení** — změny se propíšou do všech budoucích webů.
```

---

## Doplněné sekce (v2.0 — celý design systém, ne jen web)

Do výstupního `design-system.md` přidej i tyhle sekce. Bez nich je to jen webový manuál.

```markdown
## Obrazový styl

- **Fotky:** vlastní / stock · atmosféra (světlé–tmavé, teplé–chladné) · co na nich je
- **Co na fotkách nikdy nebude:**
- **Ilustrace a ikony:** styl, nebo „nepoužíváme“
- **Chybějící záběry (zadání na focení):** portrét na světlém pozadí · práce s klientem · detail …

## Šablona e-mailu

- Šířka: 600 px (nebo 500 px) · jeden sloupec · rozvržení tabulkami · styly inline
- Font: {systémový font + řetězec záloh} · text {16–20} px · řádkování 1,5
- Tlačítko: HTML (ne obrázek) · barva {hex} · zaoblení {px}
- Obrázky: alternativní text vždy · průhledné PNG (tmavý režim)
- Preheader: skrytý první řádek · Patička: kdo píše, odkud adresa, odhlášení jedním klikem
- Limit: celé HTML pod 100 kB

## Šablony na sítě

- Formáty: 1 : 1 · 4 : 5 · 9 : 16
- Titulek v obrázku: font, velikost, zarovnání, max slov
- Barvy pozadí (světlá / tmavá varianta) · kde je logo
- Rozpoznávací prvek, který drží mřížku profilu pohromadě
- 2–3 opakovatelné šablony (víc si nikdo neudrží)

## Prezentace, PDF, e-book

- Titulní strana · běžná strana · velikost písma pro promítání (min. 24 px)
- Světlá i tmavá varianta (promítání vs. tisk) · kde je logo · poslední strana s výzvou

## Knihovna grafiky (odkud se berou obrázky)

- **Vlastní fotky mají vždycky přednost před stockem.**
- Kde bydlí: {knihovna assetů v aplikaci pro agenta · složka v projektu}
- Logo (varianty a formáty): {odkazy}
- Portréty a nejpoužívanější grafiky: {odkazy + k čemu se hodí}
- Čeho je málo: {seznam}

## Tone of voice

**Nepatří sem.** Jak značka mluví, drží samostatný stylový průvodce (skill `styl-komunikace`).
Tady je jen odkaz, ať se to nerozejde: {kde stylový průvodce leží}
```

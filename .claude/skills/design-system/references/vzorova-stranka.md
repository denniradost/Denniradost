# Vzorová stránka a přehled prvků

> K čemu to je: aby design systém nebyl jen popis, ale **něco, co se dá otevřít v prohlížeči
> a odkud se dá kopírovat.** Vzniknou tři soubory, které spolu drží.
> Naposledy změněno: 2026-08-06.

---

## Proč vzorová stránka, a ne jen přehled komponent

Přehled komponent (tlačítka vedle sebe, palety, ukázky písma) ukazuje **prvky**. Neukazuje ale,
jestli spolu **fungují na skutečné stránce** — jestli hero sekce nezabírá celou obrazovku, jestli
sekce po sobě dýchají, jestli po třetím odstavci ještě někdo čte.

Proto vznikají **dvě stránky, ne jedna**:

| | `ukazka.html` | `prvky.html` |
|---|---|---|
| Co to je | **reálná landing page** od hlavičky po patičku | **přehled prvků** — komponenta po komponentě |
| K čemu | pozná se, jestli vzhled funguje **v provozu** | odsud se **kopíruje** při stavbě další stránky |
| Texty | skutečné (produkty, nadpisy, reference) | popisné („Primární tlačítko“, „Kdy použít“) |
| Kdo se na ni dívá | majitel — schvaluje vzhled | agent i majitel — pracovní nástroj |

Obě si tahají hodnoty ze stejného **`tokens.css`**.

---

## Soubor 1: `tokens.css` (jediné místo, kde bydlí hodnoty)

Kostra. Konkrétní hodnoty vyplní fáze 2 a 3 skillu.

```css
/* ===========================================================
   <PROJEKT> · DESIGN TOKENS
   Master hodnot. Kdo chce barvu nebo font, bere si ji odsud.
   Změna hodnoty tady se promítne do všech stránek.
   =========================================================== */

:root {
  /* --- Barvy značky --- */
  --barva-hlavni: #000000;
  --barva-doplnkova: #000000;
  --barva-akcent: #000000;        /* jen na tlačítka a to, co má vyskočit */
  --barva-akcent-svetla: #000000;
  --barva-akcent-tmava: #000000;

  /* --- Plochy a text --- */
  --pozadi: #ffffff;
  --pozadi-sekce: #f7f7f7;
  --pozadi-karta: rgba(0,0,0,0.03);
  --text: #1a1a1a;                /* tmavě šedá, ne čistá černá */
  --text-tlumeny: #5a5a5a;
  --oddelovac: rgba(0,0,0,0.08);

  /* --- Písmo --- */
  --font-nadpis: "<Font>", Georgia, serif;
  --font-text: "<Font>", -apple-system, "Segoe UI", sans-serif;
  --text-zaklad: 17px;            /* na webu nikdy pod 16 px */
  --text-radek: 1.65;

  /* --- Rozestupy (stupnice, ne náhodná čísla) --- */
  --mezera-1: 4px;   --mezera-2: 8px;   --mezera-3: 16px;  --mezera-4: 24px;
  --mezera-5: 32px;  --mezera-6: 48px;  --mezera-7: 64px;  --mezera-8: 96px;

  /* --- Tvar --- */
  --zaobleni-karta: 16px;
  --zaobleni-tlacitko: 999px;
  --stin-karta: 0 2px 20px rgba(0,0,0,0.06);

  /* --- Šířky --- */
  --sirka-obsah: 1140px;
  --sirka-text: 680px;            /* text nikdy přes celou šířku, nečte se to */
}
```

**Pravidlo:** v `ukazka.html` ani v žádné stránce webu se nesmí objevit `#hex` barva natvrdo.
Vždycky `var(--barva-…)`.

---

## Soubor 2: `ukazka.html` — závazný seznam prvků

Tohle je **minimum**. Když některý prvek značka nepoužívá, vynech ho a napiš proč.

### Nad ohybem (co je vidět bez scrollování)
1. **Navigace** — logo, odkazy, tlačítko vpravo. Verze pro mobil (hamburger).
2. **Hero sekce** — hlavní nadpis, podnadpis, primární tlačítko, případně obrázek nebo video.
   *(Tady se nejčastěji pozná, že je reálný nadpis delší, než se čekalo.)*

### Tělo stránky
3. **Sekce s obrázkem vlevo / textem vpravo** — a hned pod ní obrácená varianta.
4. **Trojice karet** (výhody, moduly, kroky) — ikona nebo číslo, nadpis, text.
5. **Sekce s citátem** nebo výrazným tvrzením přes celou šířku.
6. **Reference** — jedna psaná s fotkou, jedna bez fotky. Když jsou video reference, i ta.
7. **Ceník nebo nabídka** — dvě až tři úrovně, jedna zvýrazněná jako doporučená.
8. **Časté otázky** — rozbalovací, aspoň tři.
9. **Formulář** — pole na jméno a e-mail, tlačítko, drobný text o soukromí.
   Ukaž i **stav chyby** (červené pole s hláškou).
10. **Závěrečná výzva k akci** — na tmavém nebo akcentním pozadí.
11. **Patička** — odkazy, kontakt, sociální sítě, drobný text.

### Prvky, které se snadno zapomenou (a pak chybí)
12. **Tmavá sekce** uprostřed světlé stránky (nebo naopak) — jestli barvy fungují i obráceně.
13. **Dlouhý běžný text** — tři odstavce za sebou, s tučným, kurzívou, odkazem a odrážkami.
14. **Tabulka** (i jednoduchá) — často vypadá úplně mimo styl.
15. **Obrázek na celou šířku** a **obrázek v textu**.
16. **Drobný text** — poznámka pod čarou, popisek obrázku.

### Texty
**Nikdy Lorem Ipsum.** Vezmi skutečné produkty, nadpisy a reference z firemního mozku.
U nového klienta si nech poslat tři věty a zbytek dopiš v jeho tématu — a **označ, že je to zástupné**.

---

## Soubor 3: `prvky.html` — přehled

Jedna stránka, rozdělená na sekce. U **každého prvku**:

- **jak vypadá** (vykreslený, ne popsaný),
- **všechny stavy** — u tlačítka: běžný, přejetí myší, zmáčknutý, neaktivní; u pole: prázdné,
  vyplněné, chyba, neaktivní,
- **kdy ji použít** (jedna věta),
- **čeho se vyvarovat** (jedna věta).

Doporučené pořadí sekcí: **Barvy** (vzorník s hexy a s ukázkou textu na každé) · **Písmo**
(nadpisy H1 až H4 a běžný text ve skutečné velikosti) · **Rozestupy** (vizuální stupnice) ·
**Tlačítka** · **Formulářové prvky** · **Karty** · **Sekce** · **Drobnosti** (oddělovače, odznaky,
popisky).

---

## Kde soubory bydlí

```
<brandová složka projektu>/
├── tokens.css
├── ukazka.html
├── prvky.html
└── components/          ← nepovinné: jednotlivé komponenty jako samostatné soubory
```

**Ostrý web si `tokens.css` nekopíruje** — odkazuje na jeho nasazenou kopii, nebo se soubor
při nasazení kopíruje jako celek. Nikdy se nepřepisuje ručně do stránky.

---

## Na co pozor

- ❌ Postavit jen `prvky.html` → ✅ **bez celé stránky se nepozná, jestli to funguje**
- ❌ Vyplnit stránku Lorem Ipsum → ✅ reálné texty odhalí, co se nevejde
- ❌ Barva natvrdo „jen na téhle jedné stránce“ → ✅ i výjimka jde přes proměnnou
- ❌ Zapomenout na stav chyby a přejetí myší → ✅ prvek bez stavů se pak dodělává narychlo a jinak
- ❌ Ukázat jen desktop → ✅ vždycky i mobilní šířka

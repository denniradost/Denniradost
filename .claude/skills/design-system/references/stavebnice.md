# Stavebnice projektu — návod, podle kterého se staví další stránky

> **K čemu to je:** aby stránka postavená za měsíc, jinou session nebo na jiném počítači
> vypadala jako zbytek webu. Ne „podobně“ — **stejně**.
>
> **Proč to musí existovat:** design systém říká, jaké má značka barvy a písmo. Neříká,
> **jak se na tomhle konkrétním webu jmenuje úvodní sekce a co v ní musí být.** Bez toho
> si to každá nová session vymyslí znovu — a vymyšlená úvodní sekce bez správného pozadí
> je přesně ten rozdíl mezi „skoro to sedí“ a „je to ono“.
>
> Vzniklo z reálného selhání 2026-08-15: na jednom počítači vznikaly krásné stránky,
> na druhém tentýž agent zapomínal na úvodní sekci s pozadím a zakládal další soubory
> se styly. Design systém přitom byl stejný. Chyběl tenhle dokument.

---

## Kdy stavebnici vytvořit

**Vždycky, když v projektu vznikne druhá stránka.** První stránka je návrh; druhá už je
systém a od ní se to začíná rozjíždět.

Vytvoří ji `design-system` (spolu se vzorovou stránkou a přehledem prvků) nebo `web-setup`
při zakládání webu. Doplňuje ji každý, kdo přidá novou opakovatelnou komponentu.

---

## Kam ji uložit a jak na ni ukázat

1. **Soubor** ulož do složky projektu jako `STAVEBNICE-<projekt>.md`
   (nebo `STAVEBNICE-WEBU.md`, když je projekt jeden).
2. 🔴 **Zapiš na ni odkaz do `CLAUDE.md`** — do části se závaznými pravidly, jednou větou:
   *„Stavím nebo předělávám stránku v projektu X → NEJDŘÍV přečti `cesta/STAVEBNICE-X.md`.“*
3. **Zapiš odkaz i do hlavičky sdíleného souboru se styly** — komentářem nahoře.
   Kdo otevře styly, přečte si ho dřív, než začne psát.

> **Pravidlo, které stojí za celým tímhle dokumentem:**
> **návod, na který nevede odkaz z `CLAUDE.md`, prakticky neexistuje.**
> Může být napsaný výborně a rok se k němu nikdo nedostane. Nová session nezná
> historii projektu — zná jen to, co jí `CLAUDE.md` řekne, aby si přečetla.

---

## Co v ní musí být (a proč zrovna tohle)

Sedm částí. Každá řeší jednu chybu, která se bez ní opakuje.

### 1. Pravidla, která se neporušují
Tři až pět vět. Nejdůležitější je vždycky: **jeden soubor se styly, nezakládat další.**
Plus: barvy a rozměry přes proměnné, ne natvrdo. Plus výjimky, pokud nějaké jsou —
a u výjimky napsat, **proč** existuje, jinak ji někdo „uklidí“.

### 2. Kostra stránky k okopírování
Celá hlavička dokumentu včetně titulku, popisku, sdílecího obrázku a odkazu na styly.
Ne popis — **hotový kus kódu**, ze kterého se začíná.

### 3. Jak se vkládá menu a patička
Když projekt používá sestavovač nebo šablony, patří sem tabulka značek a co která vloží.
Ať nikdo nekopíruje menu ručně — to je nejrychlejší cesta k webu, kde má každá stránka
jiné menu.

### 4. Úvodní sekce (hero) — všechny varianty, celé
**Tohle je část, kvůli které stavebnice vzniká.** Úvodní sekce bývá nejsložitější prvek
webu: vrstvy pozadí, přechody, animace, výjimky pro mobil. Když se popíše slovy, nikdo
ji nezopakuje. **Musí tu být celý kód každé varianty** a u ní jedna věta, kdy se používá.

### 5. Prvky obsahu
Sekce, sloupec textu, tlačítka, karty, reference, boxy. U každého název třídy a kdy ji
použít. Stačí tabulka plus dva tři delší příklady.

### 6. Barvy a písmo jako tabulka proměnných
Název proměnné, hodnota, k čemu je. Aby nikdo nepsal `#d6ab2b`, když existuje
`var(--dm-gold)`.

### 7. Postup nasazení a checklist před odevzdáním
Přesné příkazy v pořadí, v jakém se spouštějí, i s pastmi („tenhle skript nahrává celou
složku, takže…“). A na konec seznam otázek, které si autor projde, než řekne „hotovo“.

---

## Čemu se v stavebnici vyhnout

- **Principům.** „Drž jednotný vzhled“ nikoho nikam neposune. Do stavebnice patří jména
  a kód. Principy jsou ve standardech.
- **Zastaralým jménům.** Když se komponenta přejmenuje, oprav i stavebnici. Návod, který
  lže, je horší než žádný — pošle člověka po cestě, která nikam nevede.
- **Popisu místo ukázky.** „Hero má tmavé pozadí se září“ → nikdo nezopakuje. Zkopírovaný
  kód → zopakuje každý.

---

## Test, jestli stavebnice funguje

> **Dokázal by podle ní postavit stránku někdo, kdo tenhle projekt v životě neviděl —
> aniž by musel otevřít jedinou existující stránku?**

Když ne, chybí tam ta část, kvůli které by ji musel otevřít. Doplň ji.

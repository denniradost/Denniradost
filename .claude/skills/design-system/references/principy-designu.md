# Designové principy — pro web

> Pomocný materiál pro skill `design-system`. Univerzální principy, které platí pro každý web.

## 1. Whitespace (prázdný prostor) je prvek designu

Prázdné místo **není ztracené místo**. Je to:
- Vizuální oddělovač sekcí
- Prostor, kde oko odpočívá
- Důraz pro klíčové prvky

**Pravidlo:** raději moc bílé než málo. Levné weby vypadají levně proto, že mají všechno nahuštěné.

**Konkrétně:**
- Sekce mezi sebou: 80-120 px na desktopu, 40-60 px na mobilu
- Mezi nadpisem a textem: alespoň 16-24 px
- Padding uvnitř karet: 24-40 px
- Mezi tlačítkem a textem nad ním: 24-32 px

## 2. Vizuální hierarchie

Návštěvník během 3 sekund pozná: *"Co je tu nejdůležitější?"* Dosáhneš toho:

- **Velikostí** — H1 je největší, drobné poznámky nejmenší
- **Kontrastem** — důležité = tmavší / barevné, méně důležité = světlejší
- **Pozicí** — co je nahoře a uprostřed se vidí dřív
- **Prostorem kolem** — izolovaný prvek přitahuje pozornost
- **Barvou** — accent barva přitahuje oko (proto ji používáš jen na CTA)

**Test:** přimhuř oči nebo se podívej na web rozmazaně. Vidíš jasně, co je hlavní?

## 3. F-pattern a Z-pattern (jak lidi čtou web)

**F-pattern** — pro stránky s textem (blogy, články):
- Oči jdou shora dolů, ale **horní část čtou nejvíc**
- První 2 řádky čtou skoro celé
- Pak skenují vlevo (důležité info patří doleva)

**Z-pattern** — pro stránky s méně textem (landing pages):
- Logo vlevo nahoře → headline / CTA vpravo nahoře
- Diagonálně dolů ke středu
- CTA vpravo dole

**Praktický důsledek:**
- Logo a hlavní CTA tam, kam se oko dívá
- Důležitý text v levé třetině
- Neztratit klíčovou informaci v pravém spodním rohu

## 4. Mobile-first

Víc než **60-80 % návštěv** je z mobilu (záleží na oboru). Pravidla:

- **Body text minimálně 16 px** na mobilu (jinak iOS přibližuje)
- **Tlačítka minimálně 44x44 px** (palec musí mít kam kliknout)
- **Klíčové info nad linií skroulu** — co je vidět hned po načtení (na mobilu je to méně než si myslíš)
- **Žádný horizontální scroll** — všechno se vejde na šířku
- **Obrázky komprimuj** — mobil má často slabší internet
- **Test na skutečném telefonu**, ne jen v devtools

## 5. CTA — výzvy k akci

Každá stránka má **jednu hlavní akci**, kterou má návštěvník udělat. CTA = tlačítko/odkaz, který ho tam dovede.

**Pravidla:**
- **Jedna primární CTA** na sekci (více = paralýza výběru)
- **Akcentní barva** s vysokým kontrastem
- **Slovesný text v 1. osobě** — *"Chci začít"*, *"Stáhnu si ukázku"* (lepší než *"Začít"* / *"Stáhnout"*, protože návštěvník mluví o sobě, ne ty mu rozkazuješ)
- **Velké, snadno kliknutelné** — minimum 44 px výška
- **Opakuj** — na delší stránce stejné CTA více než jednou (lidi nečtou celé)

**Anti-příklad:**
> *"Klikněte zde pro více informací"* ❌ (vágní, nikdo nechce "více informací")

**Lepší:**
> *"Chci se podívat na program"* ✅ (jasný výsledek)

## 6. Konzistence

**Stejné věci vypadají stejně.** Když má jedno tlačítko zaoblení 8 px, všechna tlačítka mají 8 px.

Kontroluj:
- Tlačítka — barva, velikost, zaoblení, padding
- Karty — stín, padding, zaoblení
- Spacing — mezery mezi sekcemi
- Fonty — H1 vždy stejný, body vždy stejný
- Ikony — jedna sada (Heroicons / Phosphor / Feather), ne mix

Tady přesně pomáhá `design-system.md` — jeden zdroj pravdy.

## 7. Loading speed (rychlost)

Web musí načíst do **2-3 sekund**, jinak 50 % návštěvníků odejde.

**Co web zpomaluje:**
- Obrovské obrázky (často 2-5 MB → měly by být max 200-500 KB)
- Příliš mnoho fontů a vah
- Externí skripty (chat widgety, trackery)
- Auto-přehrávané video v hero sekci

**Co s tím:**
- Komprese obrázků (https://tinypng.com nebo https://squoosh.app)
- Formát `.webp` místo `.jpg` / `.png` (50 % menší velikost)
- Jen 1-2 fonty z Google Fonts
- Lazy loading obrázků (`loading="lazy"`)

## 8. Accessibility (přístupnost)

Web musí fungovat i pro:
- Slabozraké (kontrast)
- Slepé (screen reader → potřebuje `alt` u obrázků, sémantické HTML)
- Lidi s dyslexií (jasné fonty, dobré řádkování)
- Klávesnicové uživatele (focus stav na tlačítkách)

**Minimum:**
- Kontrast textu / pozadí ≥ 4.5:1 (https://webaim.org/resources/contrastchecker/)
- Každý obrázek má `alt` atribut
- Tlačítka jsou opravdu `<button>`, ne `<div onclick>`
- Při tabování je vidět, kde je focus (border, outline)
- Vyvarovat se barvy jako jediného nositele informace (colorblind)

## 9. Méně je víc

Když si nejsi jistý, **odeber, ne přidej**.

Časté zlepšení = odstranit:
- Nepotřebnou sekci
- Extra tlačítko vedle hlavní CTA
- Druhý font
- Třetí barvu
- Ozdobné prvky, které neslouží sdělení

**Test:** projdi web a u každého prvku se zeptej *"K čemu to tady je? Co se stane, když to odstraním?"* Pokud odpověď je *"vlastně nic"*, smaž.

## 10. Test ze 3 metrů

Postav se 3 metry od obrazovky (nebo si dej zoom na 50 %). Ze tří metrů musíš pořád:
- Poznat, o čem stránka je (1-2 slova)
- Najít hlavní CTA (kde mám kliknout?)
- Vidět hierarchii (co je nahoře, co dole)

Pokud ne → hierarchii a kontrast je potřeba zesílit.

## Nástroje pro inspiraci a kontrolu

- **Land-book** (https://land-book.com) — galerie krásných landing pages
- **Mobbin** (https://mobbin.com) — UI inspirace z reálných aplikací
- **Awwwards** (https://www.awwwards.com) — oceněné weby (pozor, často přes-designed)
- **Coolors** (https://coolors.co) — palety
- **WebAIM Contrast Checker** (https://webaim.org/resources/contrastchecker/) — kontrola kontrastu
- **TinyPNG** (https://tinypng.com) — komprese obrázků
- **PageSpeed Insights** (https://pagespeed.web.dev) — Google rychlostní test

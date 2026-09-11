# Standardy — rozcestník

> **Standard = pravidla, která platí napříč skilly.** Skill říká, JAK se něco dělá. Standard říká,
> CO musí platit vždycky, ať to dělá kterýkoli skill.
>
> **Skilly standardy neopisují, odkazují sem.** Když se pravidlo změní, mění se na jednom místě
> a platí okamžitě všude, i pro skilly, které ještě nevznikly.
>
> Vzniklo: 2026-08-06 · Naposledy změněno: 2026-08-15

---

## Co si přečíst kdy

| Chystám se… | Standard |
|---|---|
| tvořit **cokoli, co míří k člověku** — text, stránku, e-mail, reklamu, scénář videa či webináře | **`sdeleni.md`** (čte se PŘED tvorbou) |
| dělat **cokoli vizuálního** — stránku, web, e-mail, grafiku, příspěvek, prezentaci | **`vizual.md`** |
| stavět nebo měnit **webovou stránku** (i tu nejjednodušší) | **`vizual.md` + `webova-stranka.md`** |
| dělat stránku, na které je **souvislý text** (prodejní, vstupní, návod, článek, právní) | **+ `ctivost.md`** |
| dělat **příspěvek na sítě** | `vizual.md` *(+ `prispevky.md`, až vznikne)* |
| chystat **e-mail do rozesílky** | `vizual.md` *(+ `email.md`, až vznikne)* |

**Pravidlo:** u všeho, co míří k člověku, platí `sdeleni.md` (myšlení) a u všeho, co se dívá, `vizual.md` (vzhled). K němu se přidá standard toho kanálu, ve kterém pracuješ.

---

## Co v nich je

### `sdeleni.md` — jak přemýšlet, než se cokoli vytvoří pro lidi
Pět otázek před první větou: komu to je a jeho doslovná slova · co mu to nabízí (každé sdělení
je nabídka, jedna silná myšlenka) · kam ho to vede (jedna akce) · čí hlas mluví · poctivost nad
konverzí. Plus konzistence slibu napříč celou cestou a rozcestník do hloubky (nabídka, prodejní
text, výzva k akci, průzkum trhu).

### `vizual.md` — platí pro všechno, co se dívá
Vzhled se bere, ne vymýšlí · **jedno CSS na celý web** (ne jedno na sekci) · **otisk verze proti staré keši** · **vizuální smyčka** (otevřít,
screenshot, posoudit, opravit, zkontrolovat mobil) · reálné texty místo Lorem Ipsum ·
jeden projekt = jeden design systém.

### `ctivost.md` — aby se dlouhý text dal číst
**Sloupec textu max 700 px** · **jedna velikost (18 px) a jedna barva** běžného textu, rozdíl dělá
tučnost · **dlouhý text se seká záchytnými body** (zvýrazňovací a orámované boxy, mezinadpisy, karty,
obrázek přes celou šířku) · **zvýraznění nikdy nesmí vypadat jako tlačítko** · stejné mezery
vodorovně i svisle · zrcadlené bloky drží poměry · **lichá karta nezůstane sama v rohu** ·
**efekt z jedné sekce se nepropisuje všude** (dostane vlastní jméno) · **uvozovky české na obou
koncích** („takhle“), v kódu rovné · **na mobilu se pilulky nesypou a ozdoby nemizí,
jen se otáčejí** · na prodejní stránce **nejdřív šipka dolů, tlačítko až po argumentu**.

*Vzniklo z ladění prodejní stránky, ale platí pro celý web — návody a právní stránky se čtou stejným okem.*

### `webova-stranka.md` — technické minimum každé stránky
Co má stránka mít, i když vypadá skvěle: **titulek a popisek** · **sdílecí obrázek** (jak odkaz vypadá
na Facebooku a ve WhatsAppu) · **jeden H1 a hierarchie nadpisů** · čitelná adresa · **měřicí kódy**
(analytika, Meta Pixel) a souhlas k nim · rychlost · **přístupnost** · formulář, který někam teče ·
404 a funkční odkazy · **hlavička a patička ze sestavovače**, ne kopie v každé stránce.

*Tenhle standard není designový.* Stránka může být krásná a přitom se sdílet bez obrázku, neměřit
a být nepřístupná.

---

## Chystané standardy

| Soubor | Co bude řešit | Kdy |
|---|---|---|
| `prispevky.md` | příspěvky na sítě: formáty, bezpečné okraje, titulek v obrázku, první řádek, alt text | až se k sítím dostaneme |
| `email.md` | rozesílka: šířka, tabulky, inline styly, tmavý režim, limit velikosti, preheader, odhlášení | až se k e-mailingu dostaneme |

Přidat další standard je levné: nový soubor + řádek v téhle tabulce. **Skilly se kvůli tomu nemění.**

---

## Jak se standardy předávají dál

Standardy jdou ven jako **jeden malý balíček „Standardy“**, ne rozsypané po skillech. Kdo si ho
stáhne jednou, zlepší tím **všechny** skilly, které už má.

Do balíčku patří tenhle rozcestník, jednotlivé standardy a **jeden řádek do hlavního souboru
s pravidly příjemce** (u nás `CLAUDE.md`), aby na ně jeho agent narazil sám:

> *Stavíš nebo měníš cokoli vizuálního (stránka, web, e-mail, grafika) → **nejdřív standardy**
> (`standardy/ROZCESTNIK.md`), pak teprve konkrétní skill.*

**Skill musí fungovat i bez standardů.** Kdo si stáhne jen jeden stavěcí skill, dostane funkční práci —
skill jen řekne, že bez standardů si část pravidel domýšlí, a nabídne je doplnit.

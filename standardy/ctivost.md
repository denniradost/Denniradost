# Standard: čtivost dlouhého textu

> **Platí pro každou stránku, na které je souvislý text** — prodejní stránku, vstupní stránku,
> návod, právní stránku, článek, děkovačku. Nejen pro prodejky.
>
> **Kdy číst:** vždycky, když stavíš stránku s víc než dvěma odstavci.
> Vzniklo: 2026-08-12 (z reálného ladění prodejní stránky) · Rozcestník: `ROZCESTNIK.md`

---

## Proč tenhle standard vznikl

Stránka může mít správné barvy, správný font a přesto se nedá číst. Text přes celou šířku,
deset odstavců za sebou bez jediného záchytného bodu, tři různé velikosti písma v jedné sekci.
**Návštěvník nečte, projíždí** — a když oko nemá kde zastavit, sjede pryč.

Tohle jsou pravidla, která to řeší. Jsou z reálného ladění, ne z teorie.

---

## 1. Sloupec textu má šířku, ne šířku obrazovky

**Čtený text: maximálně 700 px.** Ne šířku sekce, ne 1180 px, ne „co zbylo“.

Na širokém řádku oko při návratu na začátek dalšího řádku občas mine a chytne se o řádek vedle.
Čtení se tím dře, i když si toho čtenář nevšimne. **700 px dá zhruba 65–70 znaků na řádek** —
to je hodnota, na které se shodne kdekterá typografická příručka.

Širší smí být jen to, co se nečte po řádcích: **mřížky karet, galerie, fotopásy, tabulky.**
Ty naopak mají ze sloupce vystoupit, ať jsou na počítači vidět.

> **Test:** *„Kolik znaků má nejdelší řádek?“* Přes 80 → zúžit.

---

## 2. Jedna velikost písma na běžný text

**18 px pro veškerý čtený text na stránce.** V kartách, v boxech, v citacích, v odpovědích
na otázky, v referencích. Malé zůstávají jen popisky, štítky a pojistky pod tlačítky.

Tři velikosti v jedné sekci vypadají jako nedodělek, i když každá z nich je sama o sobě rozumná.
Na mobilu nikdy pod 17 px.

---

## 3. Jedna barva písma, rozdíl dělá tučnost

Na tmavém pozadí **nepoužívej čistě bílou pro běžný text** — „tahá oči“. A nemíchej dvě barvy
(tlumenou pro text, bílou pro tučné): stránka pak vypadá roztřepeně.

**Jedna barva pro všechen čtený text, zvýraznění dělá jen tučný řez.** Bílá zůstává nadpisům.

*U Digitálního Mága: `--txt-prodej` (#B7BDD8) pro text, bílá jen nadpisy.*

---

## 4. Dlouhý text se rozseká záchytnými body

Po každých zhruba **třech až čtyřech odstavcích** má přijít něco, o co oko zavadí. Ne dekorace —
záchytný bod, který nese obsah:

| Prvek | K čemu |
|---|---|
| **Zvýrazňovací box** (barevný nádech + silná linka vlevo) | jedna věta, na které stojí celá pasáž |
| **Orámovaný box** | krátký výčet, dva důvody, checklist |
| **Mezinadpis** | nový úsek myšlenky |
| **Karta s ikonou** | seznam, který se dá rozsekat na body |
| **Obrázek přes celou šířku** | předěl mezi dvěma velkými částmi |
| **Citace / bublina** | slova někoho jiného |
| **Zvýraznění uvnitř věty** | to nejdůležitější v odstavci |

**Boxy musí mít jasnou hierarchii, ne náhodné barvy.** U nás: plná barva = tlačítko,
barevný nádech = zvýraznění, sklo = obsahová karta. **Zvýraznění nikdy nesmí vypadat jako tlačítko** —
člověk na něj klikne a nic se nestane.

---

## 4b. Fotky a předěly se plánují před psaním

- **Každé 2 až 3 sekce předěl:** fotka přes celou šířku, mockup nebo jiný obrazový prvek. Dva čistě textové
  bloky za sebou se nesmí potkat. Plán „sekce → typ bloku → fotka“ vzniká PŘED první větou textu.
- **Fotky se vyžádají v zadání, ne u designu.** Návrh bez fotek je kostra, ne stránka; chybějící fotky
  se pojmenují jako díra.
- **Fotka přes celou šířku** má přechod nahoře i dole do barvy sousedních sekcí, na širokém monitoru vyšší
  výšku (min 520 px, na 1920 px až 800 px) a ořez podle obličeje. Popisek v pilulce; na mobilu pod fotkou.
- **Ukázky produktu vždy jako realistické zařízení s reálným screenem.** Nikdy kreslený obdélník,
  nikdy roztažený screenshot přes celou šířku. (Postup: skill `sales-page`, `references/mockupy.md`.)
- **Stejný typ karet se neopakuje dvakrát za sebou.** Po kartách s ikonou přijde časová osa, dvě cesty,
  citáty, skládačka, ne další karty s ikonou. (Přidáno 2026-09-05 z ladění AI Magic.)

## 5. Prvky drží stejný rytmus

- **Mezery mezi kartami stejné vodorovně i svisle.** (Pozor na roztahování do stran — mezera
  pak vzniká sama a je jiná, než jakou jsi nastavil.)
- **Zrcadlené rozvržení drží poměry.** Obrázek vlevo a obrázek vpravo mají mít stejnou šířku —
  jinak se při prohození pořadí obrázek roztáhne do širšího sloupce.
- **Obrázky v kartách zarovnané k hornímu okraji**, ne na střed. Delší text jinak obrázek „utopí“.
- **Kulaté prvky bez čtvercového rámu.** Obrázek s průhledným pozadím nemá dostat okraj.

---

## 6. Co se kontroluje na mobilu (a na počítači se to nepozná)

- **Pilulky a štítky se nesypou do sloupečků.** Pružné řádky s mezerami se na úzkém displeji lámou;
  běžný textový tok ne. Částky a čísla drž na jednom řádku.
- **Ozdoby, které mají smysl, nezahazuj — otoč je.** Šipka u fotky nemá zmizet, má se stočit.
- **Text se nezužuje do provázku.** Fotka vedle textu → na mobilu fotka nad text.
- **Skupiny karet se skládají do jednoho sloupce**, včetně zrcadlených variant.

---

## 7. Prodejní stránka: kde smí být tlačítko

Prodejní stránka nejdřív vypráví, teprve pak prodává:

- **V úvodu není prodejní tlačítko.** Patří tam šipka dolů — pozvání ke čtení.
- **Tlačítko přichází až po argumentu**, ne uprostřed budování důvěry.
- **Jedna nabídka = jedna sada tlačítek.** Když stránka umí dva režimy (zavřeno / prodej),
  nesmí být na stránce obojí naráz.
- **Všechno kolem ceny bydlí na jednom místě** a je označené, ať se to dá schovat nebo
  personalizovat jedním zásahem.

---

## 8. Okraje bloku musí být stejné ze všech stran

Poslední odstavec uvnitř karty nebo bubliny si nese vlastní spodní mezeru. Sečte se s vnitřním
okrajem bloku a **spodek je najednou vyšší než vršek a boky.** Poslednímu prvku uvnitř bloku
spodní mezeru vynuluj.

---

## 9. Efekt z jedné sekce se propíše všude

Uděláš hezký nápad pro jednu sekci (třeba **střídavé posunutí karet jako časová osa**)
a zapíšeš ho na obecnou třídu. Za týden se diví, proč jinde v mřížce zejí díry a proč pod ní
zmizela mezera. Nikdo to nespojí s tou původní sekcí.

**Efekt, který platí jen pro jedno místo, dostane vlastní jméno** (modifikátor) a používá se
jen tam. Obecná třída zůstane obecná.

> **Test:** *„Kolik míst na webu tohle pravidlo ovlivní?“* Když víc než jedno a nechceš to,
> je to modifikátor, ne obecné pravidlo.

---

## 10. Lichá karta nezůstane sama v rohu

Tři karty ve dvou sloupcích. Dvě sedí vedle sebe, třetí visí vlevo a vedle ní je díra.
Vypadá to jako nedodělek, i když je to jen matematika.

**Poslední karta liché skupiny se roztáhne přes celou šířku mřížky a vycentruje** (v původní
šířce, ať nezhrubne). Platí pro všechny mřížky karet, ne jen pro tu, kde sis toho všiml.

---

## 11. Obecné pravidlo umí přebít centrování

Nadpis je uprostřed a odstavec pod ním utíká doleva, i když má v CSS „margin: auto“.
Skoro vždycky je příčina stejná: **obecnější pravidlo pro odstavce uvnitř obsahu má vyšší
váhu** (`.obsah p` je silnější než `.perex`) a přepíše okraje.

Když se prvek nechová podle svého vlastního pravidla, hledej, **co ho přebíjí**. Nepřidávej
další výjimku naslepo a nesahej po „!important“.

> **Test:** *„Sedí střed odstavce přesně pod středem nadpisu?“* Když ne, přebíjí to něco jiného.

---

## 12. Uvozovky: hlídej i tu zavírací

V češtině se píše **„takhle“**: otevírací dole, zavírací nahoře. Nejčastější tichá chyba je,
že se opraví jen ta první a zavírací zůstane rovná (`"`). V odstavci to pak bliká a vypadá to
jako nedbalost, které si autor nevšimne, protože „uvozovky tam přece jsou“.

**V kódu, JSON, cestách a příkazech naopak vždycky rovné ASCII uvozovky** — jinak to spadne.

> **Test:** vyhledej v hotové stránce `„` a projdi, čím je každá dvojice zavřená.

---

## Checklist před odevzdáním

1. Je čtený text max 700 px široký?
2. Má veškerý běžný text stejnou velikost (18 px) a stejnou barvu?
3. Není nikde čistě bílý běžný text na tmavém?
4. Přijde záchytný bod aspoň po každých třech odstavcích?
5. Nevypadá žádné zvýraznění jako tlačítko?
6. Jsou mezery mezi kartami stejné vodorovně i svisle?
7. Drží zrcadlené bloky stejné poměry?
8. Nesypou se pilulky na mobilu do sloupečků?
9. Zůstaly ozdoby (šipky, ocásky) i na mobilu?
10. Má karta i bublina stejný okraj nahoře, dole i po stranách?
11. Vede první tlačítko na stránce k dalšímu čtení, ne rovnou k prodeji?
12. Nezůstala lichá karta sama v rohu?
13. Neovlivnilo pravidlo z jedné sekce i všechny ostatní?
14. Sedí střed odstavce pod středem nadpisu?
15. Jsou uvozovky české **na obou koncích** („takhle“) a v kódu rovné?

---

## Kdo tenhle standard používá

`sales-page` · `vstupni-stranka` · `dekovaci-stranka` · `design-system` · `prodejni-text` ·
budoucí skilly na články a návody. **Čte se spolu s `vizual.md`**, nenahrazuje ho.

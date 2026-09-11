# Standard: vizuální práce

> **Platí pro všechno, co se dívá** — webovou stránku, e-mail, příspěvek na sítě, prezentaci, PDF,
> grafiku. Ne jen pro web.
>
> **Kdy číst:** vždycky, než začneš stavět nebo měnit něco vizuálního.
> Vzniklo: 2026-08-06 · Naposledy změněno: 2026-08-06 · Rozcestník: `ROZCESTNIK.md`

---

## 1. Vzhled se nevymýšlí, bere se

Než začneš, **najdi uložený vzhled** v tomhle pořadí:

1. **`tokens.css` a hotové komponenty** v brandové složce projektu (u nás `knowledge/brand/<projekt>/`)
   — živé soubory mají přednost před popisem
2. **destilát design systému ve firemním mozku** (ve firemním mozku)
3. `design-system.md` v kořeni projektu

> 🔴 **Když je design systém rozdělený na části, čti VŽDY základ PLUS soubor kanálu.**
> U nás: `pravda/design/zaklad.md` (barvy, font, tvar, fotostyl, tón — platí všude) **a k tomu**
> `web.md`, `email.md` nebo `socialni-site.md` podle toho, co zrovna děláš. Základ sám nestačí
> (nemá konkrétní velikosti ani komponenty) a kanál sám taky ne (nemá barvy ani charakter).

**Nic z toho neexistuje** → spusť skill `design-system`, ať vzhled vznikne jednou a pak drží.
**Nový vzhled vymýšlej jen na výslovné přání** — a co vznikne, zapiš zpátky.

⚠️ Nejčastější chyba není chybějící design systém, ale **design systém, o kterém se zapomnělo.**
Podívej se, co v projektu leží, dřív než začneš tvořit.

---

## 2. Jedno CSS na celý web, ne jedno na stránku

**Celý web má jeden stylový soubor. Ne jeden na sekci, ne jeden na typ stránky. Jeden.**

Stránka nemá vlastní `<style>` blok a nenačítá si vlastní styl „jen pro sebe“.

> **Test, který se dá spočítat:** *„Kolik stylových souborů načítá každá stránka?“*
> Musí to být **jedna, na každé stránce webu**. Když jich je víc nebo se počet mezi stránkami liší,
> web se už větví, jen to ještě není vidět.

> **Druhý test:** *„Když teď změním hlavní barvu na jednom místě, přebarví se všechny stránky?“*
> Musí být ano. Když ne, není to web, ale sbírka kopií, které se rozejdou.

### Pozor na dvě pasti, do kterých se padá i s dobrým úmyslem

**Past první: „tohle je přece jen pro tuhle sekci.“** Vznikne styl pro právní stránky, pak pro návody,
pak pro objednávku. Každý z nich je sám o sobě rozumný. Dohromady je z webu pět různých webů a nikdo
už neví, co kde platí. Když sekce potřebuje vlastní prvky, přidají se **do společného souboru** jako
další oddíl, ne do nového souboru.

**Past druhá: kopie stylu v hlavičce stránky.** Šablona stránky si nese `<style>` blok. Založí se
z ní dvacet stránek a každá má vlastní kopii. Když se pak společný styl opraví, těch dvacet kopií
ho přebije a oprava se neprojeví. Vypadá to, jako by změna nefungovala. **Přišel jsi na to,
až když se web tváří, že tvoji opravu ignoruje.**

### Prohlížeč drží starý styl

Když se stylový soubor změní, jeho adresa zůstane stejná a prohlížeč klidně ještě hodiny servíruje
starou verzi. Stránka pak vypadá rozbitě: obrázky bez rozměrů, ikony přes celou šířku. **Není to
chyba v CSS, je to keš.**

Řešení: k adrese stylu se připojí otisk obsahu, `styl.css?v=a1b2c3d4`. Změní se soubor, změní se
adresa, prohlížeč si musí stáhnout nový. Nezmění se nic, keš dál platí. **Dělá se to při nasazování,
automaticky** — ne ručně, protože na ruční krok se zapomene.

Výjimka: **e-mail**. Tam se styly musí psát přímo k prvkům (jinak je poštovní klienti zahodí) —
ale hodnoty se pořád berou z design systému, jen se zapisují jinak.

Jak to změřit a jak posbírat rozsypaný web zpátky:
příloha `kontrola-jednoho-css.md` ve skillu Design systém (máš-li ho)

---

## 3. Vizuální smyčka — podívej se na to, co jsi postavil

**Bez tohohle kroku se nic vizuálního nesmí ohlásit jako hotové.**

1. **Otevři** v prohlížeči (`preview_start`, nebo skill `agentni-prohlizec`).
2. **Screenshot.** Podívej se na obrázek, ne na kód.
3. **Projeď osm otázek:** Dýchá to? · Vidím hierarchii? · Vyskočí tlačítko? · Nejsou řádky delší
   než zhruba 70 znaků? · Drží zarovnání? · Je kontrast čitelný (4,5 : 1)? · Nejsou tam osamělá slova
   na řádku? · Sedí obrázky?
4. **Oprav a podívej se znovu.** Klidně třikrát.
5. **Zkontroluj mobil** (šířka 375 px, znovu screenshot): nepřetéká to do stran, nadpis není na pět
   řádků, tlačítko se dá zmáčknout prstem, text není pod 16 px.
6. **Do zprávy přilož obrázek, ne popis.** „Postavil jsem to podle design systému“ není důkaz.

U **e-mailu** se smyčka dělá na náhledu (a ideálně i v tmavém režimu). U **příspěvku na sítě**
na skutečném formátu, ne na výřezu.

Detail (co je vidět jen na screenshotu, typické chyby):
příloha `vizualni-smycka.md` ve skillu Design systém (máš-li ho)

---

## 4. Reálné texty, nikdy Lorem Ipsum

Do ukázek a vzorových stránek patří **skutečné texty** — jeho produkty, nadpisy, reference (ve firemním
mozku). Na latinské výplni vypadá dobře každý návrh; teprve reálný nadpis ukáže, že je o pět slov delší,
než se do sekce vejde.

U nového klienta: nech si poslat **tři věty** a zbytek dopiš v jeho tématu, **označené jako zástupné**.

---

## 5. Jeden projekt = jeden design systém

Značka může mít víc projektů a každý může vypadat jinak. **Vždycky se ptej, pro který projekt vzhled
vzniká**, a nepřepisuj ten druhý.

---

## 6. Stavebnice projektu — a odkaz na ni z CLAUDE.md

Design systém říká, jaké má značka **barvy a písmo**. Neříká, **jak se na tomhle konkrétním
webu jmenuje úvodní sekce a co v ní musí být**. Bez toho si to každá nová session vymyslí
znovu — a vymyšlená úvodní sekce bez správného pozadí je přesně ten rozdíl mezi „skoro to
sedí“ a „je to ono“.

**Každý projekt proto má stavebnici:** jeden soubor s kostrou stránky, hotovým kódem
úvodních sekcí, názvy tříd, tabulkou proměnných a postupem nasazení. Ne principy — **jména
a kód k okopírování.**

🔴 **A hlavně: odkaz na ni patří do `CLAUDE.md`.**

> **Návod, na který nevede odkaz z `CLAUDE.md`, prakticky neexistuje.**
> Může být napsaný výborně a rok se k němu nikdo nedostane. Nová session nezná historii
> projektu — zná jen to, co jí `CLAUDE.md` řekne, aby si přečetla.

Totéž platí pro odkaz v **hlavičce sdíleného souboru se styly**: kdo otevře styly, přečte
si tam „nezakládej další soubor, chybí komponenta? přidej ji sem“ dřív, než začne psát.

*(Pravidlo vzniklo z reálného selhání 2026-08-15: na jednom počítači vznikaly stránky, které
držely vzhled, na druhém tentýž agent zapomínal na úvodní sekci a zakládal další soubory se
styly. Design systém byl přitom stejný. Návod existoval — jen na něj nikde nevedl odkaz.)*

---

## 7. Obrázky: nikdy prázdné plochy

Co platí pro texty (nikdy Lorem Ipsum), platí i pro obrázky. **Návrh nebo stránka
s prázdnými místy místo fotek vypadá nedodělaně**, i když jsou barvy, písmo a rozestupy
úplně správně — a člověk podle toho posuzuje celou práci.

- **Vlastní fotky mají přednost před stockem.** Stock je nouzové řešení, ne výchozí.
- **Když stavíš podle existujícího webu, stáhni z něj obrázky** (logo, portréty, produkty,
  pozadí úvodních sekcí) **do fotobanky** — hned na začátku, ne až nakonec. Obrázky jsou
  vstup do návrhu, ne dekorace na konec.
- **Fotobanka je jedna složka** se srozumitelnými názvy souborů a poznámkou, k čemu se
  který hodí. `IMG_4471.jpg` si za měsíc nikdo nevybere.
- **Nemá-li majitel fotky vůbec:** označené zástupné plochy s popisem, co na to místo
  patří, plus **seznam záběrů k nafocení** — a řekni to nahlas, ať si nemyslí, že takhle
  bude vypadat výsledek.

*(Z reálného případu 2026-08-15: klientce se postavil design podle jejího webu, barvy
a písmo seděly, obrázky chyběly úplně. Bez nich to vypadalo špatně.)*

---

## 8. Co jde ukázat, to nepopisuj slovy

**Když se dá věc vyjádřit obrázkem, tvarem nebo pozicí, nepiš k ní větu.** Text, který
jen popisuje to, co je vedle vidět, čtenáře zdržuje a stránku zahlcuje.

| Místo věty | Ukaž |
|---|---|
| „Cena se bude postupně zvyšovat, teď jsi v první hladině" | linku se třemi zastávkami, na aktuální bublinu „TEĎ" |
| „Běžně to stojí 1 770 Kč, ty zaplatíš 357" | přeškrtnutou cenu vedle té nové |
| „Zdarma dostaneš skilly jen v dnešní verzi, bez aktualizací" | tři stavy v porovnání: fajfka, pomlčka, křížek |
| „V balíčku jsou 3 záznamy a 2 skilly" | obrázek těch záznamů a skillů |
| „Hotovo z 95 %" *(bez proužku)* | proužek průběhu, do kterého se to číslo napíše |

**Zkouška:** zakryj si všechen text kolem prvku. Pozná se z toho, co zbylo, o co jde?
Když ne, prvek nefunguje vizuálně a věta ho jen zachraňuje. Oprav prvek, ne větu.

**Druhá zkouška, opačným směrem:** projdi hotový text a u každé věty se zeptej, jestli
už to samé neříká něco vedle. Když ano, věta jde pryč.

⚠️ **Nejde o to psát míň informací.** Jde o to nepsat dvakrát totéž, jednou obrázkem
a jednou větou. Informace, kterou obrázek neunese (proč, pro koho, co z toho má),
patří pořád do textu.

*(Z reálného ladění děkovací stránky. Cenový žebřík byl původně
tři cedule plus vysvětlující věta „Jsi v prvním sloupci“. Věta byla potřeba jenom proto,
že ten prvek sám nic neukazoval.)*

---

## Kdo tenhle standard používá

`design-system` (vyrábí vzhled) · `sales-page` · `vstupni-stranka` · `dekovaci-stranka` ·
`smartemailing-email` · `psani-emailu` (když vzniká HTML) · budoucí skilly na příspěvky a prezentace.

**Skilly tenhle text neopisují.** Mají jednu větu: *„Než začneš, přečti si standardy.“*

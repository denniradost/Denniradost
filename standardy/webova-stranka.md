# Standard: webová stránka (technické minimum)

> **Tohle není o vzhledu.** Stránka může být krásná a přitom se sdílet bez obrázku, neměřit,
> být nedohledatelná a nepřístupná. Tenhle standard drží to, co **musí mít každá stránka**, kterou
> pustíme ven.
>
> **Kdy číst:** vždycky, když vzniká nebo se mění webová stránka. Spolu s `vizual.md`.
> Vzniklo: 2026-08-06 · Naposledy změněno: 2026-08-06 · Rozcestník: `ROZCESTNIK.md`

---

## 1. Hlava stránky (bez tohohle stránku nepouštěj ven)

```html
<!doctype html>
<html lang="cs">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>Konkrétní titulek stránky | Značka</title>
  <meta name="description" content="Jedna věta o tom, co na stránce je a proč na ni kliknout.">

  <link rel="icon" href="/favicon.ico">
  <link rel="canonical" href="https://adresa.cz/tato-stranka">
</head>
```

| Prvek | Pravidlo | Proč |
|---|---|---|
| `lang="cs"` | vždycky | čtečky pro nevidomé jinak čtou češtinu anglickou výslovností, prohlížeč špatně nabídne překlad |
| `viewport` | vždycky | bez toho se stránka na mobilu zobrazí zmenšená jako na počítači |
| `<title>` | **do zhruba 60 znaků**, konkrétní, na začátku to podstatné | tohle je modrý odkaz ve vyhledávání a název záložky |
| `description` | **do zhruba 155 znaků**, věta pro člověka, ne seznam klíčových slov | text pod odkazem ve vyhledávání; rozhoduje o kliknutí |
| `favicon` | vždycky | bez ní má záložka prázdný list |
| `canonical` | když je stránka dostupná na víc adresách | jinak si vyhledávač myslí, že máš dvě stejné stránky, a obě potopí |

⚠️ **Titulek a popisek se nesmí opakovat napříč stránkami.** Dvanáct stránek se stejným titulkem
je nejčastější chyba webu postaveného kopírováním.

---

## 2. Sdílecí obrázek (jak odkaz vypadá na Facebooku a ve WhatsAppu)

Když někdo pošle odkaz na tvoji stránku, **rozhoduje obrázek, ne text**. Bez něj se ukáže šedý
obdélník nebo náhodný obrázek ze stránky.

```html
<meta property="og:title" content="Titulek pro sdílení">
<meta property="og:description" content="Jedna věta, proč to otevřít.">
<meta property="og:image" content="https://adresa.cz/sdileni.jpg">
<meta property="og:url" content="https://adresa.cz/tato-stranka">
<meta property="og:type" content="website">
<meta name="twitter:card" content="summary_large_image">
```

- **Rozměr 1200 × 630 px**, JPG nebo PNG, do 1 MB.
- **Adresa musí být absolutní** (`https://…`), relativní cesta nefunguje.
- **Text na obrázku drž uprostřed** — okraje se v náhledech ořezávají.
- Když stránka vlastní obrázek nemá, použij **značkový výchozí** (jeden pro celý web).

Kontrola po nasazení: pošli si odkaz sám sobě do zprávy a podívej se, jak vypadá.

---

## 3. Nadpisy: jeden H1, hierarchie bez děr

- **Přesně jeden `<h1>`** na stránku, a je to hlavní nadpis (ten, co člověk vidí nahoře).
- Podsekce jsou `<h2>`, jejich části `<h3>`. **Nepřeskakuj úrovně** (z `h2` rovnou na `h4`).
- **Nadpis se nepoužívá kvůli velikosti písma.** Když potřebuješ velký text, který není nadpis,
  je to odstavec se stylem.
- Nadpisy mají nést smysl i **vytržené ze stránky** — kdo si je přečte za sebou, má rozumět, o čem
  stránka je. *(To je zároveň copywritingové pravidlo ze skillu `prodejni-text`.)*

---

## 4. Adresa stránky

- **Malá písmena, pomlčky, bez diakritiky:** `/kod-bohatstvi`, ne `/Kód_Bohatství1`.
- **Čitelná pro člověka.** Z adresy má být poznat, co na stránce je.
- **Neměň adresu už zveřejněné stránky.** Když musíš, nastav přesměrování ze staré na novou —
  jinak umřou všechny odkazy, které na ni někdo dal.

---

## 5. Měřicí kódy (analytika, Meta Pixel)

- **Jednou, ne dvakrát.** Dvakrát vložený pixel počítá každou návštěvu dvojmo a rozbije čísla
  v reklamě. Než kód přidáš, **zkontroluj, jestli tam už není.**
- **Měřicí kódy patří do sdílené části webu** (hlavička nebo patička, kterou mají všechny stránky),
  ne do každé stránky zvlášť. Jinak na některé chybí a data jsou děravá.
- **Vždycky ověř, jaká čísla to má sbírat** — u prodejní stránky je důležitá událost odeslání
  objednávky, u vstupní stránky odeslání formuláře. Bez toho měříš jen návštěvy a nevíš nic.
- **Když stránka měří, musí mít souhlas** (viz níž).

⚠️ Kódy a identifikátory (pixel ID, měřicí kód) jsou **údaje majitele** — ber je z jeho zdroje,
netipuj a nekopíruj z jiného projektu.

---

## 6. Soukromí a souhlas

- **Měříš nebo máš pixel → potřebuješ cookie lištu** se skutečnou volbou (odmítnout musí být stejně
  snadné jako přijmout) a **měřicí kódy se pouští až po souhlasu.**
- **Formulář sbírá kontakt → potřebuje** větu o tom, co se s údaji stane, a odkaz na zpracování
  osobních údajů. Zaškrtávátko se **nesmí předvyplnit.**
- Odkaz na zásady soukromí patří do patičky každé stránky.

Nemá-li majitel tyhle stránky připravené, **řekni to** — je to jeho rozhodnutí, ne tvoje.

---

## 7. Rychlost

- **Obrázky ve WebP** (nebo aspoň komprimované), ne surové fotky z foťáku. Fotka na 4 MB udělá
  ze stránky na mobilu nepoužitelnou věc.
- **U každého obrázku uveď rozměry** (`width` a `height`), aby stránka při načítání neposkakovala.
- **Obrázky pod ohybem načítej líně** (`loading="lazy"`), ten hlavní nahoře ne.
- **Písma:** načítej jen ty řezy, které opravdu používáš, s `font-display: swap`.
- Cíl: **stránka se na mobilu ukáže do 3 sekund.**

---

## 8. Přístupnost (a je to i SEO)

- **Každý obrázek má `alt`** — popis toho, co je na něm. Dekorativní obrázek má `alt=""`.
- **Kontrast textu 4,5 : 1** vůči pozadí.
- **Tlačítko je `<button>` nebo `<a>`**, ne `<div>`, na který se dá kliknout — jinak se k němu nedá
  dostat klávesnicí.
- **Na dotek aspoň 44 × 44 px.**
- **Formulářová pole mají popisek** (`<label>`), ne jen šedý text uvnitř pole.
- **Video s mluveným slovem má titulky** nebo přepis.

---

## 9. Formulář, který někam teče

Než stránku pustíš ven, **ověř celou cestu**, ne jen že se formulář odešle:

1. Kam data tečou (e-mailový nástroj, tabulka, databáze) a **je to napojené?**
2. Co člověk uvidí po odeslání (děkovací stránka nebo hláška)?
3. Přijde mu něco e-mailem? Za jak dlouho?
4. Co se stane při **chybě** (neplatný e-mail, výpadek) — vidí to, nebo mu formulář jen zmizí?
5. **Odešli si testovací záznam sám** a zkontroluj, že dorazil.

Formulář, který nikam neteče, je nejdražší chyba na webu: stránka vypadá funkčně a kontakty se ztrácejí.

---

## 10. Odkazy a 404

- **Projdi všechny odkazy** na stránce, než ji pustíš ven. Odkaz na neexistující stránku je horší
  než žádný odkaz.
- **Odkazy ven** (na cizí web) otvírej v novém okně (`target="_blank" rel="noopener"`).
- Web má mít **vlastní 404 stránku** ve svém vzhledu, s odkazem zpátky na hlavní stránku.

---

## 11. Hlavička a patička na jednom místě, ne na každé stránce

**Menu a patičku nekopíruj do každé stránky.** Web má jedny a všechny stránky si je berou odtamtud.

Proč to není detail: jakmile jsou hlavička a patička na šedesáti místech, přestane se do nich sahat.
Přidat odkaz do patičky znamená šedesát úprav, takže se to buď neudělá, nebo se udělá jen někde
a web se rozejde. **Pozná se to podle toho, že na jedné stránce je v patičce odkaz, který na jiné chybí.**

### Jak to udělat

1. Hlavička a patička bydlí každá ve **svém souboru** (`sablony/hlavicka.html`, `sablony/paticka.html`).
2. Stránka má na jejich místě jen **značky**, kam se mají vložit:

   ```html
   <!-- #hlavicka --> <!-- /hlavicka -->
   <!-- #paticka -->  <!-- /paticka -->
   ```

3. **Sestavovač** (malý skript) před nasazením obsah mezi značky doplní. Pustí se vždycky
   před nasazením, ne ručně podle nálady.
4. **Zvýraznění stránky, na které návštěvník je**, si sestavovač spočítá sám z adresy.
   Nikdy se nenastavuje ručně na každé stránce, protože to je zase kopie, která se rozejde.

### Ne každá stránka má mít stejnou hlavičku

Prodejní stránka, objednávka a vstupní stránka **záměrně** menu nemají. Odvádělo by pryč od jediné
věci, kterou tam člověk má udělat. Na to se udělá **druhá varianta** šablony (hlavička jen s logem,
zkrácená patička jen s povinnými odkazy) a stránka si řekne o ni.

**Stránka, která nemá značky, zůstane nedotčená.** To je správně: takhle se dělá stránka, která
nemá mít ani hlavičku, ani patičku.

> **Zkratka pro kontrolu:** *„Když teď přidám odkaz do patičky, kolik souborů musím otevřít?“*
> Odpověď musí být **jeden**.

---

## Kontrolní seznam před nasazením

- [ ] `lang`, `viewport`, `charset`, favicon
- [ ] **Titulek a popisek** vyplněné a **jiné než na ostatních stránkách**
- [ ] **Sdílecí obrázek** (1200 × 630, absolutní adresa) a ověřený náhled odkazu
- [ ] **Jeden `<h1>`** a hierarchie nadpisů bez děr
- [ ] Čitelná adresa; u změněné adresy nastavené přesměrování
- [ ] **Měřicí kódy jednou**, ve sdílené části, s ověřenou událostí
- [ ] Cookie lišta, když se měří; u formuláře věta o zpracování údajů
- [ ] Obrázky komprimované, s rozměry, pod ohybem líné
- [ ] `alt` u obrázků, kontrast 4,5 : 1, tlačítka dosažitelná klávesnicí
- [ ] **Formulář otestovaný celou cestou** (odeslání → uložení → děkovačka → e-mail)
- [ ] Odkazy prošlé, 404 stránka existuje
- [ ] **Každý ovládací prvek opravdu něco dělá** — filtry, přepínače, rozbalovátka, tlačítka.
      Klikni na ně. Prvek, který vypadá funkčně a nedělá nic, je horší než žádný.
- [ ] **Text sedí muži i ženě** (žádné „poradíš si sám“, žádná lomítka) — viz `cestina-bez-ai`
- [ ] **Každá stránka načítá jeden stylový soubor** (spočítej to, viz `vizual.md` bod 2)
- [ ] **Hlavička a patička přišly ze sestavovače**, nejsou v každé stránce zvlášť
- [ ] Styly a skripty mají v adrese **otisk verze**, ať prohlížeč nedrží starou podobu
- [ ] **Projetá vizuální smyčka** podle `vizual.md` (screenshot, desktop i mobil)

**Nasazení na živý web je nevratná akce** — ukaž screenshot a nech potvrdit, pak nasazuj.

# Kontrola jednoho CSS

> K čemu to je: ověřit, že stránky webu **sdílejí styly** a nemá každá své vlastní. Když je nesdílejí,
> oprava na jedné stránce se nikam nepromítne a web se pomalu rozpadá na dvanáct různých vzhledů.
> Vzniklo z reálného nálezu 2026-08-06 (13 stránek, 0 sdílených souborů se styly).
> Naposledy změněno: 2026-08-11.

---

## Testy, které se dají spočítat

Názor se dá obejít, číslo ne. Proto dva testy, a oba mají číselnou odpověď.

> **1. Kolik stylových souborů načítá každá stránka?**
> Musí to být **jedna, na každé stránce webu**. Když se počet mezi stránkami liší, web se už větví,
> jen to ještě není vidět.

> **2. Když teď změním hlavní barvu na jednom místě, přebarví se všechny stránky?**
> Musí být ano. Když ne, není to design systém, ale sbírka kopií, které se rozejdou.

---

## Dvě pasti, do kterých se padá i s dobrým úmyslem

**Past první: „tohle je přece jen pro tuhle sekci.“** Vznikne styl pro právní stránky, pak pro
návody, pak pro objednávku. Každý sám o sobě rozumný, dohromady pět různých webů. Když sekce
potřebuje vlastní prvky, přidají se **do společného souboru jako další oddíl**, ne do nového souboru.

**Past druhá: kopie stylu v šabloně stránky.** Šablona si nese `<style>` blok, z ní vznikne dvacet
stránek a každá má vlastní kopii. Když se pak opraví společný soubor, těch dvacet kopií ho přebije
a **web se tváří, že tvoji opravu ignoruje**. Hledá se to těžko, protože v CSS je všechno správně.

*Obě pasti jsou z reálné práce na webu 2026-08-11, ne z teorie.*

---

## Kdy jeden soubor přestává být správná odpověď

Jeden soubor je pro malý a střední web **rychlejší**, ne pomalejší: prohlížeč nevykreslí stránku,
dokud nemá všechny styly, takže pět souborů znamená pět čekání místo jednoho. A po cestě se soubor
posílá zabalený, takže 40 kB kódu je ve skutečnosti okolo 9 kB dat.

**Hranice je zhruba 100 kB nekomprimovaně.** Nad ní si každá stránka stahuje velkou porci stylů,
které nikdy nepoužije, a má smysl dělit. Ale **jedině strojem při sestavování**, který zároveň hlídá,
že se nic nerozejde. Ruční dělení „tenhle soubor bude pro tuhle sekci“ je přesně past první.

---

## Prohlížeč drží starý styl (a vypadá to jako rozbitý web)

Když se stylový soubor změní, jeho adresa zůstane stejná a prohlížeč klidně ještě hodiny servíruje
starou verzi. Stránka pak vypadá rozbitě: obrázky bez rozměrů, ikony přes celou šířku, rozhozené
rozvržení. **Není to chyba v CSS, je to keš** — a stojí to hodiny hledání v souboru, kde je všechno
v pořádku.

Řešení: k adrese stylu se připojí otisk obsahu.

```
<link rel="stylesheet" href="/css/styl.css?v=a1b2c3d4">
```

Změní se soubor → změní se otisk → změní se adresa → prohlížeč si musí stáhnout nový.
Nezmění se nic → adresa zůstane → keš dál platí.

**Dělá se to automaticky při nasazování**, ne ručně. Na ruční krok se zapomene právě ve chvíli,
kdy na něm nejvíc záleží.

---

## Jak to změřit

Ve složce webu:

```bash
echo "stránek s vlastním <style> blokem: $(grep -rl '<style' --include='*.html' . | wc -l)"
echo "stránek odkazujících na lokální .css: $(grep -rl 'href="[^"]*\.css"' --include='*.html' . | grep -v fonts | wc -l)"
```

**Jak číst výsledek:**

| Co vidíš | Co to znamená |
|---|---|
| CSS souborů 0, `<style>` bloků tolik co stránek | **Rozsypané.** Každá stránka je ostrov. Oprava se nikam nepropíše. |
| CSS soubor je, ale stránky mají i vlastní `<style>` s barvami | **Poloviční.** Část se propíše, část ne. Nejzrádnější stav. |
| CSS soubor je, `<style>` bloky jen na rozvržení jedné stránky | **V pořádku.** |
| Stránka odkazuje na `.css`, který neexistuje | **Rozbité.** Stránka běží na výchozím vzhledu prohlížeče. |

Zkontroluj i to, jestli se v HTML neobjevují barvy natvrdo:

```bash
grep -rc '#[0-9a-fA-F]\{6\}' --include='*.html' . | grep -v ':0$'
```

Každý zásah je barva, která by měla být proměnná.

---

## Jak rozsypaný web posbírat zpátky

Nedělej to jedním velkým přepisem. Po krocích, s vizuální smyčkou po každém:

1. **Sesbírej hodnoty.** Projdi `<style>` bloky všech stránek a vypiš, jaké barvy, fonty a rozestupy
   se používají. Uvidíš, že jich je víc, než mělo být (tři odstíny zlaté, čtyři velikosti nadpisu).
2. **Rozhodni, co je správné.** Ne co je nejčastější, ale co je podle design systému správně.
   Rozdíly ukaž majiteli, ať potvrdí, která zlatá je ta pravá.
3. **Napiš `tokens.css`** s vyčištěnými hodnotami.
4. **Napiš `styl.css`** se společnými prvky (nadpisy, tlačítka, karty, sekce) — všechno přes proměnné.
5. **Přepiš stránky jednu po druhé.** V každé: přidat odkaz na oba soubory, vyhodit z `<style>`
   všechno, co je teď společné, nechat jen skutečná specifika téhle stránky.
6. **Po každé stránce screenshot** a porovnat s tím, jak vypadala předtím. Cíl je **stejný nebo lepší
   vzhled**, ne jiný.
7. **Nakonec pusť test znovu** a ukaž čísla před a po.

⚠️ **Přepis stránek je zásah do živého webu.** Když už web běží, nasazení potvrzuje majitel
(nevratná akce). Udělej změnu, ukaž screenshoty, teprve pak nasazuj.

---

## Pravidlo pro nové stránky

Každá nová stránka začíná odkazem na sdílené soubory, ne prázdným `<style>` blokem:

```html
<link rel="stylesheet" href="/tokens.css">
<link rel="stylesheet" href="/styl.css">
```

**Vlastní `<style>` blok smí obsahovat jen rozvržení, které je opravdu jen na téhle stránce** —
a i tam se barvy a rozestupy berou přes `var(--…)`.

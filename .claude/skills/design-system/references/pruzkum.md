# Průzkum: jak se dělá design systém

> Podklad ke skillu `design-system` (v2.0). Průzkum 2026-07-26: rozdíl design systém / style guide /
> brand guidelines, design tokens (UXPin, Design Systems Collective), metodika vizuálního brand auditu
> (Frontify, Forge & Spark, Evoke), pravidla HTML e-mailů 2026 (Designmodo, Retainful a další).

---

## 1. Tři různé věci, které se pletou

| | Co to je | Pro koho |
|---|---|---|
| **Brand guidelines** | nejširší dokument — strategie, hlas, vizuální identita, použití | čte se |
| **Style guide** | užší, jen vizuál: logo, barvy, typografie, layout | odkazuje se na něj |
| **Design system** | kódovaná knihovna komponent a hodnot (tokens) | importuje se do kódu |

**Závěr pro nás:** solopreneur bez softwarového produktu potřebuje **brand guidelines, které v sobě
absorbují style guide** — a k tomu **šablony pro kanály** (web, e-mail, sítě). Nepotřebuje kódovanou
komponentovou knihovnu jako softwarová firma. Proto náš skill míchá obojí: pojmenované hodnoty
(barvy, rozestupy, zaoblení) + komponenty + šablony podle kanálu. Název „design systém“ držíme,
protože je to termín, který lidé znají.

## 2. Hodnoty (design tokens) — a proč jsou jich potřeba jen pár

Tokeny = pojmenované hodnoty (barva, rozestup, velikost písma, zaoblení), které se dají použít
napříč nástroji a platformami. Moderní praxe jde dál než barvy a rozestupy (typografie, stavy,
animace), ale **pro malou značku má cenu jen minimální sada**:

- 4–6 barev (hlavní, doplňková, akcentní, text, pozadí, oddělovač)
- 2 fonty + 4–5 velikostí
- 1 stupnice rozestupů
- 1 zaoblení pro karty, 1 pro tlačítka
- 1–2 stíny

Víc znamená, že se to nikdo nenaučí a začne improvizovat. **Míň hodnot = větší konzistence.**

## 3. Dokumentace komponenty = vzhled + kdy + čeho se vyhnout

Napříč zdroji stejné: u komponenty nestačí, jak vypadá. Musí být i **kdy ji použít, jak se chová
a čemu se vyhnout**. Bez toho vzniká hezký manuál, podle kterého nikdo neumí pracovat.

**Důsledek pro skill:** ve fázi 3 je to explicitní požadavek u každé komponenty.

## 4. Vizuální audit — jak číst, co značka má

Z metodik brand auditu:

- Otevřít **5–10 nedávných materiálů** a porovnat, jestli hex kódy a fonty odpovídají tomu, co má být.
- Zkontrolovat **logo napříč místy** (web, sítě, e-maily, prezentace) — správná verze, proporce,
  prostor okolo.
- U fotek se ptát, jestli **vypadají jako z jednoho světa**, nebo jako složené z různých stocků.
- Projít **všechny doteky** (web, sítě, e-mail, prezentace, materiály partnerů), ne jen web.
- Zapsat správné hodnoty barev (hex a RGB) na jedno místo.

**Proč to má cenu:** lidé si nepamatují značku, která vypadá na každé platformě jinak. Rozpoznatelnost
stojí na opakování — a nekonzistence ji ředí.

**Důsledek pro skill:** vznikla samostatná reference `vizualni-audit.md` a výstup auditu má formát
**zachovat · sjednotit · chybí**.

## 5. HTML e-maily 2026 — co platí

Klíčová zjištění (detail v `sablony-kanalu.md`):

- **Inline styly** — část klientů odstraní `<style>` v hlavičce.
- **Tabulkové rozvržení**, ne `<div>` — kvůli Outlooku.
- **600 px, jeden sloupec**; responzivita se dělá obráceně než na webu (desktop základ, mobil
  přes media queries).
- **Systémové fonty s náhradou** — webové fonty se často nenačtou.
- **Bulletproof tlačítka** (HTML/CSS, ne obrázek).
- **Alternativní text** — obrázky bývají blokované.
- **Tmavý režim:** průhledné PNG, netvrdit bílé pozadí, testovat; Gmail, Outlook a Apple Mail se chovají různě.
- **Pod 100 kB** — Gmail nad ~102 kB obsah zkrátí.

---

## 6. Když značka nemá nic — jak vzhled objevit

Z metodik brandových discovery dotazníků a práce grafiků s klienty:

- **Neptej se na preference slovy, nech vybírat z obrázků.** *„Vyber 3 obrázky, které ti připadají
  jako tvoje značka"* dá výrazně použitelnější směr než jakýkoli slovní popis. Totéž u log: nech
  ukázat 2–3, které se líbí, a **doptej se, co konkrétně** na nich (jednoduchost, barevnost,
  modernost, symbolika).
- **Mood board** jako společný jazyk — prohlížet cizí značky spolu a mluvit o nich **očima cílovky**,
  ne očima majitele.
- Otázky mají mířit na **publikum a pocit**, ne na vkus majitele.

### Barvy — co je podložené
- **Teplé** (červená, oranžová, žlutá) = energie, chuť, akce; časté v jídle, fitness, zábavě.
- **Studené** (modrá, zelená, fialová) = klid, důvěra, profesionalita; časté v technice, financích,
  zdraví.
- **Sytost** rozhoduje o hlasitosti: vysoká sytost přitahuje pozornost a budí vzruch, nízká působí
  klidně a dráž.
→ Proto se v režimu B ptáme na **teplotu, sytost a světlost**, ne na konkrétní barvu.

### Písmo — co je podložené
- **Patková** písma lidé hodnotí jako stabilní, praktická, zralá a formální.
- **Bezpatková** jako moderní, jasná a přístupná; převažují na webu (v jedné studii preference
  ~62 % pro text na webu, zatímco patková ~71 % pro obchodní dokumenty).
- Když **osobnost písma sedí k osobnosti značky**, reakce lidí jsou měřitelně příznivější
  (výzkum Monotype uvádí až +13 %).
→ Proto se font vybírá podle **slov z otázky „jak se má čtenář cítit“**, ne podle módy — a vždycky
se ukazuje na stejném textu ve dvou až třech variantách.

### Zdroje k tomuhle bloku
- Brandový discovery dotazník a práce s obrázky — https://www.weavely.ai/blog/branding-questionnaire-how-to-ask-the-right-questions-and-actually-get-useful-answers · https://manyrequests.com/blog/branding-questionnaire-for-clients
- Teplé vs. studené barvy a sytost — https://www.brandcrowd.com/blog/the-psychology-of-warm-vs-cool-colors · https://madegooddesigns.com/warm-vs-cool-colors/
- Vnímání písem (osobnostní rysy fontů) — https://soma.sbcc.edu/users/russotti/113/personality_Shaikh.pdf · https://anonymous.com.sg/the-psychology-behind-font-personality-and-when-to-use-serif-vs-sans-serif/

## Co jsme vědomě NEpřevzali

- **Kódovaná komponentová knihovna** (Storybook, Figma library s variantami). Pro solopreneura je to
  režie, kterou neudrží. Stačí popis a jedna ukázka.
- **Rozsáhlé brand manuály na 40 stran.** Nikdo je nečte a agent z nich neumí vybrat pravidlo.
  Náš výstup je jeden soubor, který se dá projít za pět minut.
- **CMYK a tiskové specifikace** — u online byznysu jen na vyžádání.
- **Automatické generátory tokenů z webu.** Vytáhnou hodnoty, ale nerozliší záměr od nahodilosti;
  pořád je potřeba otázka „je to schválně, nebo se to sešlo?“.

## Zdroje

- Design system vs. style guide vs. brand guidelines — https://www.digitalpolo.com/design-system-vs-style-guide-vs-brand-guidelines/
- Design tokens — https://www.uxpin.com/studio/blog/what-are-design-tokens/ · https://www.designsystemscollective.com/design-tokens-in-2026-beyond-colors-and-spacing-d2fd632029e1
- Stavba design systému — https://kreativagroup.com/post/how-to-create-a-design-system-that-scales-in-2026
- Vizuální brand audit — https://forgeandspark.com/the-ultimate-guide-to-a-brand-visual-audit/ · https://www.frontify.com/en/guide/brand-audit · https://madebyevoke.com/blog/brand-consistency-audit
- HTML e-maily — https://designmodo.com/html-css-emails/ · https://www.retainful.com/blog/email-design-best-practice · https://startup-house.com/blog/best-practices-responsive-html-email-design

**Vytvořeno:** 2026-07-26.

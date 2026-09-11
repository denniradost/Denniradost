# Kostry stránek prezentačního webu

> Každá stránka má **jednu hlavní akci** (stejnou napříč webem, nebo její místní podobu), mluví
> k návštěvníkovi a končí krokem dál. Pořadí sekcí je doporučení, ne dogma; co nemá obsah,
> vynechej (prázdná sekce je horší než žádná). Texty: hlas majitele, `cestina-bez-ai` na závěr.
> Vzhled: design systém a standardy (`vizual.md`, `ctivost.md`, `webova-stranka.md`).

## Společné pro všechny stránky

- **Hlavička:** logo (odkaz na domov) · menu 4 až 6 položek · zvýrazněné tlačítko hlavní akce.
  U provozovny telefon v hlavičce. Na mobilu sbalené menu, tlačítko zůstává viditelné.
- **Patička:** 3 skupiny vedle sebe (na mobilu pod sebou):
  1. **Navigace** (stejné položky jako menu + Reference + Obsah zdarma, když existuje)
  2. **Kontakt a identifikace:** jméno / obchodní firma, IČO, sídlo, zápis v rejstříku, DIČ
     (u plátce), e-mail, telefon, sítě
  3. **Právní:** Ochrana osobních údajů · Cookies (jen když jsou) · Obchodní podmínky (jen když se
     na webu objednává) · © rok
- **Každá stránka:** titulek a popisek pro vyhledávač, sdílecí obrázek, jeden H1, čitelná adresa
  (`/sluzby`, `/o-mne`, `/kontakt`), stejný design, hlavní akce na konci.

## 1. Domovská stránka

**Úkol:** za 5 sekund říct co, pro koho a co teď; pak jemně vést k hlavní akci.

| # | Sekce | Obsah | Akce |
|---|---|---|---|
| 1 | **Hero** | Nadpis = co děláš a pro koho (slovy zákazníka, ne oboru) · podnadpis = výsledek nebo jak · **fotka skutečného majitele, místa nebo práce** · 1 hlavní tlačítko, nanejvýš 1 vedlejší (textový odkaz) | hlavní |
| 2 | **Důkaz hned** | Jedna silná reference, číslo („1 200 klientů za 8 let“), loga, hodnocení z Googlu. Krátké, skenovatelné | – |
| 3 | **Pro koho a s čím** | 3 až 4 dlaždice: situace zákazníka → co s tím děláš. Ne seznam služeb, ale seznam problémů | odkaz na službu |
| 4 | **Jak to probíhá** | 3 kroky od prvního kontaktu k výsledku. Snižuje strach z neznámého („co se stane, když zavolám“) | hlavní |
| 5 | **Krátce o mně** | 3 až 5 vět + fotka: kdo, proč tohle, jeden fakt. Odkaz na O mně | „Poznej můj příběh“ |
| 6 | **Reference** | 2 až 3 skenovatelné (výsledek nahoře, jméno, fotka) + odkaz na stránku Reference | – |
| 7 | **Obsah zdarma** (expert) / **Ukázky práce** (řemeslník) / **Ceník** (provozovna) | Podle typu; jen když je co ukázat | odkaz |
| 8 | **Hlavní akce znovu** | Pozvánka: co se stane po kliknutí, do kdy se ozveš | hlavní |
| 9 | **Patička** | viz výš | – |

Expertní web s víc vstupními body (magnet, webinář, vstup do prostoru): hlavní blok hned za hero
je ten nejdůležitější vstup (například webinář), reference **rozmístěné** k tomu, k čemu patří,
ne v jednom bloku. Bez tlaku, bez odpočtů.

## 2. O mně / O nás

**Úkol:** proměnit zvědavost v důvěru. Druhá nejnavštěvovanější stránka, čte se brzy, při
rozhodování, jestli ti věřit.

1. **Nadpis o čtenáři** („Pomáhám {komu} {co}“), ne „O mně“ jako jediný nadpis.
2. **Souhrn v prvním odstavci:** kdo jsi, co děláš, pro koho, kde, 2 až 3 konkrétní fakta (roky,
   počty, certifikace). Člověk, který nečte dál, ví to podstatné.
3. **Příběh, zkrácený**, ve 4 částech: jak to vypadá dnes → nebylo to tak vždycky → údolí (co se
   nedařilo) → zlom a proč děláš zrovna tohle. Jedna scéna místo kroniky. Plnou verzi a napojení na
   metodu dělá skill `expertni-pribeh`; sem jde jeho zkrácená verze.
4. **Čím se lišíš** (slovy klientů) a **na čem si zakládáš** (2 až 3 doložitelné hodnoty).
5. **Tým** (u firmy): jméno, role, fotka, jedna lidská věta. Bez fotek tým nepůsobí skutečně.
6. **Fakta a důkazy:** čísla, loga, média, ocenění. Skenovatelně.
7. **Skutečné fotky** majitele (a místa). Ne fotobanka.
8. **Akce na konci:** hlavní akce webu, nebo „Napiš mi“ s odkazem na Kontakt.

Ne: životopis od narození · „jsme dynamická firma s individuálním přístupem“ · stránka bez fotky.

## 3. Služby / Nabídka (rozcestník)

**Úkol:** mapa toho, s čím pomáháš, a rychlá cesta ke správné službě.

- Úvod 2 věty: pro koho a co dohromady.
- **Karta na službu** (3 až 6): název běžnými slovy · pro koho · co dostane (výsledek, ne proces) ·
  cena / „od“ / „po úvodním hovoru“ (řekni to, neschovávej) · tlačítko.
- Tlačítko vede podle typu služby:
  - **na poptávku** → stránka služby (níž) nebo rovnou formulář poptávky
  - **prodává se na webu** (kurz, členství) → prodejní stránka (skill `sales-page`), ne sem
  - **rezervace** → rezervační systém
- Na konci: „Nevíš, co vybrat?“ + hlavní akce (úvodní hovor, poptávka).
- Pojmenuj položku menu **Služby** (řemeslník, provozovna, kouč) nebo **Programy** (expert s kurzy,
  má větší hodnotu než „Kurzy“). Ne „Nabídka“ a „Služby“ vedle sebe.

### 3a. Stránka jedné služby (na poptávku)
Nadpis se službou a pro koho · problém → co s tím uděláme · **jak to probíhá ve 3 až 4 krocích** ·
co je v ceně a cena / rozpětí · reference k téhle službě · časté otázky (3 až 5) · poptávka
(formulář 3 až 5 polí nebo telefon) · odkaz zpět na rozcestník. Jedna služba = jedna stránka,
když ji lidé hledají samostatně (vyhledávač) nebo se výrazně liší cenou a zákazníkem.

## 4. Reference

**Úkol:** samostatná stránka s důkazy, na kterou se dá odkázat odkudkoli (patička, e-mail, nabídka)
a kterou najde vyhledávač. Zároveň jsou reference **rozmístěné** po webu tam, kde vzniká
pochybnost (u služby, u ceny, u tlačítka). Stránka sama o sobě nestačí.

- Nadpis o výsledku („Co se změnilo lidem, se kterými pracuju“).
- **Skenovatelná struktura reference:** výsledek tučně nahoře · 2 až 4 věty · jméno, role/město,
  fotka (nebo iniciály, když nechce). Video reference, když jsou.
- Seskupit podle služby nebo typu zákazníka, když jich je víc než 8.
- **Odkaz na externí recenze** (Google, Firmy.cz, Seznam): lidé jim věří víc než recenzím na
  vlastním webu. Když ještě nejsou, poprosit o ně je první úkol (skill `socialni-dukazy`).
- Na konci hlavní akce.
- Nic vymyšleného, nic „upraveného do krásy“: reference, která zní jako reklama, přestává být důkazem.

## 5. Kontakt

**Úkol:** aby se člověk, který se rozhodl ozvat, ozval. 44 % lidí odejde, když kontakt nenajde.

1. Nadpis lidsky („Ozvi se, ozvu se do 24 hodin“).
2. **Všechny kanály vedle sebe:** telefon (nezakrývat, klikací na mobilu) · e-mail (klikací) ·
   adresa / oblast působení · sítě · případně WhatsApp / Messenger.
3. **Doba odpovědi** a **otevírací doba** (provozovna: včetně svátků a dovolené; zákaznice, která
   přijde na zavřeno, se nevrátí).
4. **Mapa** u provozovny, foto vchodu, jak zaparkovat.
5. **Formulář 3 až 5 polí** (jméno, e-mail, zpráva; telefon volitelně). Bez povinné registrace,
   bez „předmětu“ z rozbalovací nabídky. Tlačítko říká, co se stane („Odeslat, ozvu se do 24 hodin“).
6. **Po odeslání:** poděkování na stránce nebo krátká děkovací stránka + potvrzení e-mailem.
   Formulář otestovaný celou cestou, než se web spustí.
7. **Fotka člověka, který odpoví.** Formulář bez tváře je zeď.
8. Časté otázky (3 až 5), když opakovaně chodí stejné.
9. Identifikační údaje firmy (mohou být tady i v patičce).

## 6. Právní stránky
Viz `pravni-minimum.md`. Vlastní adresy (`/ochrana-udaju`, `/cookies`, `/obchodni-podminky`),
odkaz z patičky, prostý text, datum poslední aktualizace. V menu nikdy.

## 7. Stránka 404
Lidsky („Tahle stránka tu není“), odkaz na domov, na Služby a Kontakt, případně hledání. Stejný
design jako zbytek webu. Vyhledávač musí dostat kód 404, ne 200.

## Co na prezentační web nepatří (a kam to patří)

| Věc | Kam |
|---|---|
| Vstupní stránka s magnetem | `vstupni-stranka`, na pozadí, odkaz z hero / Obsah zdarma |
| Prodejní stránka | `sales-page`, na pozadí, odkaz z rozcestníku služeb |
| Objednávková a děkovací stránka | `objednavkova-stranka`, `dekovaci-stranka` |
| Kampaně, výzvy, webináře | `funnel-mapa` + příslušné stránky, odkazované z webu |
| Blog | jen když ho bude majitel opravdu psát; jinak obsah zdarma jako pár stálých návodů |

**Vytvořeno:** 2026-09-06.

---
name: prezentacni-web
description: >
  Provede člověka k jeho **prezentačnímu webu** (vizitce firmy nebo osobnímu webu): účel webu
  a jedna hlavní akce, **menu a logika navigace**, **domovská stránka**, **O mně / O nás**,
  **Služby (rozcestník nabídky)**, **Reference**, **Kontakt**, **patička a právní stránky**.
  Nejdřív se podívá, co o majiteli a firmě už ví (firemní mozek, podklady, sousední skilly),
  a na zbytek se **zeptá v rozhovoru**, aby agent měl podklady pro texty i stavbu. Univerzální:
  kadeřnictví, kouč, konzultant, řemeslník, malá firma, osobní web experta. Spouští se, když
  uživatel řekne: „chci web“, „prezentační web“, „webová vizitka“, „firemní web“, „osobní web“,
  „web pro moje podnikání“, „co má být na mém webu“, „stránka O mně“, „domovská stránka“,
  „úvodní stránka“, „stránka Kontakt“, „stránka Reference“, „stránka Služby“, „menu na web“,
  „patička webu“, „co musí být na webu ze zákona“, „/prezentacni-web“. NE pro: vstupní stránku
  s magnetem (`vstupni-stranka`), prodejní stránku (`sales-page`), objednávkovou stránku
  (`objednavkova-stranka`), děkovací stránku (`dekovaci-stranka`), techniku webu, doménu
  a nasazení (`web-setup`), vzhled (`design-system`). Ty stránky na prezentační web NEPATŘÍ,
  tenhle skill na ně jen odkazuje.
---

# Skill: Prezentační web

**Než začneš:** web je sdělení. Platí standard `standardy/sdeleni.md` (komu to je a jeho
slova · co mu to nabízí · kam ho to vede · čí hlas · poctivost). Projdi ho před první větou.

Prezentační web je **vizitka, která odpovídá na 3 otázky dřív, než člověk stihne odejít:**
*Co děláš? Pro koho? Co mám udělat teď?* Návštěvník se rozhoduje během několika sekund, většina
lidí na webu čte jen zlomek textu a 44 % odejde, když nenajde kontakt. Web není brožura
o firmě. Je to cesta od cizího člověka k prvnímu kroku (rezervace, poptávka, hovor, registrace).

**Zlaté pravidlo:**
> Web mluví o **návštěvníkovi**, ne o majiteli. Každá stránka má **jednu hlavní akci**.
> Co k ní nevede, na web nepatří (nebo patří na pozadí, dostupné odkazem, ne v menu).

**Co tenhle skill NEstaví:** vstupní stránky s magnetem, prodejní a objednávkové stránky,
děkovačky, funnely. To jsou samostatné nástroje s vlastními skilly. Prezentační web na ně jen
**odkazuje** (z menu, z rozcestníku služeb, z tlačítka), nikdy je nenahrazuje. Když člověk chce
„web, na kterém se prodává kurz“, postav mu prezentační web tímhle skillem a prodejní stránku
skillem `sales-page` jako samostatnou stránku na pozadí.

---

## Pořadí práce: nejdřív obsah, pak vzhled, pak technika

1. **Obsah a struktura** (tenhle skill, kroky 1 až 4): účel, hlavní akce, menu, mapa webu, texty
   stránek → `web-struktura.md`, **majitel ho odsouhlasí**.
2. **Vzhled** (skill `design-system`): až teď. Design systém potřebuje skutečné texty (nadpisy,
   služby, reference) do vzorové stránky, a ty vznikají v kroku 1. Když majitel už logo a barvy má,
   design systém je jen zachytí; když nemá, vymyslí se **na hotový obsah**, ne naopak.
3. **Technika** (skill `web-setup`): doména, hosting, nasazení. Klidně souběžně s krokem 2.
4. **Stavba a kontrola** (krok 5 níž): stránky z obsahu + vzhledu, vizuální smyčka, spuštění.

🔴 **Nezačínej barvami, písmem ani stavbou stránek, dokud `web-struktura.md` neexistuje
a majitel ho neviděl.** Web, který začne designem, je web o majiteli; web, který začne obsahem,
je web o zákazníkovi. Když majitel začne otázkou na vzhled („jaké barvy?“), řekni mu, že vzhled
přijde jako druhý krok, a vrať ho k otázce, co má web říct a kam vést.

## Krok 0: Co musím mít, než začnu (vstupní brána)

**Nejdřív hledej, pak se ptej, nikdy nepředpokládej.** Většina podkladů už může existovat.

| Vstup | Kde ho hledám (hotový výsledek) | Když chybí (postup, jak ho vytvořit) |
|---|---|---|
| **Kdo je majitel a firma** (co dělá, pro koho, kde, jak dlouho) | firemní mozek: firemní a osobní kontext | rozhovor níž; hlubší poznání skilly `firemni-kontext` / `osobni-kontext` |
| **Zákazník a jeho slova** | pravda o zákazníkovi, `pruzkum-trhu.md` | rozhovor (blok B); u experta, který chce web „na míru trhu“, skill `pruzkum-trhu` |
| **Nabídka** (služby, produkty, ceny) | kanonický zdroj o produktech a cenách | rozhovor (blok C). **Ceny nikdy netipuj** |
| **Příběh na O mně** | `pribeh.md` (výstup skillu `expertni-pribeh`) | rozhovor (blok D) dá krátkou verzi; plný příběh skill `expertni-pribeh` |
| **Reference a důkazy** | sbírka důkazů, `socialni-dukazy` | rozhovor (blok E); jak je získat: skill `socialni-dukazy` |
| **Hlas majitele** | stylový průvodce v mozku | teprve pak skill `styl-komunikace`; když ho dělat nechce, piš a označ, že tón je odhad |
| **Vzhled** | design systém projektu (`design-system.md`, tokeny) | skill `design-system`, **ale až po kroku 4** (potřebuje hotové texty). Bez něj nestavěj, vznikne web s tolika vzhledy, kolik má stránek |
| **Technika** (doména, hosting, nasazení) | `web-infrastructure.md` | skill `web-setup` |
| **Právní údaje** (IČO, sídlo, forma) | firemní kontext | rozhovor (blok F); `references/pravni-minimum.md` |

Sousední skill, který **nemáš**, nezastaví práci: místo něj se zeptám na otázky z rozhovoru
(příslušný blok) a řeknu jednou větou, co by přidal. Standardy jsou ve složce `standardy/`
(dostal jsi je s balíčkem); nemáš-li je, platí aspoň to, co je u nich v závorce.

**Před stavbou stránek:** standardy `standardy/vizual.md` (vzhled se bere, ne vymýšlí; jedno CSS;
vizuální smyčka), `standardy/ctivost.md` (šířka textu, záchytné body) a `standardy/webova-stranka.md`
(titulek, popisek, sdílecí obrázek, jeden H1, měření se souhlasem, formulář otestovaný celou
cestou, 404). Má-li web vlastní stavebnici (soubor s kostrou stránky a názvy komponent), platí navíc ona.

## Když něco nevím, zeptám se

Otázky jsou v `references/rozhovor.md`, rozdělené do bloků A až F. **Ptej se jen na to, co jsi
nenašel.** Když už mozek zná firmu, zákazníka i ceny, zbývá typicky 5 otázek. Když člověk nemá
nic, jde to na 2 dávky (nejdřív blok A + B + C, pak D + E + F), vždy **bez otázek, na které už
odpovědělo samo zadání** (typ podnikání, město). Vždy s návrhem odpovědi, ať stačí
„ano“ nebo oprava. Rozliš **musím vědět** (typ podnikání, hlavní akce, nabídka, kontakt, právní
údaje) a **hodilo by se** (příběh, reference, fotky): bez druhé skupiny web postavíš s označeným
místem „sem doplníš“.

---

## Postup

### 1. Účel webu a hlavní akce (jedna věta)
Než vznikne první stránka, napiš jednu větu: *„Web má {komu} ukázat {co} a přivést ho k {jedna
akce}.“* Hlavní akce se liší podle typu podnikání a je to **nejdůležitější rozhodnutí celého webu**:

| Typ | Hlavní akce (tlačítko v menu i v hero) | Vedlejší |
|---|---|---|
| Místní provozovna (kadeřnictví, studio, ordinace) | **Rezervovat termín** / zavolat | kde nás najdeš, ceník |
| Řemeslník, služby na zakázku | **Nezávazná poptávka** / zavolat | ukázky práce, oblast působení |
| Kouč, konzultant, terapeut | **Úvodní hovor zdarma** / poptávka | něco zdarma, příběh |
| Expert s online produkty | **Něco zdarma** (magnet, webinář, vstup do prostoru), ne „koupit“ | programy, obsah zdarma |
| Malá firma, tým | **Poptávka** / kontakt | reference, tým |

Expertní web vede na **vztah, ne na nákup**: hlavní tlačítko je registrace, e-mail nebo webinář,
prodej přijde uvnitř (vzorec, který drží Hormozi, Kern, Burchard, Porterfield, Sigrun; podrobně
`references/pruzkum.md`). U provozovny a řemeslníka je hlavní akce naopak co nejkratší cesta
k objednání.

### 2. Menu a logika navigace
- **4 až 6 položek + 1 zvýrazněné tlačítko** (hlavní akce). Ne proto, že „sedm je limit“ (to je
  mýtus), ale proto, že prezentační web víc věcí, které lidé hledají, nemá.
- **Běžná slova, ne značky ani slovní hříčky:** *Služby · O mně · Reference · Kontakt*. Lidé
  neklikají na odkaz, u kterého netuší, co za ním je. Jméno majitele jako položka („majitel“) funguje
  jen u osobní značky, kde lidi jméno znají.
- Každá položka **jedna jasná věc**, položky se nepřekrývají („Služby“ a „Nabídka“ vedle sebe je chyba).
- **Bez rozbalovacích menu**, dokud web nemá víc než zhruba 8 stránek.
- **Co v menu NENÍ:** prodejní stránky, objednávky, děkovačky, právní stránky (patička),
  kampaně. Zobrazí se, jen když k nim člověk dojde přirozenou cestou.
- Kontakt je **vždy v menu i v patičce**; telefon u provozovny navíc v hlavičce.
- Na mobilu: hlavní tlačítko viditelné i po sbalení menu.

### 3. Seznam stránek (mapa webu)
Základ pro každého: **Domovská · O mně (O nás) · Služby · Reference · Kontakt · Ochrana údajů
(+ Cookies) · 404.** Volitelně: stránka jedné služby (když ji lidé hledají samostatně nebo se prodává
na poptávku), Ceník (provozovna), Ukázky práce (řemeslník), Obsah zdarma (expert), Obchodní podmínky
(jen když se na webu objednává nebo platí). Mapu ulož jako `web-struktura.md` do složky projektu:
stránka · účel · hlavní akce · odkud se na ni vede.

### 4. Texty stránek podle koster
Každá stránka má svou kostru v `references/kostry-stranek.md`. Nejdůležitější body:

- **Domovská:** hero (co děláš + pro koho + hlavní akce + fotka skutečného člověka nebo místa,
  žádná fotobanka lidí v obleku), hned důkaz (jedna reference, číslo, loga), pro koho a s čím
  (3 až 4 dlaždice), jak to probíhá (3 kroky), krátce o mně s odkazem, reference, hlavní akce
  znovu, patička. **Test 5 sekund:** cizí člověk po 5 s řekne, co děláš, pro koho a co má udělat.
- **O mně:** nadpis o čtenáři, ne o majiteli · první odstavec je **souhrn** (kdo, co, pro koho,
  2 až 3 konkrétní fakta) · pak příběh, zkrácený, ve 4 částech (dnes → nebylo to tak vždy → údolí →
  zlom, plnou verzi dělá `expertni-pribeh`) · hodnoty a čím se lišíš · skutečné fotky · akce
  na konci. Druhá nejnavštěvovanější stránka webu, přes polovinu lidí ji hledá při prvním kontaktu.
- **Služby (rozcestník nabídky):** karta na službu: pro koho · co · výsledek · cena nebo „od“ ·
  akce. Služba, která se prodává na webu → odkaz na prodejní stránku (jiný skill). Služba na
  poptávku → vlastní stránka s postupem ve 3 až 4 krocích a poptávkou.
- **Reference:** samostatná stránka (kvůli vyhledávačům a prokliku odkudkoli) + reference
  **rozmístěné** tam, kde vzniká pochybnost. Výsledek nahoře, jméno, fotka; skenovatelná struktura
  dostává o 74 % víc pozornosti než odstavec. Odkaz na externí recenze (Google, Firmy.cz), lidé jim
  věří víc než těm na vlastním webu.
- **Kontakt:** **všechny kanály** (telefon nezakrývat, e-mail, adresa, sítě), doba odpovědi
  („ozvu se do 24 hodin“), otevírací doba a mapa u provozovny, formulář **3 až 5 polí**, co se
  stane po odeslání, fotka člověka, který odpoví.
- **Patička (na každé stránce):** 3 skupiny: navigace · kontakt + identifikační údaje ·
  právní odkazy. Sem patří i odkaz na Reference a sítě.
- **Právní stránky:** `references/pravni-minimum.md`. Identifikační údaje (jméno/firma, IČO, sídlo,
  zápis v rejstříku, DIČ u plátce) patří na web ze zákona, i když se na něm nic neprodává.
  Cookies lišta jen tehdy, když web nasazuje nepovinné cookies (měření, reklama).

Kde vzniká text s nadpisem nebo tlačítkem: nadpisy `nadpisy-a-nazvy`, tlačítka `vyzva-k-akci`,
delší souvislý text `prodejni-text`. **Vždy hlasem majitele**, nikdy obecnou marketingovou češtinou.

### 5. Stavba a kontrola
Stavba podle design systému a `web-setup` (jedno CSS, žádné barvy natvrdo). Před ohlášením
hotovo **vizuální smyčka** na počítači i mobilu, formulář projetý celou cestou (odeslat, přijde
e-mail, děkovací stav), a `cestina-bez-ai` na všechny texty.

### 6. Výstup
- `web-struktura.md` (mapa webu, menu, hlavní akce, texty stránek) ve složce projektu nebo klienta.
- Hotové stránky nasazené podle `web-infrastructure.md`.
- Kde vzniká rozhodnutí (název položky menu, hlavní akce, nadpis hero, pořadí sekcí): **3 varianty
  a jedno doporučení** s jednou větou proč.

---

## Na co pozor

- ❌ Začít barvami a písmem → ✅ nejdřív `web-struktura.md`, vzhled až na hotový obsah
- ❌ Web o majiteli („jsme dynamická firma“) → ✅ web o návštěvníkovi a jeho situaci
- ❌ Tři tlačítka v hero → ✅ jedna hlavní akce, nanejvýš jedna vedlejší
- ❌ Menu z 9 položek a rozbalovaček → ✅ 4 až 6 + tlačítko
- ❌ Fotobanka usmívajících se lidí v obleku → ✅ skutečný majitel, skutečné místo, skutečná práce
- ❌ O mně jako životopis od narození → ✅ souhrn napřed, příběh zkrácený, závěr s akcí
- ❌ Schovaný telefon, jen formulář → ✅ všechny kanály + doba odpovědi
- ❌ Reference jen v jedné sekci dole → ✅ rozmístěné k pochybnostem + samostatná stránka
- ❌ Prodejní a objednávkové stránky v menu → ✅ na pozadí, přes rozcestník služeb
- ❌ Chybějící IČO a sídlo („my nic neprodáváme“) → ✅ povinné pro každého podnikatele s webem
- ❌ Cookies lišta „pro jistotu“ bez cookies → ✅ lišta jen tam, kde jsou nepovinné cookies
- ❌ Vymyšlené počty a recenze → ✅ poctivost nad konverzí, chybějící důkaz pojmenovat
- ❌ Hotovo bez pohledu na mobil → ✅ vizuální smyčka, screenshot, oprava

## Checklist před spuštěním

- [ ] Umí cizí člověk po **5 sekundách** na domovské říct, co děláš, pro koho a co má udělat?
- [ ] Má web **jednu hlavní akci** a je v menu, v hero i na konci každé stránky?
- [ ] Má menu **4 až 6 položek** s běžnými slovy a bez překryvů?
- [ ] Mluví **O mně** nejdřív ke čtenáři a začíná souhrnem?
- [ ] Jsou na Kontaktu **všechny kanály**, doba odpovědi a formulář do 5 polí, projetý celou cestou?
- [ ] Jsou reference **rozmístěné** a existuje stránka Reference odkazovaná z patičky?
- [ ] Je v patičce **jméno/firma, IČO, sídlo, zápis v rejstříku** (DIČ u plátce) a odkaz na ochranu údajů?
- [ ] Jsou prodejní, objednávkové a děkovací stránky **mimo menu**?
- [ ] Vzhled z **design systému**, jedno CSS, skutečné fotky, žádné Lorem Ipsum?
- [ ] Titulek, popisek, sdílecí obrázek, 404, měření jen se souhlasem (`webova-stranka.md`)?
- [ ] Prošel jsem to na **počítači i mobilu** a texty skillem `cestina-bez-ai`?
- [ ] Je `web-struktura.md` uložený a majitel ví kde?

## Smyčka učení

Co se o firmě dozvíš v rozhovoru (nabídka, ceny, hlavní akce, právní údaje, hlas), **zapiš do
firemního mozku**, ne jen do webu: příště se na to nikdo nebude ptát znovu. Rozhodnutí s důvodem
(proč tahle hlavní akce, proč tohle menu) do deníku. Když majitel opraví strukturu nebo text,
oprava jde zpátky sem do „Na co pozor“.

## Vazby

- **Před tím:** `design-system` (vzhled), `web-setup` (technika); volitelně `pruzkum-trhu`,
  `expertni-pribeh`, `socialni-dukazy`, `styl-komunikace`.
- **Uvnitř:** `nadpisy-a-nazvy`, `vyzva-k-akci`, `prodejni-text`, `cestina-bez-ai`.
- **Po tom (na pozadí webu, jiné skilly):** `vstupni-stranka`, `sales-page`, `objednavkova-stranka`,
  `dekovaci-stranka`, `funnel-mapa`.

## Reference

| Soubor | Co v něm je |
|---|---|
| `references/rozhovor.md` | Otázky v blocích A až F, co hledat dřív, návrhy odpovědí, podle typu podnikání |
| `references/kostry-stranek.md` | Kostra každé stránky sekci po sekci: domov, O mně, služby, reference, kontakt, patička, 404 |
| `references/pravni-minimum.md` | Co na webu musí být ze zákona (ČR), cookies, ochrana údajů, podmínky, přístupnost |
| `references/pruzkum.md` | Průzkum se zdroji a datem + co jsme vědomě nepřevzali |

**Vytvořeno:** 2026-09-06 (MAIA) z majitelova zadání („průvodce, který provede člověka k jeho
webu; vyzpovídat ho, když to v mozku není“) + průzkumu (NN/g, Baymard, Stanford, KoMarketing,
české právní zdroje) + strategie nového webu Digitálního Mága (2026-07-24).


---

## Kde si beru zbytek (rejstřík)

Nepředpokládám, že máš všechno. Než začnu:

1. **Kontext** — kdo jsi, co prodáváš, jak píšeš a jak to u tebe vypadá — beru z **tvého firemního
   mozku**. Když tam něco chybí, zeptám se tě na to nejnutnější a půjdu dál.
2. **Navazující dovednosti** — podívám se do **knihovny skillů** (`list_skills`), jestli tam není
   něco, co k téhle práci patří (třeba nadpisy, výzvy k akci, reference, prodejní text).
   Když navazující skill máš, použiju ho. Když ne, řeknu ti jednou větou, co by přidal — a práci
   odvedu i bez něj.

Knihovna roste. Proto se do ní dívám pokaždé znovu, místo abych se spoléhal na seznam v tomhle textu.

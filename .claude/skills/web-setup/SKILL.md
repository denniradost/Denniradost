---
name: web-setup
description: >
  Připraví technické prostředí pro nový web (doména, hosting, nasazování) tak,
  aby do něj další skilly (vstupní a děkovací stránka, prodejní stránka a další) mohly
  automaticky nasazovat hotové stránky. **Napojí agenta na Cloudflare**, aby uměl nasazovat
  sám bez klikání, **rozplete doménu a DNS** (zjistí, kam vede, a když na ní běží živý web,
  nabídne subdoménu místo riskantního překlopení) a **založí sdílené styly**, aby se web
  nerozpadl na tolik vzhledů, kolik má stránek. Zvládne i případ, kdy uživatel doménu nemá
  ani nechce — aplikace může běžet na adrese zdarma. Spouští se když uživatel říká "chci si
  založit web", "potřebuju doménu", "kde mám hostovat web", "jak nastavit web", "připrav mi
  Cloudflare", "rozjet nový web", "potřebuju webhosting", "mám doménu, co dál",
  "nastav DNS", "udělej subdoménu", "deployuj web na Cloudflare", nebo cokoliv ohledně technického
  setupu webu (NE design, NE copy — jen infrastruktura). Tento skill je první
  v rodině web-* skillů a jeho výstupem je `web-infrastructure.md`, který další
  skilly čtou.
---

# Skill: Nastavení webového prostředí

Tento skill provede uživatele kompletním technickým setupem nového webu — od domény přes hosting až po automatický deploy. Výstupem je funkční prostředí, kam pak ostatní skilly (sales-page, prezentacni-web, ...) automaticky nasazují hotové stránky.

**Čeho se skill NETÝKÁ:**
- ❌ Designu (barvy, fonty, vizuál) → použij `design-system`
- ❌ Obsahu stránek (copy, prodejní text) → použij `sales-page` (prodejní stránka) nebo `prezentacni-web` (prezentační web: domov, O mně, služby, reference, kontakt)
- ❌ Mioweb a podobných WYSIWYG nástrojů — tento skill řeší *kódový* web, který Claude Code dokáže sám nasadit

## Místo v rodině web-* skillů

```
0. standardy            ← pravidla platná napříč vším (vizuál + čtivost + webová stránka)
                              ↓
1. cloudflare-pristup   ← napojení agenta (účet, klíč, DNS)  ← volá se z fáze 2
                              ↓
2. web-setup (TENTO)    → web-infrastructure.md + sdílené styly (tokens.css, styl.css)
                              ↓
3. design-system        → tokens.css se skutečnými barvami, vzorová stránka, přehled prvků
                              ↓
4. vstupni-stranka / dekovaci-stranka / sales-page …
                        → konkrétní stránky, které čtou výstupy výše a nasazují se
                          do prostředí připraveného tímhle skillem
```

Pořadí: **standardy → přístup → technika (tenhle skill) → vzhled → stránky.**

**Když některý článek chybí, skill funguje dál** — jen řekne, co si tím uživatel zhoršuje,
a nabídne doplnění. Nikdy se nezasekni na tom, že něco není.

📐 **Standardy jsou povinné čtení, ne doporučení.** U nás `standardy/vizual.md`
(jedno CSS · vizuální smyčka · reálné texty), `standardy/ctivost.md` (šířka a velikost čteného
textu, sekání dlouhého textu záchytnými body, zvýraznění ≠ tlačítko) a `standardy/webova-stranka.md` (titulek a popisek ·
sdílecí obrázek · měřicí kódy jednou · formulář otestovaný celou cestou · 404). Kdykoli v rámci
nastavení vzniká stránka — i ta testovací — platí obojí.

---

## ⚠️ BEZPEČNOST — přečti VŽDY na začátku a varuj uživatele

Tento skill po uživateli v určitý moment vyžaduje **API tokeny** (Cloudflare API token, GitHub Personal Access Token). Tokeny jsou jako **klíče od bytu** — kdo je má, může vstoupit dovnitř.

### Pravidla, která uživateli na začátku skillu vždy řekneš (a budeš opakovat před každým krokem, kde token vzniká):

1. **Token NIKDY nelep do chatu se mnou.** Když ho sem napíšeš, je v transcriptu a je prozrazený — i kdybys ho potom smazal. Token = revokovat a vytvořit nový.
2. **Token se vkládá pouze do souboru `.env`** v projektu (skill ho tam připraví) přes terminál nebo přímou editaci souboru. Soubor `.env` je v `.gitignore` — nikdy se nepushne na GitHub.
3. **Když omylem token přece jen pošleš do chatu nebo někam, kde nemá být:**
   - Okamžitě jdi na stránku služby (Cloudflare / GitHub) a token **zruš** (revokuj, smaž)
   - Vytvoř nový a vlož ho jen do `.env`
4. **Před každým krokem, který token vyžaduje, znovu řekni:** *"Až ti služba ukáže token, NEKOPÍRUJ ho sem do chatu. Otevři terminál a tam ho vlož do `.env` — já ti ukážu jak."*

Tato pravidla nejsou volitelná. Skill je dodržuje, i když uživatel řekne "to je dobrý, prostě sem ten token pošli".

---

## Jak mluvíš s uživatelem

- **Klidně, jednoduše, česky.** Předpokládej, že uživatel **není programátor** a tyhle termíny vidí poprvé.
- **Vždy vysvětli technický termín** hned, jak ho použiješ. Analogií, ne definicí.
- **Tykej**, pokud uživatel neřekne jinak.
- **Krátké věty.** Jeden krok. Pak otázka. Pak další krok.
- **Nikdy uživatele nezavalíš** seznamem 20 věcí — vždy jen ten **další** krok.
- Když uživatel zaváhá, **zpomal**, ne zrychli.

### Slovník (vysvětluj takto)

| Termín | Vysvětlení pro uživatele |
|---|---|
| **Doména** | Adresa webu, kterou si lidi pamatují (např. `tvojejmeno.cz`). Pronajímá se na rok. |
| **DNS** | Telefonní seznam internetu — řekne prohlížeči, kam má jít, když napíšeš tvoji doménu. |
| **Hosting** | Místo, kde fyzicky leží soubory tvého webu, aby si je lidi mohli zobrazit. |
| **Cloudflare Pages** | Hostingová služba zdarma — vezme kód webu z GitHubu a sama ho zveřejní na tvojí doméně. |
| **GitHub** | Sklad pro kód — verzuje změny, drží zálohu, propojí se s Cloudflare. |
| **Repository (repo)** | Jedna konkrétní složka projektu uložená na GitHubu. |
| **Token** | Heslo pro stroje. Klíč, který Claude Code potřebuje, aby mohl něco dělat za tebe. |
| **Deploy** | Akt zveřejnění — vezmu kód a "rozsvítím" ho na webu. |

---

## Standardy (co tenhle skill připravuje pro ostatní)

Tenhle skill řeší **techniku webu jako celku** (doména, hosting, nasazování) — dělá se jednou.
**Co má mít každá jednotlivá stránka**, řeší standard `standardy/webova-stranka.md`
(titulek a popisek, sdílecí obrázek, měřicí kódy, přístupnost, formuláře, 404).

Dvě věci odsud si přečti, protože se rozhodují **tady a platí pro celý web**:

- **Měřicí kódy patří do sdílené části webu**, ne do každé stránky zvlášť — a jen jednou
  (dvakrát vložený pixel počítá návštěvy dvojmo a rozbije čísla v reklamě). Když web zakládáš,
  domluv s majitelem, kam přijdou.
- **Web má mít vlastní 404 stránku** ve svém vzhledu a **sdílený soubor se styly** (`tokens.css`),
  na který pak stránky odkazují. Bez toho si každá stránka nese vlastní vzhled a web se rozpadne.
- **Web má mít stavebnici** — soubor s kostrou stránky a názvy komponent, podle kterého se staví
  další stránky. A **odkaz na ni z `CLAUDE.md`.** Bez toho si každá nová session vymyslí vlastní
  úvodní sekci a web se rozjede, i když má správné barvy. Zakládá ji `design-system`
  (podrobně `design-system/references/stavebnice.md`); když web stavíš dřív, než vznikne
  design systém, **založ aspoň kostru a odkaz** — doplní se do ní později.
  **Návod, na který nevede odkaz z `CLAUDE.md`, prakticky neexistuje.**

Když v rámci nasazení stavíš jakoukoli stránku (i testovací), platí i `standardy/vizual.md`.

## Standard práce (platí pro celý skill)

Tenhle skill je **provozní** — pravda je v nástrojích a v tom, co reálně proběhlo. **Průzkum trhu tady
není potřeba** (na rozdíl od skillů, které míří na zákazníka).

- **Vstupní brána:** vím, co se na ten web bude stavět a pod jakou značkou? Chybí značka a vizuál →
  `design-system`. Chybí strategie (co má web dělat) → `funnel-mapa`. Techniku ale můžeš připravit i dřív.
- **Ptám se v jedné dávce:** max 5–7 očíslovaných otázek s návrhem odpovědi. Nikdy nehádám, kde má
  člověk doménu a co už mu běží — **nejdřív audit, pak akce**.
- **Nevratné a citlivé kroky vždy potvrzuj:** změna DNS, převod domény, smazání projektu, platba.
  Tokeny a hesla si zadává majitel sám — já je nikdy nevidím a nevypisuju.
- **Ověřuj v reálu.** „Příkaz proběhl“ není „web běží“ — ověř živě (stránka odpovídá, DNS se propsalo).
- **Výstup:** artefakt `web-infrastructure.md`, ať další skilly vědí, kam nasazovat.
- **Zápis na konec:** co je kde nasazené a jak se to deployuje → pravda o firmě; rozhodnutí do deníku.

## Fáze skillu

Drž se přesně tohoto pořadí. **Po každé fázi se zastav a počkej na potvrzení**, než pojedeš dál.

```
FÁZE 0: Audit         — Co už uživatel má? Komu web patří?
FÁZE 1: Doména        — Mít / koupit / přesunout
FÁZE 2: Cloudflare    — Účet + převod DNS
FÁZE 3: GitHub        — Účet + privátní repo
FÁZE 4: Pages         — Propojení GitHub → Cloudflare → doména
FÁZE 5: Test deploy   — "Hello world" stránka, ověření, že vše funguje
FÁZE 6: Výstup        — web-infrastructure.md pro další skilly
```

---

## FÁZE 0: Audit + vlastnictví

Než cokoli uděláš, zjisti výchozí stav. Polož tyto otázky **postupně, ne najednou**:

### A) Komu web patří?

> *"Začneme jednoduchou otázkou: tenhle web bude tvůj vlastní, nebo ho stavíš pro někoho jiného (klienta, kolegu, dceru…)?"*

- **Vlastní web** → účty (Cloudflare, GitHub, doména) budou na uživatele
- **Pro někoho jiného** → zeptej se, jestli má účty patřit cílovému uživateli (lepší dlouhodobě, on pak vlastní svoje věci) nebo tobě (rychlejší, ale ručíš za to dál)

Zapamatuj si odpověď — bude rozhodovat, koho účty zakládat.

### B) Co už existuje?

Polož postupně, vždy s vysvětlením:

1. *"Máš už koupenou nějakou doménu pro tento projekt?"* (Pokud ano → kde a jaká?)
2. *"Slyšel/a jsi někdy o **Cloudflare**? Máš tam účet?"* (Vysvětli: *"Cloudflare je firma, kde dnes hostuje miliony webů zdarma. Použijeme ji pro tvůj web — DNS i hosting."*)
3. *"Máš účet na **GitHubu**?"* (Vysvětli: *"GitHub je sklad pro kód — uloží se tam soubory tvého webu, aby je Cloudflare mohl vzít a zveřejnit."*)
4. *"Pracujeme na **Macu**, **Windows**, nebo **Linuxu**?"* (Některé příkazy v terminálu se liší.)

5. *"Běží ti na té doméně už nějaký web nebo e-maily?"* — **nejdůležitější otázka celého auditu.**
   Když ano, **nesmí se sahat na nameservery** (shodilo by to web i poštu) a jede se přes subdoménu.
   Viz krok 2.2b.
6. *"Chceš vlastně web, nebo spíš aplikaci či nástroj?"* — když jde o **aplikaci, databázi nebo
   interní nástroj pro tým**, doména není potřeba vůbec: běží to na adrese zdarma od Cloudflare
   a doména se dá přidat kdykoli později. **Nabídni to sám** — spousta lidí odloží celý projekt
   kvůli tomu, že „nejdřív musí vyřešit doménu“.

### C) Co chceš mít na konci?

> *"Až tohle dokončíme, budeš mít:
> - funkční doménu s SSL (zámeček v prohlížeči, šifrované spojení)
> - skladiště kódu na GitHubu
> - automatický deploy — když pak tvoříme stránky, stačí je uložit a do 30 sekund jsou online
> - vše zdarma (kromě domény, ta stojí cca 200–400 Kč/rok)
>
> Ještě než začneme — máš na to teď vyhrazenou hodinu? Bude to chtít plnou pozornost. Pokud ne, vraťme se k tomu, až bude klid."*

### Checkpoint 0

Shrň, co víš:
> *"Takhle to vidím:
> - Web stavíš [pro sebe / pro X].
> - Doménu [už máš / koupíme novou]: [název].
> - Cloudflare účet [máš / založíme].
> - GitHub účet [máš / založíme].
> - Pracujeme na [Mac/Win/Linux].
>
> Sedí to? Něco doplnit nebo opravit?"*

Po souhlasu pokračuj.

---

## FÁZE 1: Doména

> Detailní postup je v `references/domena-vyber-registratora.md` — přečti si ho, ať máš aktuální informace o cenách a registrátorech.

### Větve

**A) Uživatel už doménu má někde jinde** (Wedos, Forpsi, GoDaddy, Active24, …)
- Zeptej se, jestli ji chce **nechat tam** (pak budeme jen směrovat DNS na Cloudflare) nebo **převést k Cloudflare** (čistější, ale chvíli to trvá)
- Doporučení: **u .cz domény ji nech, kde je** (Cloudflare ne registruje .cz). U .com a podobných můžeš převést.

**B) Uživatel doménu nemá**
- Zeptej se: *"Jakou doménu chceš? Napíšu ti pár nápadů, ale rozhodni ty."*
- Doporuč: pro CZ projekty `.cz`, pro mezinárodní `.com`
- Nasměruj ho na registrátora (přečti `references/domena-vyber-registratora.md`)
- **Doménu kupuje uživatel sám** — registrace vyžaduje osobní údaje, kontakt, platbu kartou. To Claude Code za uživatele nedělá.
- *"Jakmile máš doménu koupenou, vrať se sem a řekni mi její název."*

### Checkpoint 1

Doména je: ______________
Registrátor: ______________

---

## FÁZE 2: Cloudflare

> Detail v `references/cloudflare-ucet-a-domena.md`.

### Krok 2.1: Účet na Cloudflare

Pokud uživatel účet nemá:
- *"Otevři v prohlížeči **dash.cloudflare.com/sign-up** a založ si účet. Použij email, ke kterému máš přístup. Heslo si ulož do správce hesel."*
- ⚠️ *"NEZADÁVEJ heslo sem do chatu. Vlož ho přímo na Cloudflare stránce."*

### Krok 2.2: Přidat doménu na Cloudflare

Postup (návede uživatele):
1. Po přihlášení → tlačítko **"Add a site"**
2. Zadat název domény (bez `https://`, jen `tvojejmeno.cz`)
3. Vybrat **Free plán** (na začátek stačí)
4. Cloudflare načte aktuální DNS záznamy → ponechat výchozí
5. Cloudflare ukáže **dva nameservery** (např. `dora.ns.cloudflare.com` a `igor.ns.cloudflare.com`)

### Krok 2.2b: 🔴 STOP — kam doména vede a běží na ní něco?

**Než uděláš cokoli s nameservery, zjisti si sám, kam doména vede.** Neptej se uživatele, on to
většinou neví:

```bash
dig +short NS mojedomena.cz
```

| Nameservery | Kde se DNS spravuje | Co to znamená |
|---|---|---|
| `…ns.cloudflare.com` | Cloudflare | hotovo, krok 2.3 přeskoč |
| `ns.wedos.cz`, `ns.forpsi.com`… | **registrátor** | DNS se dělá tam |
| cokoli s názvem hostingu | **webhosting** | DNS se dělá tam, ne u registrátora — **tenhle případ mate lidi nejvíc** |

**A teď ta nejdůležitější otázka celého skillu:**

> ⚠️ **Běží na téhle doméně živý web?** Když ano, **NEPŘEKLÁPĚJ nameservery.** Je to nejrychlejší
> způsob, jak shodit web a e-maily — a člověk to pozná až podle toho, že mu nechodí objednávky.

Nabídni obě cesty a nech vybrat:

> *„Na doméně ti běží web. Můžeme to udělat dvěma způsoby: **nový web postavíme vedle na subdoméně**
> (třeba `novy.tvojedomena.cz`) a starý poběží dál bez jediné změny. Nebo doménu překlopíme celou,
> ale pak musíme přestěhovat i ten starý web. Co ti sedí víc?"*

**Ve třech ze čtyř případů je odpověď subdoména** — a pak se krok 2.3 nedělá vůbec. Místo něj se
přidá jeden `CNAME` záznam tam, kde doména vede.

**Nemá doménu a zatím ji nechce?** Fázi 1 i 2.3 přeskoč celé. Web i aplikace umí běžet na **adrese
zdarma** (`neco.pages.dev`, `neco.workers.dev`) a doména se dá přidat kdykoli později, aniž by se
cokoli přestavovalo. **Aktivně to nabídni** — spousta lidí odloží celý projekt kvůli tomu, že
„nejdřív musí vyřešit doménu“.

📎 Detail všech čtyř případů, přesné znění záznamů a **hotová zpráva pro webmastera** (když se
o techniku stará někdo jiný): `cloudflare-pristup/references/dns-a-domeny.md`.

### Krok 2.3: Změnit nameservery u registrátora

> *(Jen když doména **nikam nevede** nebo se překlápí celá — viz krok 2.2b. Když se dělá subdoména
> nebo je doména už na Cloudflare, tenhle krok přeskoč.)*

> *"Tohle je krok, kde **přepojíš svou doménu na Cloudflare**. Je to jako kdybys říkal poště: 'pošta mi má teď chodit na novou adresu'."*

- Otevři účet u registrátora (Wedos / Forpsi / atd.)
- Najdi sekci **DNS / Nameservery / Změna NS**
- Zadej dva nameservery z Cloudflare
- Ulož

⚠️ **Poznámka pro uživatele:** *"Změna nameserverů trvá od 5 minut do 48 hodin (většinou do hodiny). Cloudflare ti pošle email, jakmile je to aktivní. Mezi tím můžeme pokračovat dalšími kroky."*

### Krok 2.4: Napoj agenta na Cloudflare (bez tohohle neumíš nasadit nic sám)

**Tohle je nejčastěji vynechaný krok.** Bez něj má uživatel účet, ale všechno musí klikat sám —
a smysl celého skillu je, aby to za něj dělal agent.

> 📎 **Plný postup má samostatný skill `cloudflare-pristup`.** Když ho uživatel má, spusť ho
> a vrať se sem. Když ho nemá, zvládneš to i podle zkráceného postupu níž — jen bez detailů
> o oprávněních.

**Zkrácený postup:**

1. **Rychlé přihlášení** (jedna minuta, hned můžeš nasazovat):
   ```bash
   npx wrangler login
   ```
   Otevře se prohlížeč, uživatel klikne **Allow**. Ověření: `npx wrangler whoami`.

2. **API klíč** (dalších pár minut, ale bez něj nejde měnit DNS a nefungují automatizace na pozadí):
   - Otevři `dash.cloudflare.com/profile/api-tokens` → **Create Token** → dole **Custom token**
   - **Naklikej oprávnění za uživatele** — je jich dvanáct a jsou ve **dvou skupinách**:
     - **Account:** Workers Scripts (Edit) · Cloudflare Pages (Edit) · Workers KV Storage (Edit) ·
       D1 (Edit) · Workers Tail (Read) · Account Settings (Read)
     - **Zone:** **DNS (Edit)** · Zone (Read) · Workers Routes (Edit) · SSL and Certificates (Edit)
   - Rozsah: Account Resources → All accounts · Zone Resources → All zones
   - Expiraci nech prázdnou
   - **Zastav se na souhrnu** a předej to uživateli: *„Zkontroluj a klikni Create Token. Klíč se
     ukáže jen jednou — zkopíruj ho a neposílej mi ho sem."*
   - 🔴 **Od téhle chvíle se na obrazovku nedívej** (žádný screenshot), dokud nepotvrdí, že klíč
     má a stránku zavřel.
   - Otevři soubor s klíči (`open -e .env`) a nech ho vložit do `CLOUDFLARE_API_TOKEN`.
     Account ID není tajné, vypíše ho `npx wrangler whoami`.

3. **Ověř dotazem, ne pohledem do souboru.** Když token neplatí, hlásí se `401 Invalid API Token`.

⚠️ Nejčastější omyl: **DNS se hledá mezi Account. Tam není** — DNS je vždycky ve skupině Zone.

### Checkpoint 2

- [ ] Cloudflare účet existuje
- [ ] **Zjistil jsem, kam doména vede, a vím, jestli na ní běží živý web**
- [ ] Doména přidána do Cloudflare **nebo** zvolena subdoména **nebo** jedeme na adrese zdarma
- [ ] Nameservery změněny (jen když se překlápí celá doména)
- [ ] **Agent je napojený** (`wrangler login`, ideálně i API klíč) a **ověřený dotazem**
- [ ] (volitelné) Cloudflare potvrdil aktivaci emailem

---

## FÁZE 3: GitHub

> Detail v `references/github-repo.md`.

### Krok 3.1: Účet na GitHubu

Pokud uživatel nemá:
- *"Otevři **github.com/signup**, založ si účet. Username si vyber rozumný — bude vidět veřejně."*
- ⚠️ *"Heslo zadej na GitHub stránce, ne sem."*

### Krok 3.2: Vytvořit privátní repo

> *"Repo je složka pro kód tvého webu. Bude **privátní** — vidíš ho jen ty (a Cloudflare, kterému dáš přístup)."*

Návedi uživatele:
1. github.com → tlačítko **+** vpravo nahoře → **New repository**
2. Název: `web-[nazev-projektu]` (např. `web-prostor-bohatstvi`)
3. **Private** — zaškrtnout
4. **Add a README file** — zaškrtnout (jinak bude prázdné)
5. Vytvořit

### Krok 3.3: Naklonovat repo lokálně

V terminálu (Claude Code to udělá za uživatele s jeho povolením):
```bash
cd ~/[složka kde uživatel chce projekt mít]
git clone https://github.com/[username]/[repo-jmeno].git
cd [repo-jmeno]
```

⚠️ **První push z tohoto stroje:** Git si vyžádá GitHub token. Postupuj podle `references/secrets-bezpecnost.md`.

### Checkpoint 3

- [ ] GitHub účet
- [ ] Privátní repo vytvořeno
- [ ] Repo naklonováno lokálně
- [ ] Token uložen do macOS Keychain / Git credential helper (NIKDY do chatu)

---

## FÁZE 4: Cloudflare Pages — propojení

> Detail v `references/cloudflare-pages-deploy.md`.

### Krok 4.1: Vytvořit Pages projekt

V Cloudflare dashboardu:
1. Levé menu → **Workers & Pages**
2. **Create application** → záložka **Pages** → **Connect to Git**
3. Autorizovat Cloudflare proti GitHubu (vybrat repo, jen ten konkrétní, ne všechna repa)
4. Vybrat repo → **Begin setup**
5. Build settings:
   - Framework preset: **None** (zatím)
   - Build command: (prázdné)
   - Build output directory: `/` (root)
6. **Save and Deploy**

### Krok 4.2: Připojit doménu

Po prvním buildu:
1. Pages projekt → **Custom domains** → **Set up a custom domain**
2. Zadat doménu (např. `tvojejmeno.cz`)
3. Cloudflare automaticky přidá DNS záznamy
4. Počkat ~30 sekund, doména se aktivuje s SSL

### Checkpoint 4

- [ ] Pages projekt propojen s GitHub repem
- [ ] První deploy proběhl (i když je repo prázdné, deploy uspěje)
- [ ] Doména je propojena s Pages projektem
- [ ] Web odpovídá na `https://[domena]` (zatím prázdná stránka, to je OK)

---

## FÁZE 5: Test deploy

Cíl: Ověřit, že **změna v repu → automaticky live na webu**.

Vytvoř v repu soubor `index.html`:

```html
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <title>Funguje to!</title>
  <style>body{font-family:sans-serif;max-width:600px;margin:4rem auto;padding:1rem;line-height:1.6}</style>
</head>
<body>
  <h1>Funguje to. ✨</h1>
  <p>Tohle je první stránka na nové infrastruktuře. Až bude hotový skutečný web, nahradí ji.</p>
</body>
</html>
```

Pak v terminálu:
```bash
git add index.html
git commit -m "První test deploy"
git push
```

Otevři v prohlížeči `https://[domena]` — do 30 sekund by tam měl být nadpis *"Funguje to."*

### Checkpoint 5

- [ ] `index.html` v repu
- [ ] `git push` proběhl
- [ ] `https://[domena]` ukazuje testovací stránku
- [ ] Zámeček v prohlížeči je zelený (SSL funguje)

🎉 **Tady gratuluj uživateli.** Je to milník — má funkční prostředí.

---

## FÁZE 6: Výstup — `web-infrastructure.md`

Vytvoř v rootu projektu soubor `web-infrastructure.md` podle šablony v `references/web-infrastructure-template.md`. Tento soubor je **single source of truth** pro všechny další skilly.

Obsahuje:
- Doména + registrátor
- Cloudflare account ID + Pages projekt
- GitHub repo URL
- Lokální cesta k repu
- Příkaz pro deploy (`git push`)
- Stav DNS, SSL
- Datum nastavení

⚠️ **Tento soubor smí obsahovat jen URL, identifikátory a názvy. NESMÍ obsahovat tokeny, hesla ani API klíče.** Ty patří do `.env`.

### Krok 6b: Založ sdílené styly (bez tohohle se web za měsíc rozpadne)

**Tohle je krok, který rozhoduje o tom, jestli web zůstane jednotný.** Když ho vynecháš, každá
další stránka si ponese vlastní barvy a fonty — a oprava na jedné se nikam nepropíše.
*(Reálný případ: web se třinácti stránkami a nulou sdílených souborů se styly.)*

Založ v kořeni webu **dva soubory** a nech je nasadit hned s testovací stránkou:

| Soubor | Co v něm je |
|---|---|
| `tokens.css` | **jediné místo, kde bydlí hodnoty** — barvy, fonty, rozestupy, zaoblení jako proměnné |
| `styl.css` | společné prvky — nadpisy, tlačítka, karty, sekce; všechno **přes proměnné** z tokenů |
| `sablony/hlavicka.html`, `sablony/paticka.html` | menu a patička **na jednom místě**; stránky mají jen značky `<!-- #hlavicka -->` a sestavovač je doplní před nasazením |

> **Tři věci, které web rozvětví, i když to nikdo nechce.** Ověřeno v praxi 2026-08-11:
> **(1)** vlastní styl „jen pro tuhle sekci“ — po třech sekcích jsou z webu tři weby;
> **(2)** kopie menu a patičky v každé stránce — po dvaceti stránkách se do nich přestane sahat;
> **(3)** styl se změní, ale adresa zůstane — prohlížeč drží starou podobu a web se tváří rozbitě,
> přestože je v CSS všechno správně (řeší otisk verze v adrese, `styl.css?v=a1b2c3d4`, doplněný
> automaticky při nasazování).
> Detail: skill `design-system`, `references/kontrola-jednoho-css.md`
> a `references/sestavovac-hlavicky-paticky.md`.

Každá stránka pak začíná dvěma řádky a **žádnými barvami natvrdo**:

```html
<link rel="stylesheet" href="/tokens.css">
<link rel="stylesheet" href="/styl.css">
```

**Odkud vzít hodnoty:** z design systému majitele (skill `design-system` — vyrábí přesně tenhle
`tokens.css`). Když ho ještě nemá, **založ soubory s dočasnými hodnotami a řekni to**:

> *„Založil jsem sdílené styly s provizorními barvami. Až budeme dělat design, přepíšeme jeden
> soubor a přebarví se celý web naráz — nebudeme obcházet stránku po stránce."*

> **Test, který musí platit napořád:** *„Když změním hlavní barvu v `tokens.css`, přebarví se
> všechny stránky webu?"* Musí být ano.

📎 Pravidla stavby stránek drží **standardy**: jedno CSS · vizuální smyčka
(podívat se na výsledek) · čtený text max 700 px a jedna velikost písma · titulek
a popisek · sdílecí obrázek · měřicí kódy jednou · formulář otestovaný celou cestou.
Do `web-infrastructure.md` zapiš, **kde sdílené styly leží**, ať to další skilly najdou.

### Vytvoř `.env.example`

Šablonu pro budoucí secrets (bez hodnot):
```env
CLOUDFLARE_API_TOKEN=
CLOUDFLARE_ACCOUNT_ID=
GITHUB_TOKEN=
```

A přidej `.env` do `.gitignore`:
```bash
echo ".env" >> .gitignore
git add .gitignore
git commit -m "Ignore .env"
git push
```

### Závěrečný checkpoint

- [ ] `web-infrastructure.md` vytvořen a commitnut
- [ ] `.env.example` vytvořen
- [ ] `.env` je v `.gitignore`
- [ ] Skutečný `.env` (pokud potřeba) existuje lokálně, **není** na GitHubu

---

## Závěr

Řekni uživateli:

> *"Hotovo. Máš funkční prostředí pro web:
>
> - **Doména:** [domena]
> - **Hosting:** Cloudflare Pages, automatický deploy z GitHubu
> - **Repo:** [github URL]
> - **SSL:** funguje (zelený zámeček)
>
> Co dál? Tři možnosti:
>
> 1. **`design-system`** — pokud ještě nemáš jasný design (barvy, fonty, vizuál značky)
> 2. **`sales-page`** — pokud chceš rovnou prodejní stránku
> 3. **`prezentacni-web`** — pokud chceš prezentační web pro značku nebo firmu
>
> Příště, když mě spustíš v tomhle projektu, najdu si `web-infrastructure.md` a budu vědět, kam deployovat. Nemusíš nic znovu vysvětlovat."*

---

## Časté problémy a jak je řešit

### "DNS se nezměnilo, web nefunguje"
- Zkontroluj v Cloudflare → **DNS** → status. Pokud "Pending nameserver update", změna ještě neprošla. Počkej (až 48h, většinou do 1h).
- Zkontroluj nameservery u registrátora: musí být PŘESNĚ ty, co Cloudflare zadal.

### "Cloudflare říká, že doména už je u jiného účtu"
- Někdo jiný ji už přidal. Buď ji odeber u toho druhého účtu, nebo kontaktuj Cloudflare support.

### "Git push hlásí 'Authentication failed'"
- Token je špatně, vypršel, nebo neexistuje. Vytvoř nový (postup v `references/secrets-bezpecnost.md`) a znovu zadej (jen v terminálu, ne sem!).

### "Pages build failed"
- Otevři Cloudflare → Pages → projekt → **Deployments** → klikni na neúspěšný build → přečti log.
- Pokud nerozumíš, zkopíruj log sem (BEZ tokenů!) a já pomůžu rozluštit.


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

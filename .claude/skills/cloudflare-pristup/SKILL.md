---
name: cloudflare-pristup
description: >
  Nastaví majiteli **přístup do Cloudflare** tak, aby jeho agent mohl sám stavět a nasazovat věci
  na internet — weby, stránky, ale i **aplikace, databáze a interní nástroje pro tým**. Provede
  založením účtu zdarma, **naklikané oprávnění připraví agent sám v prohlížeči** (uživatel jen
  potvrdí a vygeneruje klíč, který agent nikdy nevidí), vloží se bezpečně a ověří neškodným dotazem.
  Umí i **rozplést domény a DNS**: zjistí, kam doména vede, a podle toho poradí, jestli se nastavuje
  u registrátora, na webhostingu, nebo v Cloudflare — a když člověk doménu nemá ani nechce, ukáže,
  že aplikace může běžet na adrese zdarma. Spouští se, když uživatel řekne: „napoj mě na Cloudflare“,
  „potřebuju Cloudflare“, „nastav mi přístup do Cloudflare“, „API klíč do Cloudflare“, „chci
  nasazovat weby", „chci si postavit aplikaci online“, „potřebuju databázi online“, „nastav DNS“,
  „udělej subdoménu“, „kde mi běží doména“, „/cloudflare-pristup“. NE pro: výběr a nákup domény
  a stavbu celého webu (to řeší `web-setup`, který si tenhle přístup zavolá), NE pro design stránek.
---

# Skill: Přístup do Cloudflare

**Co to je, jednoduše:** Cloudflare je místo, kde může na internetu bydlet cokoli, co postavíš —
web, stránka, aplikace, databáze, formulář, interní nástroj pro tým. Základ je **zdarma** a vydrží
i dost velkému provozu. Tenhle skill zařídí, aby tam **tvůj agent mohl sám sahat**: postavit,
nasadit, opravit, aniž bys musel klikat.

**Proč to má vlastní skill a není to schované ve stavbě webu:** Cloudflare potřebuješ, i když
žádný web nechceš. Aplikace pro tým, databáze, chytrý formulář, přesměrování odkazů — to všechno
tam běží bez jediné stránky navíc.

**Zlaté pravidlo:**
> **Klíč vytváří člověk, ne agent.** Agent připraví všechno až k poslednímu tlačítku, pak se
> odvrátí. Vygenerovaný klíč nesmí projít jeho očima ani jeho pamětí.

---

## Krok 0: Co potřebuju vědět, než začnu

Zeptej se **v jedné dávce** (a u každé otázky nabídni tip, ať stačí odpovědět „ano“):

1. **Máš už účet na Cloudflare?** (Nevíš? Zkus se přihlásit e-mailem, který používáš k podnikání.)
2. **Co chceš stavět?** web nebo stránku · aplikaci či nástroj pro tým · databázi · zatím nevím
3. **Máš doménu?** Ano (jakou) · mám, ale běží na ní web, kterého se nechci dotknout · nemám
   a zatím nechci
4. **Máš na téhle doméně živý web, který musí dál fungovat?** *(Nejdůležitější otázka. Podle ní
   se rozhoduje, jestli se sahá na celou doménu, nebo jen na subdoménu.)*

Když má doménu, **zjisti si sám, kam vede** (viz `references/dns-a-domeny.md`) — ušetříš mu
polovinu vysvětlování.

---

## FÁZE 1: Účet (dělá uživatel, trvá dvě minuty)

**Nemá účet:**
> *„Otevři si `dash.cloudflare.com/sign-up` a založ účet. Použij e-mail, ke kterému máš přístup.
> Heslo si ulož do správce hesel. Vyber plán **Free** — na všechno, co budeme dělat, stačí."*

⚠️ **Heslo ani nic dalšího mi sem neposílej.** Zadáváš to jen na stránce Cloudflare.

**Má účet:** ať se přihlásí a napíše, že je uvnitř. Pak pokračuj fází 2.

---

## FÁZE 2: Rychlé přihlášení agenta (wrangler)

`wrangler` je nástroj, kterým agent s Cloudflare mluví. **Přihlášení přes něj je otázka jedné
minuty** a hned potom umí agent nasazovat.

```bash
npx wrangler login
```

Otevře se prohlížeč, uživatel klikne **Allow**, hotovo. Ověření: `npx wrangler whoami`.

**Proč to nestačí a děláme ještě API klíč:**

| | přihlášení přes `wrangler` | API klíč |
|---|---|---|
| Nastavení | 1 minuta, jeden klik | 5–10 minut, klikání oprávnění |
| Nasazování webů a aplikací | ✅ | ✅ |
| **Změna DNS záznamů** | ❌ **neumí** (má na domény jen čtení) | ✅ |
| **Automatizace na pozadí** (noční úlohy, hlídače) | ❌ nespolehlivé, přihlášení vyprší | ✅ drží |

Takže: **wrangler na rozjezd a interaktivní práci, API klíč na DNS a na všechno, co má běžet samo.**
U člověka, který chce jen zkusit, jak to chodí, se dá u wrangleru zůstat a klíč dodělat později —
ale **řekni mu, co tím zatím nemá.**

---

## FÁZE 3: API klíč (tohle je ta část, kde lidi tápou)

Zaklikat správná oprávnění je nejotravnější krok celého nastavení: **oprávnění jsou ve dvou
oddělených skupinách** (účet zvlášť, domény zvlášť), je jich přes sto a jmenují se podobně.
Proto to **naklikej za uživatele.**

### 3.1 Otevři stránku a naklikej oprávnění

Přes agentní prohlížeč (skill `agentni-prohlizec`, kde je uživatel přihlášený):

1. Otevři `dash.cloudflare.com/profile/api-tokens`
2. **Create Token** → dole **Custom token** → **Get started**
3. Pojmenuj token, ať se pozná: `agent-<jméno>`
4. **Naklikej oprávnění** podle `references/opravneni-tokenu.md` — je jich 12 a jsou ve **dvou
   skupinách**, což je přesně to, co lidi mate:
   - **Account** (věci účtu: aplikace, databáze, stránky)
   - **Zone** (věci domén: DNS, směrování, certifikáty)
5. Nastav **Account Resources** a **Zone Resources** (které účty a domény token uvidí)
6. **Token nechej bez data expirace**, pole na omezení podle IP nech prázdné
7. **Zastav se na stránce se souhrnem.** Nemačkej nic dalšího.

### 3.2 Předej to uživateli a odvrať se

> *„Máš to připravené na obrazovce. Zkontroluj souhrn a klikni **Continue to summary**
> → **Create Token**. Ukáže se ti klíč — **nekopíruj ho sem do chatu.** Zkopíruj ho a za chvíli
> ti otevřu soubor, kam ho vložíš."*

🔴 **Od téhle chvíle se agent na obrazovku nedívá.** Žádný screenshot, žádné čtení stránky,
dokud uživatel nepotvrdí, že klíč má zkopírovaný a stránku zavřel. Klíč se zobrazí **jen jednou**
a nesmí projít agentem.

### 3.3 Vložení klíče

Otevři soubor s klíči v textovém editoru a nech ho vložit:

```
CLOUDFLARE_API_TOKEN=
CLOUDFLARE_ACCOUNT_ID=
```

**Account ID není tajné** — najdeš ho sám (`npx wrangler whoami` ho vypíše) a můžeš mu ho rovnou
napsat, ať ho nehledá. **Token ale nikdy nečti, nevypisuj a neopakuj.**

⚠️ **Na soubor s klíči nikdy nesahej nástroji na čtení a psaní souborů.** Kostru řádků zakládej
přes příkazovou řádku, hodnoty doplňuje uživatel v editoru. Když už soubor existuje, jen ho otevři.

---

## FÁZE 4: Ověření (a tady se pozná, že to opravdu funguje)

Ověřuj **dotazem, ne pohledem do souboru.** Neškodný test, který nic nemění:

- token platí a je aktivní,
- kolik domén vidí a kterých,
- funguje účet (vypíše se, co v něm je).

Vzorový ověřovací skript: `references/overeni.md`. **Hodnota klíče se v žádném výstupu neobjeví.**

Když je token neplatný, ohlásí se to jako `401 Invalid API Token` — pak se vrací do fáze 3
(nejčastěji se nezkopíroval celý, nebo se zapomněl uložit soubor).

---

## FÁZE 5: Řekni, co teď agent umí

Tohle nepřeskakuj. Uživatel právě něco nastavil a **potřebuje vědět, co za to dostal.** Lidsky:

- **postavit a nasadit web nebo stránku** (a hned mu ukázat adresu),
- **udělat subdoménu** a nasměrovat ji, kam je potřeba,
- **postavit aplikaci nebo nástroj pro tým** — běží na adrese zdarma, doména není potřeba,
- **založit databázi** pro objednávky, kontakty, cokoli,
- **přesměrovat odkazy**, chytat data z formulářů,
- **opravovat to všechno bez klikání**, na slovo.

A dodej **jeden konkrétní další krok**: *„Chceš, abych rovnou postavil zkušební stránku, ať vidíš,
že to celé funguje?"*

---

## Domény a DNS (nejčastější zádrhel)

**Nikdy nepředpokládej, že se má celá doména překlopit na Cloudflare.** Když na ní běží živý web,
je to nejrychlejší způsob, jak ho shodit.

Postup: **zjisti, kam doména vede** (nameservery umí agent přečíst sám), a podle toho se rozhodni:

| Kam doména vede | Kde se nastavuje DNS | Co udělat |
|---|---|---|
| **na Cloudflare** | v Cloudflare | agent to zvládne sám (s API klíčem) |
| **na registrátora** (Wedos, Forpsi…) | u registrátora | navést uživatele na přihlášení, nebo mu dát hotové záznamy |
| **na webhosting** | na webhostingu | totéž — a tohle je případ, který lidi mate nejvíc |
| **nemá doménu / nechce ji** | — | aplikace poběží na **adrese zdarma** od Cloudflare |

A tři cesty, jak záznamy vzniknou: **uživatel si je nastaví sám** podle přesného zadání ·
**pustí agenta** do svého účtu přes agentní prohlížeč · **pošle je webmasterovi** (agent napíše
hotovou zprávu, stačí přeposlat).

**Chce zkusit web, ale na doméně mu běží starý?** Nabídni **subdoménu** (`novy.jehodomena.cz`) —
starý web běží dál nedotčený a nový vzniká vedle. Detail i s hotovou zprávou pro webmastera:
`references/dns-a-domeny.md`.

---

## Bezpečnost (nepřekročitelné)

- **Klíč negeneruje agent.** Připraví oprávnění, pak se odvrátí.
- **Klíč se nikdy nečte, nevypisuje, neopakuje ani neukládá** jinam než do souboru s klíči.
- **Do chatu klíč nepatří.** Když ho tam uživatel přesto pošle, upozorni ho, že je tím prozrazený,
  a **nech ho ho zneplatnit** v Cloudflare a vytvořit nový.
- **Nejmenší možná oprávnění.** Když člověk chce jen stránky, nedávej mu práva na mazání databází.
- **Klíč do zálohy a do sdílených souborů nikdy.**

---

## Checklist před „hotovo“

- [ ] Účet existuje a uživatel je přihlášený
- [ ] Vím, **co chce stavět** — a podle toho jsem zvolil rozsah oprávnění
- [ ] Když má doménu: **zjistil jsem, kam vede**, a nesahám na živý web bez jeho vědomí
- [ ] Oprávnění jsem **naklikal já**, ne uživatel
- [ ] **Klíč jsem neviděl** — vygeneroval a vložil ho uživatel
- [ ] Token **ověřen dotazem** (ne pohledem do souboru) a vypsáno, kolik domén vidí
- [ ] Account ID je doplněné
- [ ] Uživateli jsem **lidsky řekl, co teď umím**, a nabídl jeden další krok
- [ ] Zapsáno, co je napojené

---

## Na co pozor

- ❌ Nechat uživatele hledat oprávnění samotného → ✅ naklikej to za něj, je jich přes sto
- ❌ Zapomenout, že oprávnění jsou **ve dvou skupinách** (účet a domény) → ✅ projít obě
- ❌ Dívat se na obrazovku, když se generuje klíč → ✅ odvrátit se, klíč vidí jen uživatel
- ❌ Překlopit celou doménu, když na ní běží web → ✅ nejdřív zjistit, kam vede, pak nabídnout subdoménu
- ❌ Ověřovat token přečtením souboru → ✅ ověřovat dotazem, hodnota se nikdy nevypisuje
- ❌ Tvrdit „hotovo“ po uložení souboru → ✅ hotovo je, až dotaz projde
- ❌ Nastavit klíč a neříct, co s ním člověk získal → ✅ fáze 5, lidsky a s dalším krokem
- ❌ Předpokládat, že člověk chce web → ✅ aplikace a databáze fungují i bez domény

---

## Vazby

- **Volá si tenhle skill:** `web-setup` (technika webu) — a má vlastní zkrácenou kopii, aby fungoval
  i samostatně.
- **Používá:** `agentni-prohlizec` (naklikání oprávnění, přihlášení k registrátorovi či webhostingu).
- **Navazuje:** `design-system` (jak to bude vypadat), stránkové skilly (co se na to nasadí).
- **Standardy:** když se v rámci nastavení staví jakákoli stránka (i zkušební), platí standard
  vizuální práce a standard webové stránky.

---

## Reference

| Soubor | Co v něm je |
|---|---|
| `references/opravneni-tokenu.md` | **Přesný seznam oprávnění** k naklikání, rozdělený na účet a domény, včetně toho, co je povinné a co volitelné podle záměru |
| `references/dns-a-domeny.md` | Jak zjistit, kam doména vede · čtyři případy a co v nich dělat · subdomény · **hotová zpráva pro webmastera** |
| `references/overeni.md` | Ověřovací dotaz (token, domény, účet) tak, aby se hodnota klíče nikdy nevypsala |

**Verze 1.0 (2026-08-06).** Vzniklo z majitelova zadání: „ať to lidem zjednodušíme“ — klikání
oprávnění v Cloudflare je pro běžného člověka nejnáročnější část celého nastavení.


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

# Domény a DNS — kam to vede a kde se to nastavuje

> K čemu to je: nejčastější zádrhel při rozjezdu webu není technika, ale **nedorozumění, kde se
> vlastně doména nastavuje.** Člověk jde k tomu, kde doménu kupoval, a tam nic nenajde — protože
> se to spravuje jinde.
> Naposledy ověřeno: 2026-08-06.

---

## Nejdřív zjisti, kam doména vede (agent to umí sám)

**Neptej se uživatele. On to většinou neví, a když odpoví, často špatně.** Zjisti si to:

```bash
dig +short NS mojedomena.cz
```

Vrátí **nameservery** — to je adresa toho, kdo o doméně rozhoduje. Podle nich poznáš všechno další:

| Nameservery vypadají takhle | Znamená to |
|---|---|
| `…ns.cloudflare.com` | doména je **na Cloudflare** |
| `ns.wedos.cz`, `ns.forpsi.com`, `ns.active24.cz` | DNS spravuje **registrátor** |
| `ns.webhostingu…`, `ns.savana.cz`, cokoli s názvem hostingu | DNS spravuje **webhosting** |
| nic se nevrátí | doména neexistuje, nebo je špatně napsaná |

**Registrátor a správce DNS nejsou totéž.** Doménu můžeš mít koupenou u Wedosu, ale nameservery
nasměrované na webhosting — a pak se DNS nastavuje **na tom hostingu, ne u Wedosu.** Přesně tady
lidi bloudí.

Kdo doménu prodal (registrátor) se zjistí přes `whois mojedomena.cz` — hodí se, když člověk neví,
kde má účet.

---

## Čtyři případy a co v nich dělat

### 1. Doména už je na Cloudflare
**Nejjednodušší.** S API klíčem (oprávnění Zone → DNS → Edit) nastaví agent všechno sám.
Řekni, co nastavíš, a udělej to.

### 2. Doména vede na registrátora
DNS se spravuje v účtu registrátora. Tři cesty:
- uživatel se přihlásí a **agent mu dá přesné záznamy** k nastavení,
- uživatel pustí agenta dovnitř přes **agentní prohlížeč** a ten to naklikala,
- záznamy jdou **webmasterovi** (viz hotová zpráva níž).

### 3. Doména vede na webhosting
Totéž jako 2, jen se uživatel přihlašuje na hosting. **Tenhle případ mate nejvíc** — člověk je
přesvědčený, že se to dělá tam, kde doménu kupoval.
Uklidni ho: *„Doménu máš u X, ale rozhoduje o ní Y. Nastavíme to tam a nikde jinde se nic nemění.“*

### 4. Doménu nemá a zatím nechce
**Nic se nekupuje.** Web i aplikace umí běžet na **adrese zdarma od Cloudflare**
(`neco.pages.dev` pro stránky, `neco.workers.dev` pro aplikace). Doména se dá přidat kdykoli
později, aniž by se cokoli přestavovalo.

Tohle **aktivně nabídni** — spousta lidí odloží celý projekt kvůli tomu, že „nejdřív musí vyřešit
doménu".

---

## Když na doméně běží živý web (nejdůležitější situace)

🔴 **Nikdy nepřeklápěj celou doménu na Cloudflare, když na ní běží web.** Je to nejrychlejší
způsob, jak ho shodit — a člověk to pozná až podle toho, že mu nechodí objednávky.

**Zeptej se dřív, než na cokoli sáhneš:**
> *„Na téhle doméně ti běží web. Máme dvě možnosti: nový web postavíme **vedle na subdoméně**
> (třeba `novy.tvojedomena.cz`), starý poběží dál bez jediné změny. Nebo doménu překlopíme celou,
> ale pak musíme přestěhovat i ten starý web. Co chceš?"*

Ve třech ze čtyř případů je odpověď subdoména.

### Jak vzniká subdoména

Když doména **není** na Cloudflare, přidá se u jejího správce jeden záznam:

| Pole | Hodnota |
|---|---|
| Typ | `CNAME` |
| Název / Host | `novy` *(u některých správců se píše celé `novy.tvojedomena.cz`)* |
| Hodnota / Cíl | `nazev-projektu.pages.dev` *(adresu dá Cloudflare při vytvoření projektu)* |
| TTL | automaticky / 3600 |

Pak se subdoména přidá i v Cloudflare u projektu (Custom domain). Naběhne to obvykle do pár minut,
někdy až za pár hodin.

⚠️ **Nesahej na záznamy `A`, `MX` a `TXT` u hlavní domény.** Drží běžící web a e-maily.
Přidává se **jeden nový řádek**, nic se nemaže.

---

## Hotová zpráva pro webmastera (k přeposlání)

Když se o techniku stará někdo jiný, napiš uživateli text, který jen přepošle:

> Ahoj,
> potřebuju u domény **{doména}** přidat jeden DNS záznam pro novou subdoménu. Na stávající web
> ani e-maily to nemá vliv, nic se nemaže, jen se přidává jeden řádek.
>
> - **Typ:** CNAME
> - **Název:** {subdoména, např. `novy`}
> - **Cíl:** {adresa, např. `muj-projekt.pages.dev`}
> - **TTL:** automaticky
> - **Proxy (oranžový mráček), pokud to nabízí:** zapnuto
>
> Až to nastavíš, dej mi prosím vědět. Díky!

**Vždycky doplň konkrétní hodnoty**, ať uživatel nic nedoplňuje sám. A dodej mu jednou větou,
co po webmasterovi chce, kdyby se ptal: *„Přidává se jedna subdoména, starý web běží dál.“*

---

## Časté zádrhely

| Projev | Příčina |
|---|---|
| Nastaveno, ale adresa nefunguje | ještě se to nerozšířilo — počkat (minuty až hodiny), pak `dig +short novy.domena.cz` |
| „Doména už je použitá u jiného účtu“ | doména je přidaná na jiném Cloudflare účtu, nejdřív ji tam odebrat |
| Web se otevře, ale hlásí nebezpečné spojení | certifikát se ještě vyrábí, obvykle do 15 minut |
| Změnili jsme DNS a spadly e-maily | smazal se `MX` záznam — obnovit ze zálohy záznamů, kterou má správce |
| Subdoména vede na starý web | zůstal tam původní `A` záznam se stejným názvem, přebíjí `CNAME` |

**Před každou změnou DNS si vypiš a ulož stávající záznamy.** Když se něco pokazí, je to jediná
cesta zpátky.

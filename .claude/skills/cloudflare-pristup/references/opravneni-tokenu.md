# Oprávnění API tokenu — přesný seznam k naklikání

> K čemu to je: v Cloudflare je přes sto oprávnění, jmenují se podobně a jsou **ve dvou oddělených
> skupinách**. Běžný člověk tady ztrácí čtvrt hodiny a stejně zaklikne špatně. Tenhle seznam
> naklikáš za něj.
> Naposledy ověřeno: 2026-08-06.

---

## Kde to je

`dash.cloudflare.com/profile/api-tokens` → **Create Token** → úplně dole **Custom token** →
**Get started**

*(Nahoře jsou hotové šablony. **Nepoužívej je** — „Edit Cloudflare Workers“ vypadá lákavě, ale nemá
DNS ani stránky, a člověk pak zjistí, že mu půlka věcí nejde.)*

---

## Proč to lidi mate: dvě skupiny, ne jedna

Každý řádek oprávnění má **tři pole**. To první je rozbalovací a rozhoduje o všem:

| První pole | Čeho se to týká | Příklad |
|---|---|---|
| **Account** | věci **účtu** — aplikace, databáze, stránky, úložiště | „smíš zakládat databáze“ |
| **Zone** | věci **domén** — DNS záznamy, směrování, certifikáty | „smíš měnit DNS na mojedomena.cz“ |
| **User** | věci **osoby** (skoro nikdy nepotřeba) | „smíš číst profil“ |

**Skoro každý omyl vzniká tím, že se DNS hledá mezi Account.** Tam není. DNS je vždycky Zone.

Řádek se přidává tlačítkem **+ Add more** pod posledním řádkem.

---

## Základní sada (nastav vždycky)

### Skupina Account

| Oprávnění | Úroveň | K čemu to je |
|---|---|---|
| **Workers Scripts** | Edit | aplikace a nástroje běžící online |
| **Cloudflare Pages** | Edit | weby a stránky |
| **Workers KV Storage** | Edit | rychlé ukládání drobností (nastavení, počítadla) |
| **D1** | Edit | databáze (objednávky, kontakty, obsah) |
| **Workers Tail** | Read | čtení záznamů běhu, když se hledá chyba |
| **Account Settings** | Read | agent zjistí, do jakého účtu patří |

### Skupina Zone

| Oprávnění | Úroveň | K čemu to je |
|---|---|---|
| **DNS** | Edit | **subdomény a nasměrování domény** — bez tohohle agent DNS nezmění |
| **Zone** | Read | agent uvidí, jaké domény v účtu jsou |
| **Workers Routes** | Edit | napojení aplikace na adresu domény |
| **SSL and Certificates** | Edit | zabezpečený zámeček u adresy (https) |

---

## Volitelné (přidej jen podle záměru)

| Oprávnění | Skupina | Kdy to přidat |
|---|---|---|
| **Workers R2 Storage** | Account | budou se ukládat soubory, obrázky, videa |
| **Workers AI** | Account | aplikace bude používat umělou inteligenci |
| **Queues** | Account | zpracování na pozadí (hromadné e-maily, dávky) |
| **Email Routing Addresses** | Account | e-maily na vlastní doméně přeposílané jinam |
| **Cache Purge** | Zone | web se má umět rychle „propláchnout“ po změně |

**Nedávej nic navíc „pro jistotu“.** Klíč je jako klíč od bytu: čím víc dveří otevírá, tím větší
škoda, když se ztratí.

---

## Rozsah (dvě pole pod oprávněními)

**Account Resources**
- `Include` → **All accounts** *(nebo konkrétní účet, když jich má víc a chce oddělit)*

**Zone Resources**
- `Include` → **All zones** — když má domén víc a chce s nimi pracovat
- nebo `Include` → **Specific zone** → vybrat jednu — když chce agenta pustit jen k jedné doméně

💡 **Když jsou účty mezi sebou propojené (sdílené)**, token z hlavního účtu vidí i domény
sdílených účtů. Nemusí se pak dělat klíč pro každý účet zvlášť.

---

## Poslední dvě pole

- **TTL / Start–Expiration date:** nech **prázdné** (bez expirace). Klíč, který za rok tiše
  vyprší, shodí automatizace v nejhorší možnou chvíli.
- **Client IP Address Filtering:** nech **prázdné**.

---

## A tady se agent zastaví

Naklikáno → **zastav se na stránce se souhrnem** a předej to uživateli:

> *„Připravil jsem ti oprávnění. Zkontroluj souhrn, klikni **Continue to summary**
> → **Create Token**. Klíč se ti ukáže **jen jednou** — zkopíruj ho a **neposílej mi ho sem**.
> Hned ti otevřu soubor, kam ho vložíš."*

🔴 **Od téhle chvíle žádný screenshot ani čtení stránky**, dokud uživatel nepotvrdí, že klíč
zkopíroval a stránku zavřel.

---

## Kontrola po vytvoření

Když se pak něco nedaří, projdi tenhle seznam — devět z deseti problémů je tady:

1. **`401 Invalid API Token`** → klíč se nezkopíroval celý, nebo se soubor neuložil.
2. **Nasazení projde, ale DNS nejde** → chybí **Zone → DNS → Edit** (nejčastější omyl, hledalo
   se to mezi Account).
3. **„Nevidím žádné domény“** → chybí **Zone → Zone → Read**, nebo je v Zone Resources vybraná
   jen jedna doména.
4. **Databáze nejde založit** → chybí **Account → D1 → Edit**.
5. **Stránky se nenasadí** → chybí **Account → Cloudflare Pages → Edit**.

Oprava se dělá **úpravou existujícího tokenu** (Edit u tokenu v seznamu), ne vytvářením nového —
při úpravě se klíč nemění a nemusí se znovu vkládat.

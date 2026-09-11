# Doména — výběr a registrátor

> **Tento soubor je pro skill (Claude Code) i uživatele.** Pomáhá rozhodnout, jakou doménu si pořídit a kde.

---

## Co je doména a jak vybrat název

**Doména** je adresa webu, kterou si lidi pamatují (`tvojejmeno.cz`). Pronajímá se na 1+ rok od **registrátora**.

### Pravidla pro dobrý název

- **Krátká** — ideálně 5–12 znaků
- **Vyslovitelná** — když ji řekneš nahlas, druhý člověk ji napíše správně
- **Bez pomlček a čísel**, pokud možno (snižují důvěryhodnost a hůř se diktují)
- **Bez ohraných fráz** (`super`, `best`, `online`)
- **Pravopis bez háčků** — `tvurce.cz` jde, `tvůrce.cz` taky funguje (IDN), ale lidi to neumí napsat

### Která koncovka?

| Koncovka | Kdy použít |
|---|---|
| `.cz` | Český projekt, česká cílovka. Důvěra v ČR/SR. |
| `.com` | Mezinárodní projekt, anglicky mluvící cílovka. |
| `.eu` | Méně časté, bez výhody nad .cz/.com. |
| `.online`, `.shop`, `.io` | Drahé, někdy "trendy", ale lidi je hůř pamatují. |
| `.sk` | Slovenský projekt. |

**Doporučení:** pro projekt zaměřený na CZ/SK → `.cz`. Pro mezinárodní → `.com`.

---

## Kde doménu koupit (registrátor)

### Pro `.cz` doménu

| Registrátor | Cena/rok (orientačně) | Plusy | Mínusy |
|---|---|---|---|
| **Wedos** | ~150 Kč | Levné, rozumný panel, česká podpora | UI je stará škola |
| **Forpsi** | ~250 Kč | Rozšířený, stabilní | Dražší |
| **Active 24** | ~250 Kč | Hodně rozšířený, integrace | Dražší |
| **Subreg** | ~150 Kč | Velký výběr koncovek | UI hutné |

⚠️ **Cloudflare Registrar `.cz` doménu NEPRODÁVÁ.** Pro .cz se musíš zaregistrovat u CZ registrátora (Wedos, Forpsi atd.) — to je jenom úvodní krok, pak doménu **napojíme přes DNS na Cloudflare** (nameservery), takže výhody Cloudflare máme i tak.

**Doporučení:** Wedos pro nejnižší cenu. Forpsi/Active24 pokud chceš zaběhnutý zavedený firmu.

### Pro `.com` doménu

| Registrátor | Cena/rok | Plusy | Mínusy |
|---|---|---|---|
| **Cloudflare Registrar** | ~9 USD (~210 Kč) | **Bez marže** — dáváš jen velkoobchodní cenu. Vše v jednom místě s hostingem. | Jen vybrané koncovky. |
| **Namecheap** | ~10 USD | Široký výběr, dobré UI | Trochu dražší |
| **Wedos / Forpsi** | ~250–350 Kč | Česká podpora | Dražší |

**Doporučení pro `.com`:** **Cloudflare Registrar** — nejlevnější a vše v jednom místě (registrace + DNS + hosting). Pokud klient ještě nemá Cloudflare účet, založíme ho ve fázi 2 a teprve potom může koupit doménu přes Cloudflare.

### Pořadí pro .com doménu přes Cloudflare

1. Nejdřív Fáze 2 (založ Cloudflare účet)
2. Pak v Cloudflare → **Domain Registration** → najdi doménu, kup
3. Doména je hned napojená — nemusíš měnit nameservery, doména už *je* na Cloudflare

(Tohle pořadí se liší od situace, kdy už doménu máš jinde. Tam je to: registrátor existuje → přidat doménu do Cloudflare → změnit nameservery → propojit Pages.)

---

## Co když uživatel doménu už má?

Zjisti:
- **Kde je registrovaná?** (Wedos, Forpsi, GoDaddy, jiný registrátor)
- **Kdy končí registrace?** Pokud do 30 dní → nejdřív obnovit, pak řešit setup.
- **Má přístup k účtu u registrátora?** Bez toho nelze změnit nameservery.

### Možnosti

**A) Nechat doménu u stávajícího registrátora**
- Cloudflare bude jen DNS + hosting
- Stačí změnit nameservery (Fáze 2 v hlavním skillu)
- ✅ Doporučeno pro `.cz` domény

**B) Přesunout doménu k Cloudflare Registrar**
- Funguje pro `.com` a vybrané jiné koncovky (NE `.cz`)
- Trvá 5–7 dní, vyžaduje **EPP / authorization kód** od stávajícího registrátora
- ✅ Stojí za to dlouhodobě (bez marže, vše v jednom)
- ❌ Komplikovanější — udělej až po dokončení základního setupu, ne během

---

## Před nákupem zkontroluj

- [ ] Doména je volná (ověř na stránce registrátora)
- [ ] **Whois privacy** je zapnutá (skryje tvoje osobní údaje, většinou zdarma nebo za pár Kč)
- [ ] **Auto-renew** je zapnuté (jinak ti doména po roce vyprší a někdo ji koupí)
- [ ] Email u registrátora je email, na který opravdu chodíš (notifikace o vypršení, transferech atd.)

---

## Co Claude Code za uživatele NEDĚLÁ

- ❌ **Nákup domény** — vyžaduje osobní údaje, kontaktní informace, platbu kartou
- ❌ **Vyplnění whois** — osobní údaje
- ❌ **Platbu** — platba kartou patří jen do rukou uživatele

Claude Code **provede uživatele krok za krokem** procesem, vysvětlí každé pole, a počká, až uživatel registraci dokončí v prohlížeči.

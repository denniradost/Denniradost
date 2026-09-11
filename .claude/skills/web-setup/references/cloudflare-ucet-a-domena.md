# Cloudflare — účet a doména

> Jak založit Cloudflare účet a propojit existující doménu (změnou nameserverů).

---

## Proč Cloudflare?

Cloudflare je největší DNS a CDN provider na světě. Pro nás dělá tři věci:

1. **DNS** — řídí, kam směřuje doména (`tvojejmeno.cz` → server, kde leží web)
2. **Hosting** přes Cloudflare Pages — místo, kde fyzicky web běží
3. **SSL** — šifrovaný zámeček v prohlížeči (zdarma, automaticky)

Vše **zdarma** v základu. Free plán pokryje 99 % případů malého/středního webu.

---

## Krok 1: Založení účtu

1. Otevři [dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)
2. **Email** + **heslo** (heslo vlož do správce hesel — 1Password / Bitwarden / Apple Heslo)
3. Klikni **Sign up**
4. Cloudflare ti pošle ověřovací email — klikni v něm na link
5. Po ověření tě přesměruje na dashboard

⚠️ **Heslo NIKDY nepiš do chatu se mnou** (Claude Code). Vlož ho přímo do Cloudflare formuláře.

### Doporučené nastavení účtu po prvním přihlášení

1. **Two-Factor Authentication (2FA)** — zapni hned. Profil ikona vpravo nahoře → My Profile → Authentication → 2FA. Ulož backup kódy do správce hesel.
2. **Recovery email** — nastav druhý email pro případ ztráty přístupu.

---

## Krok 2: Přidání domény do Cloudflare

> Tento krok platí, **pokud máš doménu jinde** (Wedos, Forpsi, atd.). Pokud kupuješ doménu rovnou přes Cloudflare Registrar (jen `.com` a další koncovky, ne `.cz`), tento krok přeskoč — doména je hned v Cloudflare.

### Postup

1. V dashboardu klikni **+ Add site** (vpravo nahoře)
2. Zadej doménu **bez `https://` a `www`**, jen `tvojejmeno.cz`
3. Vyber **Free plán** (úplně dole) → **Continue**
4. Cloudflare se podívá na současné DNS záznamy domény a načte je
5. Zkontroluj, že načtené záznamy jsou OK (pokud máš email na doméně, měly by tam být MX záznamy)
6. **Continue**

### Krok 3: Změna nameserverů u registrátora

Cloudflare ti teď ukáže **dva nameservery** (vždy dva, ve formátu jméno.ns.cloudflare.com). Něco jako:

```
dora.ns.cloudflare.com
igor.ns.cloudflare.com
```

⚠️ **Tvoje nameservery budou jiné** — vždy dvě konkrétní jména pro tvůj účet.

### Návod pro běžné registrátory

#### Wedos
1. [client.wedos.com](https://client.wedos.com) → přihlas se
2. Levé menu → **Domény** → klikni na svoji doménu
3. Záložka **DNS** → **Změnit nameservery**
4. Přepni na **vlastní DNS servery**
5. Vyplň 2 nameservery z Cloudflare (smaž stávající Wedos NS)
6. Ulož

#### Forpsi
1. [www.forpsi.com](https://www.forpsi.com) → Klientská zóna → přihlas se
2. **Domény** → tvoje doména → **DNS servery**
3. Vyplň 2 nameservery z Cloudflare
4. Ulož

#### Active 24
1. [www.active24.cz](https://www.active24.cz) → Klientské centrum → přihlas se
2. **Domény** → klikni na doménu → **DNS** → **Vlastní DNS servery**
3. Zadej 2 nameservery z Cloudflare
4. Ulož

#### Cloudflare Registrar (pokud doména už je tam)
Tento krok přeskoč. Doména už používá Cloudflare DNS automaticky.

### Krok 4: Čekání na propagaci

Po změně nameserverů se **změna šíří internetem**. Cloudflare píše "až 24 hodin", ale v praxi to bývá **5 minut až 1 hodina**.

- Cloudflare ti pošle email *"Site is now active on Cloudflare"*, jakmile je hotovo
- Mezitím můžeš pokračovat dalšími fázemi (GitHub, Pages) — pak se na konci jen propojí

### Jak ověřit, že to už funguje

V dashboardu Cloudflare → tvoje doména → **Overview** → status:
- ⏳ **Pending nameserver update** = ještě čekáme
- ✅ **Active** = funguje

Nebo v terminálu:
```bash
dig NS tvojejmeno.cz +short
```
Pokud vidíš jména `*.ns.cloudflare.com` → je to aktivní.

---

## Časté problémy

### "Nameservery se nezměnily, čekám už 6 hodin"
- Zkontroluj, že u registrátora jsou opravdu **přesně** ty nameservery z Cloudflare (žádný překlep)
- Některé registrátory vyžadují potvrzení změny emailem — zkontroluj inbox
- Když nepomáhá, kontaktuj support registrátora

### "Cloudflare říká, že doména je už u jiného účtu"
- Doménu už někdo přidal pod jiný Cloudflare účet (možná tvůj starý, nebo bývalý spolupracovník)
- Buď ji odeber z toho druhého účtu, nebo kontaktuj Cloudflare support

### "Po změně mi přestaly chodit emaily"
- Cloudflare při importu DNS někdy nepřevezme MX záznamy správně
- Otevři Cloudflare → DNS → Records → zkontroluj MX záznamy, jestli odpovídají původním u registrátora
- Pokud ne, doplň je ručně podle staré DNS konfigurace

---

## Co když uživatel chce doménu **přesunout** k Cloudflare Registrar

> Jen pro `.com` a vybrané jiné koncovky. **`.cz` Cloudflare neregistruje.**

1. Cloudflare → **Domain Registration** → **Transfer Domains**
2. Cloudflare požádá o **EPP / authorization kód** od stávajícího registrátora
3. Ve starém registrátoru: odemkni doménu pro transfer + vyžádej EPP kód (pošlou na email)
4. Vlož kód do Cloudflare → potvrď
5. Transfer trvá **5–7 dní**

⚠️ **Před transferem zkontroluj:** doména musí být **aktivní více než 60 dní** od registrace nebo posledního transferu (ICANN pravidlo).

⚠️ **Doporučuji transfer řešit AŽ PO** dokončení základního setupu (Pages + první deploy). Ne během.

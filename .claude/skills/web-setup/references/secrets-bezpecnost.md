# Secrets a bezpečnost — pravidla pro klienta

> **Tento soubor čte skill (Claude Code) i uživatel.** Je v něm vše, co je potřeba vědět o bezpečné práci s tokeny a hesly při setupu webu.

---

## Co je token?

**Token je heslo pro stroje.** Když ty se přihlašuješ na Cloudflare, zadáš email a heslo. Když se přihlašuje **Claude Code za tebe**, potřebuje token — krátký řetězec znaků, který říká "tohle je oprávněný."

Jako fyzická analogie: token je **klíč od bytu**, který dáváš pomocníkovi v domácnosti. Dokud ho má, může vstoupit. Když ho ztratíš, vyměníš zámek (= revokuješ token a vytvoříš nový).

---

## ZLATÉ PRAVIDLO

> **Token nikdy NEVKLÁDEJ do chatu se mnou (Claude Code).**
>
> Jakmile ho sem napíšeš, je v transcriptu konverzace — i kdybys ho potom smazal. Token je prozrazený. Musí se zrušit a vytvořit nový.

To platí **vždy**. I když ti řeknu "pošli mi token" (to bych nikdy neměl říkat — pokud to čteš a já jsem to napsal, něco se pokazilo). I když ti web řekne "nasdílej token tady" (nikdy). I když si myslíš "to je dobrý, je to jen na chvilku" (není).

---

## Kde token bezpečně uložit

Existují **tři správná místa**:

### 1. Soubor `.env` v projektu (nejjednodušší)

```env
CLOUDFLARE_API_TOKEN=tvuj-token-tady
GITHUB_TOKEN=druhy-token-tady
```

**Důležité:** soubor `.env` MUSÍ být v `.gitignore`, jinak ho omylem pushneš na GitHub a bude veřejný.

Zkontroluj v terminálu:
```bash
cat .gitignore | grep .env
```
Pokud nic nevypíše:
```bash
echo ".env" >> .gitignore
```

### 2. macOS Keychain (pro Git tokeny)

Když pracuješ na Macu a poprvé `git push`, macOS automaticky nabídne **uložit přihlášení do Keychain**. Klikni "Ano" — od té doby Git token používá automaticky a tebe se neptá.

Zkontroluj, že je Keychain helper aktivní:
```bash
git config --global credential.helper
```
Mělo by vypsat `osxkeychain`. Pokud ne:
```bash
git config --global credential.helper osxkeychain
```

### 3. Správce hesel (1Password, Bitwarden, Apple Heslo, …)

Jako záloha — token si zkopíruj z Cloudflare/GitHub stránky **přímo do správce hesel** (ne přes prostředníka). Když ho budeš potřebovat znovu, vezmeš si ho odtud.

---

## Jak vytvořit Cloudflare API token

> **Před začátkem si připrav `.env` soubor lokálně (já tě tím provedu).**

### Postup

1. Přihlaš se do Cloudflare → klikni na **profil ikonu vpravo nahoře** → **My Profile**
2. Levé menu → **API Tokens**
3. **Create Token**
4. Vyber template: **"Edit Cloudflare Workers"** (nebo Custom token, viz níže)
5. **Permissions** (pro setup webu stačí):
   - Account → Cloudflare Pages → **Edit**
   - Zone → DNS → **Edit**
6. **Account Resources:** Include → **tvoje konkrétní account** (ne všechny)
7. **Zone Resources:** Include → **tvoje konkrétní doména**
8. **TTL** (volitelné): nastav vypršení — např. 1 rok. Bezpečnější než nekonečný token.
9. **Continue to summary** → **Create Token**
10. ⚠️ **Cloudflare ti token ukáže JEN JEDNOU.** Po zavření stránky už ho znovu nezobrazí.

### Co s tím tokenem teď?

**ALE NEKOPÍRUJ HO SEM DO CHATU.**

Místo toho:
1. Otevři terminál
2. Otevři `.env` soubor v editoru:
   ```bash
   nano .env
   ```
3. Vlož řádek:
   ```env
   CLOUDFLARE_API_TOKEN=zde-vlož-token-z-Cloudflare
   ```
4. Ulož (Ctrl+O, Enter, Ctrl+X v `nano`)
5. Vrať se sem a napiš jen *"hotovo"* — já token nikdy neuvidím a nepotřebuju.

---

## Jak vytvořit GitHub Personal Access Token

### Postup

1. github.com → **profil ikona vpravo nahoře** → **Settings**
2. Levé menu (úplně dolů) → **Developer settings**
3. **Personal access tokens** → **Fine-grained tokens** → **Generate new token**
4. **Token name:** např. `cloudflare-pages-deploy`
5. **Expiration:** 90 dní nebo 1 rok (bezpečnější než "No expiration")
6. **Repository access:** **Only select repositories** → vyber pouze ten konkrétní repo, který používá tento web
7. **Permissions** → Repository permissions:
   - **Contents:** Read and write
   - **Metadata:** Read (povinné)
   - (ostatní nech)
8. **Generate token**
9. ⚠️ **GitHub ti token ukáže JEN JEDNOU.** Zkopíruj ho hned do správce hesel nebo `.env`.

### Co s tím tokenem teď?

**NEKOPÍRUJ HO SEM DO CHATU.**

Buď:
- vlož ho do `.env` jako `GITHUB_TOKEN=...`
- nebo počkej, až `git push` vyzve k zadání hesla, a vlož ho v terminálu (macOS pak nabídne uložit do Keychain — řekni "Ano")

---

## Co dělat, když omylem pošleš token do chatu

Stalo se. Bez paniky, ale jednej hned:

### 1. Zruš token (revokuj)

**Cloudflare token:**
- Cloudflare → My Profile → API Tokens → najdi token → **Roll** (vygeneruje nový a starý zruší) nebo **Delete**

**GitHub token:**
- GitHub → Settings → Developer settings → Personal access tokens → najdi token → **Revoke**

### 2. Vytvoř nový

Stejným postupem jako výše. Tentokrát ho vlož **jen** do `.env` nebo Keychain.

### 3. Zkontroluj, že nikde nezůstal

```bash
grep -r "ghp_" . --exclude-dir=node_modules --exclude=.env
grep -r "ghs_" . --exclude-dir=node_modules --exclude=.env
```

(nahraď `ghp_` / `ghs_` prefixem podle typu tokenu)

Pokud něco najdeš, smaž to a commitni opravu.

### 4. Pokud byl token už pushnutý na GitHub

GitHub má funkci **Secret scanning** — pokud rozpozná token v commitu, sám ho revokuje a pošle ti email. Ale spolehnout se na to nelze. Vždy revokuj sám.

---

## Jak rozpoznat, že je něco token (ať to nepošleš omylem)

Pokud vidíš řetězec, který:
- má 30+ znaků
- vypadá jako náhodný mix písmen, čísel, někdy `_` nebo `-`
- začíná typickým prefixem:
  - `ghp_` → GitHub Personal Access Token (klasický)
  - `github_pat_` → GitHub Fine-grained PAT
  - `ghs_` → GitHub Server-to-server token
  - `xoxb-`, `xoxp-` → Slack
  - `sk-` → OpenAI / Anthropic
  - `eyJ...` (začíná "eyJ") → JWT

**→ je to token. Nikdy ho nevkládej do chatu.**

---

## Shrnutí: Bezpečnostní checklist před pokračováním

- [ ] `.env` je v `.gitignore`
- [ ] Token je jen v `.env` nebo Keychain, **NE v chatu, NE v git commitu, NE v Google Drive**
- [ ] Token má **omezené oprávnění** (jen na konkrétní repo / doménu, ne na všechno)
- [ ] Token má **expiraci** (90 dní, 1 rok — ne "navždy")
- [ ] Vím, jak token zrušit, kdyby unikl

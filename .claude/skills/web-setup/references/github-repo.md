# GitHub — účet a privátní repo

> Jak založit GitHub účet, vytvořit privátní repo pro web a naklonovat ho lokálně.

---

## Proč GitHub?

GitHub je největší světový sklad pro kód. Pro nás dělá tři věci:

1. **Verzování** — uchová historii všech změn webu (vždy se můžeš vrátit zpátky)
2. **Záloha** — pokud se rozbije počítač, kód je v cloudu
3. **Propojení s Cloudflare Pages** — Cloudflare automaticky vezme z GitHubu novou verzi a zveřejní ji na webu

Pro běžný web je **zdarma** (privátní repa neomezeně).

---

## Krok 1: Účet na GitHubu

Pokud uživatel účet nemá:

1. Otevři [github.com/signup](https://github.com/signup)
2. **Email** + **heslo** + **username** (pozor: username bude vidět veřejně, vyber rozumný — ideálně tvoje jméno nebo brand)
3. GitHub pošle ověřovací kód emailem → vlož ho
4. Vyber free plán
5. **(Volitelné)** Personalizační otázky — můžeš přeskočit

⚠️ **Heslo NIKDY nepiš do chatu.** Vlož ho jen na GitHub stránce.

### Doporučené nastavení po prvním přihlášení

1. **Two-Factor Authentication (2FA)** — povinné. Settings → Password and authentication → 2FA. Použij authenticator app (Google Authenticator, 1Password atd.).
2. **Backup codes** — ulož do správce hesel.

---

## Krok 2: Vytvořit privátní repo

> **Privátní = vidíš ho jen ty** (a kdokoli, koho přizveš). Cloudflare dostane omezený přístup tokenem.

### Postup

1. Po přihlášení klikni **+** vpravo nahoře → **New repository**
2. **Repository name:** `web-[nazev-projektu]` (např. `web-prostor-bohatstvi`, `web-kurz-leden-2026`)
3. **Description:** krátký popis (nepovinné, ale praktické: *"Web pro produkt X"*)
4. **Privát** ← **VŽDY zaškrtni**, ne public
5. **Add a README file** — zaškrtni (jinak je repo prázdné a Cloudflare Pages nezvládne první build)
6. **Add .gitignore:** vyber šablonu **None** (uděláme vlastní)
7. **Choose a license:** žádná
8. Klik **Create repository**

### Naming convention pro repo

| Typ webu | Doporučené jméno |
|---|---|
| Hlavní brand web | `web-[brand]` (např. `web-digitalni-mag`) |
| Konkrétní produkt | `web-[produkt]` (např. `web-kod-bohatstvi`) |
| Prodejní stránka kurzu | `web-prodejka-[kurz]` |
| Klientský web | `web-klient-[jmeno]` |

Konzistence pomůže — za rok najdeš na GitHubu 20 repozitářů a hned uvidíš, který co je.

---

## Krok 3: Naklonovat repo lokálně

Lokálně = na tvém počítači. Tady budeš mít kopii repa, do kterého kreslíme web.

### Mac / Linux (Terminál)

```bash
# 1. Jdi do složky, kde chceš mít projekty (např. ~/Projekty)
cd ~/Projekty   # nebo cd ~ pokud projekty zatím nemáš

# 2. Vytvoř složku, pokud ji nemáš
mkdir -p ~/Projekty
cd ~/Projekty

# 3. Naklonuj repo
git clone https://github.com/[username]/[repo-jmeno].git

# 4. Vejdi dovnitř
cd [repo-jmeno]
```

### Windows (PowerShell)

```powershell
# 1. Jdi do složky pro projekty
cd $HOME\Projekty   # nebo cd $HOME

# 2. Vytvoř složku, pokud ji nemáš
mkdir -p $HOME\Projekty
cd $HOME\Projekty

# 3. Naklonuj repo
git clone https://github.com/[username]/[repo-jmeno].git

# 4. Vejdi dovnitř
cd [repo-jmeno]
```

### Poznámka pro klienta: nemá Git nainstalovaný?

```bash
git --version
```

Pokud to vyhodí "command not found":
- **Mac:** Otevři terminál, spusť `xcode-select --install` → nainstaluje vývojářské nástroje včetně Gitu
- **Windows:** Stáhni z [git-scm.com/download/win](https://git-scm.com/download/win)
- **Linux:** `sudo apt install git` (Debian/Ubuntu) nebo `sudo dnf install git` (Fedora)

---

## Krok 4: Autentizace pro `git push`

Při prvním pokusu o `git push` GitHub zeptá na **username + heslo**. Ale jako "heslo" musíš použít **Personal Access Token (PAT)**, ne skutečné heslo (GitHub heslové autentikace pro Git zrušil).

> Detailní postup vytvoření PAT je v `secrets-bezpecnost.md` (sekce "Jak vytvořit GitHub Personal Access Token").

### Mac (s Keychain — doporučeno)

První `git push` vyzve:
```
Username for 'https://github.com': [tvoje-username]
Password for 'https://...':         [vlož PAT, ne tvoje skutečné heslo]
```

Po úspěšném push macOS nabídne **uložit přihlášení do Keychain**. **Klikni "Vždy povolit"** — od té doby Git PAT používá automaticky a tebe se neptá.

Pokud Keychain helper není aktivní, zapni:
```bash
git config --global credential.helper osxkeychain
```

### Windows

Win 10+ má vestavěné **Credential Manager**. Při prvním push se otevře okno → vlož PAT → zaškrtni "Pamatovat".

### Linux

Použij `libsecret` helper:
```bash
sudo apt install libsecret-1-0 libsecret-1-dev
sudo make --directory=/usr/share/doc/git/contrib/credential/libsecret
git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

---

## Krok 5: První commit + push (test)

> Tento test ověří, že vše funguje, **před** propojením Cloudflare Pages.

```bash
# Předpoklad: jsi v naklonované složce repa

# Vytvoř testovací soubor
echo "# Web pro [nazev-projektu]" > README.md

# Pošli změnu
git add README.md
git commit -m "Initial setup"
git push origin main
```

Pokud `git push` proběhne bez chyby → otevři GitHub stránku tvého repa, README by tam mělo být aktualizované.

⚠️ Pokud `git push` selže s "Authentication failed" → token je špatně. Vrať se k `secrets-bezpecnost.md`.

---

## Časté problémy

### "Permission denied (publickey)"
- Používáš SSH URL (`git@github.com:...`) místo HTTPS. Změň URL repa:
  ```bash
  git remote set-url origin https://github.com/[username]/[repo].git
  ```

### "Repository not found"
- Špatné jméno repa nebo username v URL
- Repo je privátní a nemáš správný token s přístupem
- Zkontroluj: `git remote -v` — vidíš správnou URL?

### "Updates were rejected because the remote contains work that you do not have locally"
- Někdo (nebo ty na druhém stroji) push v mezičase. Stáhni nejdřív:
  ```bash
  git pull origin main
  ```
  → vyřeš případné konflikty → znovu push.

### "fatal: not a git repository"
- Nejsi ve složce repa. Zkontroluj `pwd` — jsi v naklonované složce?

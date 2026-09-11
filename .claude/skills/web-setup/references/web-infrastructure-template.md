# Šablona pro `web-infrastructure.md`

> Skill na konci Fáze 6 vytvoří v rootu projektu uživatele soubor `web-infrastructure.md`. Tento soubor je **single source of truth** pro všechny další web skilly. Když potom uživatel spustí `design-system`, `sales-page` nebo `presentation-web` v tomto projektu, ony si přečtou tento soubor a vědí, kam deployovat.

Skill zkopíruje obsah níže (mezi `--- START ---` a `--- END ---`), nahradí placeholdery skutečnými hodnotami a uloží.

---

## --- START ---

```markdown
# Web Infrastructure

> Single source of truth pro deploy webu. Vyplněno skillem `web-setup` dne {{datum}}. Když je potřeba změnit, znovu spusť `web-setup` (najde tento soubor a aktualizuje ho).

## Vlastnictví

- **Web patří:** {{jméno / firma — kdo má účty}}
- **Stavěl/a:** {{jméno toho, kdo nastavoval}}
- **Datum nastavení:** {{YYYY-MM-DD}}

## Doména

- **Doména:** `{{domena.cz}}`
- **Registrátor:** {{Wedos / Forpsi / Cloudflare Registrar / ...}}
- **Vyprší:** {{YYYY-MM-DD}}
- **Auto-renew:** {{ano / ne}}
- **Whois privacy:** {{zapnuto / vypnuto}}

## DNS

- **DNS provider:** Cloudflare
- **Status:** {{Active / Pending}}
- **Nameservery:** `{{ns1.cloudflare.com}}`, `{{ns2.cloudflare.com}}`

## Hosting

- **Provider:** Cloudflare Pages
- **Pages projekt:** `{{nazev-projektu}}`
- **Pages URL (záložní):** `https://{{nazev-projektu}}.pages.dev`
- **Production URL:** `https://{{domena.cz}}`
- **SSL:** {{aktivní / pending}}

## Cloudflare

- **Account ID:** `{{xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx}}`
- **API token:** uložen v `.env` jako `CLOUDFLARE_API_TOKEN` (nikdy ne zde)

## GitHub

- **Repo:** `https://github.com/{{username}}/{{repo-jmeno}}`
- **Visibility:** Private
- **Production branch:** `main`
- **PAT:** uložen v macOS Keychain / `.env` jako `GITHUB_TOKEN` (nikdy ne zde)

## Sdílené styly (jedno CSS pro celý web)

> Bez tohohle se web rozpadne na tolik vzhledů, kolik má stránek. **Každá nová stránka odkazuje
> na tyhle soubory a nemá vlastní barvy natvrdo.**

- **Soubor s hodnotami:** `{{/tokens.css}}` — barvy, fonty, rozestupy, zaoblení jako proměnné
- **Soubor se společnými prvky:** `{{/styl.css}}` — nadpisy, tlačítka, karty, sekce
- **Zdroj hodnot:** {{design systém majitele / zatím provizorní — doplní `design-system`}}
- **Vkládá se do každé stránky:**
  ```html
  <link rel="stylesheet" href="/tokens.css">
  <link rel="stylesheet" href="/styl.css">
  ```
- **Kontrola:** změna hlavní barvy v `tokens.css` musí přebarvit **všechny** stránky webu

## Lokální cesta

- **Working directory:** `{{/Users/.../Projekty/repo-jmeno}}`

## Deploy workflow

```bash
# Standardní deploy
cd {{/Users/.../Projekty/repo-jmeno}}
git add .
git commit -m "{{popis změny}}"
git push origin main

# Cloudflare Pages do 30 sekund deployuje na https://{{domena.cz}}
```

## Build settings (Cloudflare Pages)

| Pole | Hodnota |
|---|---|
| Framework preset | None |
| Build command | (prázdné) |
| Build output directory | `/` |
| Root directory | `/` |
| Production branch | `main` |

## Co tento web umí

- ✅ Statický web (HTML, CSS, JS) — automatický deploy po pushi
- ✅ SSL zdarma (zelený zámeček)
- ✅ CDN po celém světě (rychle všude)
- ❌ Server-side logika (Python/Node backend) — pro to bude potřeba Cloudflare Workers, separátně
- ❌ Databáze — pro to bude potřeba Cloudflare D1 / KV, separátně

## Pro budoucí skilly (design-system, sales-page, presentation-web, ...)

Když děláš stránku v tomto projektu, pamatuj si:
- **Working directory:** `{{/Users/.../Projekty/repo-jmeno}}`
- **Output:** statický HTML / CSS / JS
- **Deploy:** `git push` → Cloudflare se postará o zbytek
- **Test URL:** `https://{{domena.cz}}` se aktualizuje do 30 sekund po pushi

## Historie změn

- **{{YYYY-MM-DD}}** — Initial setup přes skill `web-setup`
```

## --- END ---

---

## Pravidla pro vyplnění (pro skill)

1. **Placeholdery** v `{{...}}` skill nahradí skutečnými hodnotami.
2. **Tokeny, hesla, secrets do tohoto souboru NIKDY nepatří.** Patří do `.env`.
3. Pokud uživatel nějakou hodnotu nezná, skill napíše `(neznámé — doplň ručně)` místo placeholderu.
4. Skill na konci Fáze 6 commitne soubor:
   ```bash
   git add web-infrastructure.md
   git commit -m "Add web infrastructure documentation"
   git push
   ```
5. **Pokud `web-infrastructure.md` už v projektu existuje** (uživatel skill spouští znovu), skill místo přepsání:
   - přečte stávající soubor
   - aktualizuje jen ty sekce, které se změnily
   - přidá řádek do "Historie změn"

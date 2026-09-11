# Ověření přístupu (bez vypsání klíče)

> K čemu to je: „soubor je uložený“ není „funguje to“. Ověřuje se **dotazem**, ne pohledem
> do souboru s klíči.
> Naposledy ověřeno: 2026-08-06.

---

## Železné pravidlo

🔴 **Na soubor s klíči nikdy nepoužívej nástroje na čtení souborů ani `cat`, `grep`, `head`.**
Ani „jen na kontrolu, jestli tam ten klíč je“. Ověřuje se tak, že se **provede neškodná akce**:
projde, nebo neprojde.

Skript si klíč načte sám a **nikam ho nevypíše.**

---

## Ověřovací skript

```python
#!/usr/bin/env python3
"""Overi pristup do Cloudflare. Hodnota klice se NIKDY nevypisuje."""
import json, urllib.request, urllib.error

ENV = ".env"          # cesta k souboru s klici
PREFIX = "CLOUDFLARE" # najde vsechny CLOUDFLARE_* klice

env = {}
with open(ENV, encoding="utf-8") as f:
    for line in f:
        line = line.strip()
        if line and not line.startswith("#") and "=" in line:
            k, v = line.split("=", 1)
            env[k.strip()] = v.strip().strip('"').strip("'")

def get(url, token):
    req = urllib.request.Request(url)
    req.add_header("Authorization", "Bearer " + token)
    try:
        with urllib.request.urlopen(req, timeout=30) as r:
            return json.loads(r.read().decode()), None
    except urllib.error.HTTPError as e:
        try:
            body = json.loads(e.read().decode())
            msg = "; ".join(x.get("message", "") for x in body.get("errors", []))
        except Exception:
            msg = ""
        return None, "HTTP %s %s" % (e.code, msg)

for name, token in env.items():
    if "TOKEN" not in name.upper() or PREFIX not in name.upper():
        continue
    print("=== %s ===" % name)
    res, err = get("https://api.cloudflare.com/client/v4/user/tokens/verify", token)
    if not res:
        print("  NEFUNGUJE -> %s" % err)
        continue
    print("  platny (stav %s)" % res.get("result", {}).get("status"))
    z, ze = get("https://api.cloudflare.com/client/v4/zones?per_page=50", token)
    if z:
        zony = [x["name"] for x in z.get("result", [])]
        print("  vidi domen: %d %s" % (len(zony), zony[:8]))
    else:
        print("  domeny: %s (chybi Zone -> Zone -> Read?)" % ze)
```

---

## Jak číst výsledek

| Výstup | Co to znamená | Co udělat |
|---|---|---|
| `platny (stav active)` + seznam domén | **hotovo** | pokračuj, řekni uživateli, co teď umíš |
| `NEFUNGUJE -> HTTP 401 Invalid API Token` | klíč je špatný, neúplný nebo neuložený | znovu vložit; pozor na mezery a uvozovky |
| `platny`, ale `vidi domen: 0` | chybí **Zone → Zone → Read** nebo je rozsah zúžený | upravit existující token (klíč se nemění) |
| `HTTP 403` | token platí, ale nemá právo na tuhle věc | doplnit chybějící oprávnění |

---

## Ověření wrangleru (když se jede bez API klíče)

```bash
npx wrangler whoami
```

Vypíše účty a **seznam oprávnění**. Užitečné i u API klíče: hned je vidět, jestli je mezi nimi
`zone (write)` — když je tam jen `zone (read)`, **DNS se měnit nedá**.

---

## Co zapsat, když je hotovo

Do firemního mozku (část o napojeních) patří: **že je Cloudflare napojený, na jaký účet, co tím
agent umí a kde klíč bydlí** — nikdy hodnota klíče. Například:

> Cloudflare napojený (účet {jméno}). Klíč v souboru s klíči jako `CLOUDFLARE_API_TOKEN`.
> Agent umí: nasazovat weby a stránky, spravovat DNS a subdomény, zakládat databáze a aplikace.
> Ověřeno {datum}, vidí {počet} domén.

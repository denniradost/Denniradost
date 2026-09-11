# Cloudflare Pages — propojení s GitHub a vlastní doménou

> Jak nastavit automatický deploy webu z GitHub repa přes Cloudflare Pages na vlastní doménu.

---

## Co je Cloudflare Pages?

**Cloudflare Pages** je hostingová služba zdarma. Funguje takto:

1. Připojí se k tvému GitHub repu
2. Pokaždé, když tam pushnel novou verzi, **sám stáhne kód** a publikuje ho na webu
3. Web běží na tvojí doméně (s SSL zámečkem zdarma)

**Zdarma:** neomezené sites, neomezené requests, 500 buildů/měsíc, 100 vlastních domén.

---

## Předpoklady

Než začneš, musíš mít hotové:
- ✅ Cloudflare účet (Fáze 2 hlavního skillu)
- ✅ Doména v Cloudflare nebo s nameservery na Cloudflare (Fáze 2)
- ✅ Privátní GitHub repo s alespoň jedním commitem (Fáze 3) — README.md stačí
- ✅ Lokálně naklonované repo

---

## Krok 1: Vytvořit Pages projekt

1. V Cloudflare dashboardu → levé menu → **Workers & Pages**
2. Klikni **Create application** → záložka **Pages** → **Connect to Git**
3. Klikni **Connect GitHub** (poprvé tě požádá o autorizaci)
4. V GitHub okně:
   - Vyber **Only select repositories** (NIKDY "All repositories")
   - Najdi a vyber **jen ten konkrétní repo** pro tento web
   - Klikni **Install & Authorize**
5. Vrátíš se zpět do Cloudflare → vyber repo ze seznamu → **Begin setup**

### Build settings

Pro obyčejný HTML web (zatím bez frameworku):

| Pole | Hodnota |
|---|---|
| Project name | (může být stejné jako repo, nebo zkrácené — pojede pod `*.pages.dev`) |
| Production branch | `main` |
| Framework preset | **None** |
| Build command | (nech prázdné) |
| Build output directory | `/` |
| Root directory | `/` |
| Environment variables | (zatím žádné) |

Klik **Save and Deploy**.

První build proběhne za 30 sekund. Cloudflare ti ukáže URL ve formátu `https://[project-name].pages.dev` — zatím web běží na téhle dočasné adrese.

---

## Krok 2: Připojit vlastní doménu

> Tady přidáme tvoji skutečnou doménu, takže web bude běžet na `tvojejmeno.cz` místo na `*.pages.dev`.

1. V Pages projektu → záložka **Custom domains** → **Set up a custom domain**
2. Zadej doménu (bez `https://`, jen `tvojejmeno.cz`)
3. Cloudflare zkontroluje, že doména je v tvém Cloudflare účtu (musí být)
4. Cloudflare automaticky přidá DNS záznamy → klik **Activate domain**
5. Počkej ~30 sekund

### Subdomény (volitelné)

Chceš `www.tvojejmeno.cz` taky? Opakuj postup s `www.` prefixem. Cloudflare přidá oba.

Doporučení: nastav redirect z `www.` na holou doménu (nebo opačně, podle vkusu) v Cloudflare → **Rules** → **Page Rules**. Ale to je nice-to-have, ne nutnost.

### SSL (HTTPS)

SSL se aktivuje **automaticky** během 1–5 minut. Žádné nastavení netřeba. V prohlížeči pak vidíš zelený zámeček.

---

## Krok 3: Test deploy z lokálu

V naklonovaném repu:

```bash
# Vytvoř testovací stránku
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <title>Funguje to!</title>
  <style>
    body{font-family:system-ui,sans-serif;max-width:600px;margin:4rem auto;padding:1rem;line-height:1.6}
    h1{color:#0066cc}
  </style>
</head>
<body>
  <h1>Funguje to. ✨</h1>
  <p>Tohle je první stránka na nové infrastruktuře.</p>
  <p><small>Postaveno přes Cloudflare Pages.</small></p>
</body>
</html>
EOF

# Pushni změnu
git add index.html
git commit -m "První test deploy"
git push origin main
```

V Cloudflare dashboard → Pages → tvůj projekt → **Deployments** uvidíš novou deployment "Building..." → "Success" během ~30 sekund.

Otevři v prohlížeči `https://tvojejmeno.cz` → měl bys vidět nadpis *"Funguje to."*.

🎉 **Tady to slav.** Máš funkční pipeline: lokál → GitHub → Cloudflare → tvoje doména.

---

## Krok 4 (volitelné): Cloudflare API token pro Claude Code

Pokud chceš, aby Claude Code uměl s Cloudflare Pages mluvit přímo (např. zjišťovat status deployů, přidávat domény bez nutnosti otvírat dashboard), vytvoř API token.

> Detailní postup vytvoření tokenu je v `secrets-bezpecnost.md` (sekce "Jak vytvořit Cloudflare API token").

⚠️ **Token vlož jen do `.env`, nikdy do chatu.**

```env
CLOUDFLARE_API_TOKEN=xxx
CLOUDFLARE_ACCOUNT_ID=yyy
```

`CLOUDFLARE_ACCOUNT_ID` najdeš v Cloudflare → pravý sidebar → **Account ID** (klikni "Copy").

---

## Časté problémy

### "Build failed: Build directory not found"
- Build output directory je špatně. Pro HTML bez frameworku má být `/` nebo prázdné, ne `dist` ani `build`.
- Otevři Pages → Settings → Builds & deployments → změň a re-deployuj.

### "Domain pending validation"
- DNS nameservery ještě nepropagovaly (viz `cloudflare-ucet-a-domena.md`)
- Počkej až 1 hodinu, potom refreshni stránku Custom domains.

### "Site not secure" / SSL nefunguje
- Cloudflare SSL aktivace někdy trvá až 24 hodin (vzácně). Většinou do 5 minut.
- Pokud po 24 hodinách nejde: Cloudflare → tvoje doména → **SSL/TLS** → Edge Certificates → zkontroluj, že je aktivní.

### "Stránka ukazuje starou verzi"
- Browser cache. Hard refresh (`Cmd+Shift+R` na Macu, `Ctrl+Shift+R` na Windows)
- Nebo zkus inkognito tab.

### "Push prošel, ale Pages neudělal nový build"
- Zkontroluj, že push šel do **správné branche** (default `main`, ne `master` ani jiné)
- Pages → Settings → Builds & deployments → **Production branch**

---

## Co udělá Claude Code za tebe automaticky

V další fázi (až budou existovat skilly `sales-page`, `presentation-web` atd.) bude Claude Code:
- Číst `web-infrastructure.md` a vědět, kam deployovat
- Vytvořit / upravit HTML, CSS, JS soubory v repu
- Spustit `git add`, `git commit`, `git push`
- Sledovat status deploye
- Hlásit ti URL, kde web běží

Tj. tvoje role pak bude **dát zadání**, ne klikat ručně.

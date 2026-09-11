# Fotobanka: posbírej obrázky dřív, než začneš stavět

> **K čemu to je:** aby vzorová stránka a všechny další stránky měly **skutečné obrázky**,
> ne prázdné rámečky. Design bez obrázků vypadá nedodělaně — i když jsou barvy, písmo
> a rozestupy úplně správně.
>
> **Proč to musí být napsané:** u textů má skill železné pravidlo „nikdy Lorem Ipsum“.
> U obrázků dlouho žádné nebylo, a tak vznikaly návrhy s prázdnými plochami. Vzniklo
> z reálného případu 2026-08-15: klientce se postavil design podle jejího webu — barvy
> a písmo seděly, obrázky chyběly úplně.

---

## Pravidlo

> **Vzorová stránka nesmí mít prázdná místa místo obrázků.**
> Buď skutečné fotky majitele, nebo — když opravdu žádné nejsou — **označené zástupné
> plochy plus seznam záběrů k nafocení**. Nikdy prázdno bez vysvětlení.

Vlastní fotky mají vždycky přednost před stockem. Stock je nouzové řešení, ne výchozí.

---

## Postup: z existujícího webu do fotobanky

Dělá se **hned v úvodním průzkumu** (fáze 0), spolu se čtením barev a písma. Ne až
nakonec — obrázky jsou vstup do návrhu, ne dekorace na konec.

### 1. Posbírej, co na webu je

Projdi web majitele (`agentni-prohlizec` nebo stažení stránky) a vytáhni:

| Co hledat | Proč to chceš |
|---|---|
| **Logo** — nejlépe průhledné PNG nebo SVG | bez něj nepostavíš hlavičku ani patičku |
| **Portréty majitele** | úvodní sekce, sekce „o mně“, reference, patička |
| **Fotky produktů, obalů, mockupů** | sekce s nabídkou, karty produktů |
| **Fotky z akcí, z práce, ze zákulisí** | důkazy, příběh, sociální důkaz |
| **Pozadí a textury úvodních sekcí** | často to nejdůležitější — bez nich hero „není ono“ |
| **Obrázkové reference** (screenshoty zpráv, komentářů) | sekce s důkazy |
| **Ikony, které si nechal udělat** | pokud nejsou obecné, patří ke značce |

Bere se **jen to, co patří majiteli** — jeho vlastní web. Cizí obrázky (stock koupený
někým jiným, fotky partnerů) do fotobanky nepatří; když je potřeba, řekni to nahlas.

### 2. Ulož do fotobanky — jedno místo pro celý provoz

🔴 **Fotobanka je vždycky složka `grafika/`** ve složce, kde agent žije. Ne „někam do
projektu“, ne vedle stránek, ne pokaždé jinam. Když si každý skill uloží obrázky jinam,
za měsíc je nikdo nenajde a stáhnou se znovu.

```
grafika/
├── loga/       ← logo ve všech podobách (průhledné PNG, SVG, na světlé i tmavé)
├── fotky/      ← portréty, fotky z akcí, ze zákulisí
├── produkty/   ← obaly, mockupy, vizuály produktů
├── web/        ← co je stažené z webu: pozadí hero sekcí, ilustrace, ikony
│   └── <projekt>/   ← když je webů nebo klientů víc, každý má svou podsložku
├── INBOX/      ← co ještě nemá popisek a zatřídění
└── README.md
```

**Tuhle složku zakládá skill na firemní mozek.** Když ji majitel nemá (mozek ani
startovací balíček nainstalovaný nejsou), **založ ji sám — ve stejné podobě.** Struktura
je stejná pro všechny, ať se člověk mezi projekty neztrácí a ať později mozek najde
obrázky tam, kde je čeká.

Ke každému obrázku:

- **Srozumitelný název souboru** — `daniel-u-bazenu.webp`, ne `IMG_4471.jpg`.
  Podle názvu se vybírá, když se za měsíc staví další stránka.
- **Popisek jako sousední soubor** `<obrázek>.md` (tzv. sidecar) — volný text, 2–4 věty:
  co na obrázku je, čemu odpovídá ve značce, kdy ho použít.
  *„Na výšku, tmavé pozadí vpravo — sedí do úvodní sekce s textem vlevo.“*
  Sidecar se stěhuje vždycky spolu s obrázkem. **Tohle je stejná úmluva, jakou používá
  mozek** — díky ní umí noční údržba obrázky bez popisku sama dopsat a zatřídit.
- **Web verze**: převeď na WebP a zmenši na rozumnou šířku (velké fotky brzdí web).
  Originál si nech, ale na stránky dávej odlehčenou verzi.
- **Průhledné PNG** označ v popisku — hodí se na tmavé pozadí, kde jinak vznikne bílý rám.

**Nevíš, kam obrázek patří?** Nech ho v `INBOX/` a napiš mu sidecar. Zatřídí se později —
horší než špatná podsložka je obrázek bez popisku, který nikdo nepozná.

### 3. Poznamenej, čeho je málo

Projdi seznam výš a napiš, co chybí. To je rovnou **zadání na focení** — konkrétní
záběry, ne „potřebuješ lepší fotky“:

> *„Chybí: portrét na šířku s prostorem vlevo na text (úvodní sekce), tři fotky
> při práci na výšku (sekce o metodě), fotka produktu na neutrálním pozadí.“*

### 4. Teprve teď stav

Vzorová stránka i přehled prvků **používají obrázky z fotobanky**, odkazem na skutečné
soubory. Ne prázdné `<div>`, ne šedý obdélník bez popisu.

---

## Když majitel opravdu žádné obrázky nemá

Stane se to u nového podnikání. Pak:

1. Vzorová stránka dostane **označené zástupné plochy** — světlá plocha s popisem,
   co na to místo patří („sem portrét na šířku, prostor vlevo na text“).
   Nikdy prázdné místo bez vysvětlení: to vypadá jako chyba, ne jako záměr.
2. Ke stránce přiložíš **seznam záběrů k nafocení** (bod 3 výš).
3. **Řekneš to nahlas** v shrnutí: *„Návrh má zástupné plochy, protože fotky zatím
   nejsou. Až je pošleš, dosadím je a vypadá to úplně jinak.“* Bez téhle věty si
   majitel myslí, že takhle bude vypadat výsledek.

---

## Kontrola před „hotovo“

- [ ] Prošel jsem web majitele a **stáhl z něj obrázky** do fotobanky?
- [ ] Leží obrázky v **`grafika/`** se správnou podsložkou (a když složka nebyla, založil jsem ji)?
- [ ] Mají soubory **srozumitelné názvy** a **sidecar popisek** `<obrázek>.md`?
- [ ] Používá vzorová stránka **skutečné obrázky**, ne prázdné plochy?
- [ ] Má úvodní sekce svůj obrázek nebo pozadí? (Tady se prázdno pozná nejdřív.)
- [ ] Když fotky nejsou: jsou plochy **označené** a existuje seznam záběrů k nafocení?
- [ ] Řekl jsem majiteli, co chybí a co to udělá s výsledkem?

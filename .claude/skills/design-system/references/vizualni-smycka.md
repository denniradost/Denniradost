# Vizuální smyčka — dívej se na to, co jsi postavil

> K čemu to je: agent, který stránku napíše a neotevře, odevzdá kód, který se **správně vykreslí,
> ale vypadá jako šablona.** Rozdíl mezi „funguje to“ a „vypadá to dobře“ je vidět jen na obrázku.
> Vzniklo z majitelovy poznámky 2026-08-06: *„zkoušel jsem dělat stránky a nebylo to ono.“*
> Naposledy změněno: 2026-08-06.

---

## Proč to funguje

Nástroj na vizuální design (Claude Design a podobné) dělá jednu věc navíc: **vykreslí výsledek
a podívá se na něj.** Není v tom lepší model, je v tom zpětná vazba. Agent na počítači má prohlížeč
taky, jen ho běžně nepoužije, protože mu to nikdo nenapsal do postupu.

**Tenhle soubor je ten postup.**

---

## Smyčka (opakuje se, dokud to nesedí)

### 1. Otevři
- Dev server: `preview_start` (má-li projekt vlastní dev server).
- Samostatný HTML soubor: `preview_start` s `url` na `file:///…`, nebo skill `agentni-prohlizec`.

### 2. Udělej screenshot
`computer` s akcí `screenshot`. **Podívej se na něj.** Ne na kód, na obrázek.

### 3. Projeď osm otázek (v tomhle pořadí)

Ptej se konkrétně. „Líbí se mi to“ není hodnocení.

1. **Dýchá to?** Je kolem nadpisů a mezi sekcemi dost prostoru? *(Nejčastější chyba je málo místa,
   ne moc.)*
2. **Vidím hierarchii?** Co je první, druhé, třetí? Když přimhouřím oči, vyskočí nadpis a tlačítko?
3. **Vyskočí tlačítko?** Nebo splývá s okolím? Je jasné, co se má zmáčknout?
4. **Nejsou řádky moc dlouhé?** Nad zhruba 70 znaků se text čte špatně. *(Klasická chyba: text
   roztažený přes celou šířku obrazovky.)*
5. **Drží zarovnání?** Začínají prvky pod sebou na stejné svislici, nebo je každý o kousek jinde?
6. **Je kontrast čitelný?** Šedý text na světlém pozadí vypadá na monitoru elegantně a na mobilu
   na slunci je neviditelný. Minimum 4,5 : 1.
7. **Nejsou tam sirotci?** Osamělé slovo na řádku, nadpis zalomený uprostřed slovního spojení.
8. **Sedí obrázky?** Nejsou roztažené, rozmazané, nebo useknuté v nejdůležitějším místě?

### 4. Zkontroluj mobil
`resize_window` na mobilní šířku (375 px), **znovu screenshot**. Podívej se hlavně na:
- nepřetéká něco vodorovně (stránka se nesmí dát posouvat do stran),
- není nadpis zalomený do pěti řádků,
- dá se tlačítko zmáčknout prstem (výška aspoň 44 px),
- není text menší než 16 px.

### 5. Oprav a vrať se na krok 2
Klidně třikrát. **Každá oprava se musí zase vidět** — často jedna oprava rozbije jinou věc.

### 6. Teprve pak hotovo
Do zprávy majiteli **přilož screenshot**, ne popis. „Postavil jsem stránku podle design systému“
není důkaz. Obrázek je.

---

## Co je vidět jen na screenshotu (a v kódu nikdy)

- Hero sekce, která zabírá celou obrazovku a **nic pod ní není vidět** — člověk neví, že má scrollovat.
- Dvě sekce za sebou ve stejné barvě → **splynou v jednu** a stránka působí nekonečně.
- Ikony v různých velikostech nebo tloušťkách čar.
- Tlačítko a odkaz vedle sebe, které vypadají stejně důležitě.
- Obrázek s bílým pozadím na barevné sekci (viditelný obdélník).
- Text přes fotku v místě, kde je fotka světlá → nečitelné.
- Karty různě vysoké, když mají různě dlouhý text.
- Patička, která vypadá jako další sekce.

---

## Kdy smyčku vynechat

Skoro nikdy. Výjimky:
- **Změna je čistě textová** (přepis odstavce, oprava překlepu) a nemění délku nadpisů.
- **Prostředí prohlížeč nemá** (běh bez obrazovky). Pak to **řekni** — „nedíval jsem se na výsledek,
  ověř prosím vzhled" — a nepředstírej hotovo.

---

## Na co pozor

- ❌ Ohlásit hotovo bez otevření → ✅ screenshot je součást odevzdání
- ❌ Dívat se jen na desktop → ✅ mobil je u většiny lidí první, ne druhý
- ❌ Opravit tři věci naráz a nepodívat se mezi tím → ✅ oprava, screenshot, oprava
- ❌ „Vypadá to dobře“ → ✅ projet osm otázek a pojmenovat, co konkrétně je dobře a co ne
- ❌ Poslat majiteli popis místo obrázku → ✅ obrázek, ať se nemusí ptát

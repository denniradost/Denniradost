# Šablony podle kanálu

> Barvy a fonty jsou jedna věc; **každý kanál má vlastní omezení**. Tenhle soubor říká, co v kterém
> kanálu z design systému platí, co se mění a co se v něm rozbije.

---

## E-mail — nejvíc omezený kanál

E-mail **není web.** Renderuje ho desítky různých klientů, z nichž některé stojí na dvacet let starém
jádru. Proto má vlastní pravidla — a proto je nejlepší mít **jednu ověřenou šablonu** a v ní jen měnit obsah.

### Technická pravidla (dodržet, jinak to spadne)

| Pravidlo | Proč |
|---|---|
| **Šířka 600 px**, u textových newsletterů klidně 500 px | historický standard, projde všude |
| **Jeden sloupec** | na mobilu se dvousloupcové rozvržení láme nepředvídatelně |
| **Rozvržení tabulkami** (`<table>`), ne `<div>` | Outlook nerenderuje moderní layout |
| **Styly inline** (`style="…"`) | část klientů odstraní `<style>` v hlavičce |
| **Systémový font + náhrada** | webové fonty se v mnoha klientech nenačtou; napiš celý řetězec záložních fontů |
| **Text min. 16 px** | na mobilu se menší text nečte |
| **Tlačítko jako HTML**, ne obrázek | obrázky se u části lidí nezobrazí a tlačítko zmizí |
| **Alternativní text u všech obrázků** | mnoho klientů obrázky blokuje ve výchozím stavu |
| **Průhledné PNG místo bílého pozadí** | v tmavém režimu vznikne bílý blok |
| **Ověřit barvy v tmavém režimu** | Gmail, Outlook a Apple Mail ho řeší každý jinak |
| **Celé HTML pod 100 kB** | Gmail nad ~102 kB e-mail zkrátí („zobrazit celou zprávu“) |
| **Preheader** — skrytý první řádek | doplňuje předmět v náhledu; bez něj tam vlezou první slova šablony |

### Co z design systému do e-mailu patří

- **Hlavní a akcentní barva** (tlačítko), barva textu, barva pozadí — plus tmavá varianta.
- **Fonty:** vybraný systémový font + řetězec záloh (webový font jen jako bonus).
- **Šířka, velikost písma, výška řádku** (1,5–1,6).
- **Podoba tlačítka** — barva, zaoblení, velikost, text vždycky podle skillu `vyzva-k-akci`.
- **Patička** — kdo píše, odkud má adresu, jednoklikové odhlášení.
- **Kde je logo** (a jestli vůbec — u osobní značky bývá lepší bez).

### Co do e-mailu nepatří

Vícesloupcové mřížky, obrázková tlačítka, pozadí přes celou šířku, jemné světle šedé texty (v tmavém
režimu zmizí), videa (vloží se náhled s odkazem), fonty jen z webu.

**Příklad z praxe:** šablona jede 500 px, Tahoma 20 px, vlevo zarovnaná, preheader jako skrytý div,
personalizace `df_salution`/`df_gender`. Technické nasazení řeší skill nasazení do e-mailového nástroje —
tenhle soubor drží **rozhodnutí o vzhledu**, ten skill jejich provedení.

---

## Sociální sítě

**Cíl: 2–3 opakovatelné šablony.** Víc si nikdo neudrží a začne improvizovat — a tím padá konzistence.

### Formáty
- **1 : 1** (1080 × 1080) — univerzální příspěvek
- **4 : 5** (1080 × 1350) — zabere nejvíc místa ve zdi, nejlepší pro dosah
- **9 : 16** (1080 × 1920) — stories a reels
- **Náhled videa na YouTube** (1280 × 720) — když se dělá i video

### Co určit v design systému
- **Titulek v obrázku:** font, velikost, zarovnání, kolik slov maximálně (víc než 8 nikdo nepřečte)
- **Kde je logo** a jak velké (u osobní značky často stačí jméno v patičce)
- **Barva pozadí** u textových a citátových postů — 2 varianty (světlá, tmavá)
- **Jak se pracuje s fotkou:** přetisk textu ano/ne, ztmavení, kde je tvář
- **Rozpoznávací prvek** — barevný pruh, rámeček, zlatá linka, cokoli, co drží mřížku profilu pohromadě
- **Co se nikdy nedělá:** stock fotky s podanou rukou, šest fontů v jedné grafice, text až k hraně

### Test
Postav si **mřížku 9 náhledů** vedle sebe. Když nevypadají jako jedna značka, šablony nejsou hotové.

---

## Prezentace, webináře, PDF a e-booky

- **Titulní strana:** název, jméno, jeden vizuál. Nic víc.
- **Běžná strana:** jeden nadpis, max 5 odrážek nebo jeden obrázek. Velikost písma pro promítání
  minimálně 24 px.
- **Barvy:** tmavé pozadí funguje na promítání lépe než bílé (nesvítí do očí), ale u PDF k tisku naopak.
  Proto měj obě varianty.
- **Kde je logo:** u prezentace stačí na první a poslední straně.
- **Poslední strana:** jeden odkaz a jedna výzva k akci.
- **PDF ke stažení** (e-book, checklist): patička s webem na každé straně, klikatelné odkazy.

---

## Web

Řeší se v hlavním postupu skillu (fáze 3) — komponenty a hodnoty jsou primárně webové. Doplňkově:

- **Mobil na prvním místě.** Rozhodnutí, které dobře vypadá na velké obrazovce a rozsype se na mobilu,
  je špatné rozhodnutí — většina lidí přijde z telefonu.
- **Hero sekce:** nadpis, podnadpis, tlačítko, jeden vizuál. Nadpisy dělá skill `nadpisy-a-nazvy`.
- **Rytmus stránky:** světlá sekce → tmavá → světlá; neměň vzhled bloku uprostřed stránky.

---

## Jak s tímhle pracovat prakticky

1. Pro každý kanál, který majitel **reálně používá**, vznikne v `design-system.md` jedna sekce.
   Kanál, který nepoužívá, se nevyplňuje — prázdné sekce nikdo nečte.
2. U každého kanálu ať je **jedna hotová ukázka** (rozpracovaný e-mail, jeden post, jedna sekce).
   Ukázka je použitelnější než popis.
3. Když se změní barva nebo font v základu, projdi kanály a **oprav je všude** — jinak se rozejdou.

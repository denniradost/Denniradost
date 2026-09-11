# Vizuální audit — jak přečíst, jak značka vypadá dnes

> **K čemu to je:** většina lidí nemá design systém, ale **nějak už vypadají**. Než se začne cokoli
> vymýšlet, přečte se, co existuje. Vznikne z toho seznam „tohle zachovat · tohle sjednotit · tohle
> chybí" — a to je mnohem lepší začátek než prázdný papír.
>
> **Pravidlo:** co najdeš, **neber automaticky za záměr.** Vždycky se zeptej: *„Je to takhle schválně,
> nebo se to sešlo?"*

---

## 1. Živý web

Nech si dát adresu (a adresy podstránek — prodejní stránka bývá jiná než úvodka).

**Co udělat:**
1. **Otevři a udělej screenshot** — desktop i mobil (skill `agentni-prohlizec`, nebo prohlížeč v aplikaci).
2. **Vytáhni skutečné hodnoty z CSS**, ne z dojmu — barvy textu a pozadí, rodiny fontů, velikosti,
   šířku obsahu, zaoblení, stíny. (V prohlížeči jde spočítat i frekvence: které barvy se opakují nejčastěji.)
3. **Zapiš, co se opakuje** a co je jednorázové. Barva, která je na webu jednou, není brandová barva.

**Co z toho vytáhnout:**

| Co | Kde se to pozná |
|---|---|
| Hlavní a akcentní barva | tlačítka, nadpisy, odkazy |
| Kolik barev celkem | čím víc, tím větší nekonzistence (víc než 5–6 je signál) |
| Fonty a velikosti | nadpisy vs. text; velikost textu pod 16 px je problém |
| Šířka a rytmus | šířka textového bloku, mezery mezi sekcemi |
| Tvarosloví | zaoblení, stíny, obrysy, čáry |
| Fotostyl | vlastní vs. stock, světlé vs. tmavé, s textem vs. bez |
| Tlačítka | kolik různých podob má „to samé“ tlačítko |

**Rychlá diagnóza konzistence:** otevři 5–10 nedávných stránek nebo materiálů a porovnej barvy a fonty.
Kde se hex kódy a fonty rozcházejí, tam je práce.

## 2. Sociální sítě

Podívej se na **posledních 9–12 příspěvků** (mřížka profilu řekne víc než jednotlivý post).

- Jsou příspěvky **rozpoznatelné jako jedna značka**, nebo vypadají jako od pěti lidí?
- Jaké formáty se opakují (fotka s textem, citát, karusel, video)?
- Jaký font v grafikách? Sedí s webem, nebo je to Canva výchozí?
- Kde je logo a jak často?
- Co dostává nejvíc reakcí — a jak to vypadá? *(Vizuál, který funguje, je vodítko, ne náhoda.)*

## 3. Rozeslané e-maily

Nech poslat 2–3 poslední e-maily (nebo si je najdi v archivu / v aplikaci).

- **Šířka** a jeden/dva sloupce
- **Font a velikost textu** — a jestli se drží webu
- **Jak vypadá tlačítko** (HTML, nebo obrázek?)
- **Jsou tam obrázky?** Fungují bez načtení obrázků?
- **Podpis a patička** — jednotné, nebo každý jinak?

## 4. Materiály mimo web

Logo (v jakých formátech existuje?), prezentace, PDF, obal e-booku, vizitka, obal videa na YouTube,
grafika do webináře. **Tady se nekonzistence sbírá nejvíc**, protože každý materiál vznikal jinde.

## 5. Knihovna fotek a grafiky

- Kolik **vlastních** fotek existuje a co na nich je?
- Kolik z nich je použitelných (světlo, ostrost, orientace na výšku i na šířku)?
- Je na nich majitel? Klienti? Prostředí?
- Máš k nim popisky, k čemu se hodí? *(V aplikaci pro agenta to drží poznámka u assetu.)*
- **Čeho je málo** → seznam chybějících záběrů pro příští focení.

---

## Jak audit shrnout (výstup)

Tři sloupce, nic víc:

| Zachovat | Sjednotit | Chybí |
|---|---|---|
| co funguje a je rozpoznatelné | co existuje ve víc verzích a má se srovnat na jednu | co vůbec není |

**Příklad:**

- **Zachovat:** noční modrá + zlatá (drží se napříč webem i e-maily), portrétní fotky z Bali.
- **Sjednotit:** tlačítka (na webu tři různá zaoblení), velikost textu v e-mailech (16 vs. 20 px),
  font v grafikách na sítě (Canva výchozí vs. Poppins na webu).
- **Chybí:** pravidla pro prezentace, šablona citátového postu, fotky s klienty, tmavá varianta loga.

Tenhle přehled ukaž majiteli **před** tím, než začneš cokoli navrhovat. Většinou z něj sám vidí,
co ho pálí — a rozhovor se pak vede o rozhodnutích, ne o vkusu.

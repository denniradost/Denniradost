# Sestavovač hlavičky a patičky

> K čemu to je: aby menu a patička žily **na jednom místě** a nekopírovaly se do každé stránky.
> Vzniklo z reálné práce 2026-08-11, kdy měl web šedesát stránek a v každé z nich vlastní kopii
> patičky. Přidat do ní jeden odkaz znamenalo šedesát úprav.
> Naposledy změněno: 2026-08-11.

---

## Proč to není detail

Kopie menu a patičky v každé stránce vypadá neškodně, dokud je stránek pět. Při dvaceti se do nich
přestane sahat, protože každá změna je dvacet úprav. Výsledek se pozná takhle:

> **Na jedné stránce je v patičce odkaz, který na jiné chybí.**

To není nepořádek, to je ztracená důvěra. Návštěvník na jedné stránce najde obchodní podmínky
a na druhé ne.

**Kontrolní otázka:** *„Když teď přidám odkaz do patičky, kolik souborů musím otevřít?“*
Odpověď musí být **jeden**.

---

## Jak to funguje

**1. Části webu bydlí ve vlastních souborech.**

```
sablony/
  hlavicka.html          plovoucí menu s celým rozcestníkem
  paticka.html           velká patička
  hlavicka-logo.html     jen logo, pro nákupní a vstupní stránky
  paticka-strucna.html   jen povinné odkazy
```

**2. Stránka má na jejich místě jen značky.**

```html
<!-- #hlavicka --> <!-- /hlavicka -->
…obsah stránky…
<!-- #paticka -->  <!-- /paticka -->
```

**3. Sestavovač obsah mezi značky doplní.** Pouští se **vždycky před nasazením**:

```bash
python3 sestav.py && python3 oznac-verze.py && <nasazení>
```

---

## Tři věci, které musí sestavovač umět

**Zvýraznit stránku, na které návštěvník je** — a spočítat si to sám z adresy. Nikdy se to
nenastavuje ručně v každé stránce, protože to je zase kopie, která se rozejde.

**Poznat podstránku.** Na `/navody/fapi/` má v menu svítit „Návody“. Porovnání na přesnou shodu
adresy nestačí — musí se testovat i začátek cesty.

**Nechat na pokoji stránku, která značky nemá.** To je funkce, ne opomenutí: takhle se dělá
stránka, která záměrně nemá ani hlavičku, ani patičku.

---

## Ne každá stránka má mít stejnou hlavičku

**Prodejní stránka, objednávka a vstupní stránka menu záměrně nemají.** Odvádělo by pryč od jediné
věci, kterou tam má člověk udělat. Proto druhá varianta šablony:

| Typ stránky | Hlavička | Patička |
|---|---|---|
| Obsahová (domovská, návody, právní) | plné menu | velká, s rozcestníkem a sítěmi |
| Nákupní a vstupní (objednávka, prodejní, magnet) | jen logo, bez odkazů | zkrácená: obchodní podmínky, ochrana údajů, kontakt |

Zkrácená patička není lenost. Na nákupní stránce má být **jen to, co tam být musí** —
zbytek jsou cesty ven.

---

## Co s tím dělá chování (JavaScript)

Rozbalování menu na mobilu patří do **sdíleného souboru** (`js/dm-menu.js`), který si stránka načte.
Nepatří do každé stránky zvlášť — ze stejného důvodu jako styl.

Chování, které patří jen jedné stránce (okno s videem, přihlášení k newsletteru), zůstává v ní.

---

## Kontrolní seznam

- [ ] Hlavička i patička jsou každá ve svém souboru, ne v každé stránce
- [ ] Stránky mají jen značky, obsah doplňuje sestavovač
- [ ] Aktivní položka menu se počítá z adresy, ne nastavuje ručně
- [ ] Na podstránce svítí nadřazená položka
- [ ] Existuje varianta pro nákupní stránky (jen logo, zkrácená patička)
- [ ] Sestavovač se pouští před **každým** nasazením, ne podle nálady
- [ ] Chování menu je ve sdíleném souboru, ne v každé stránce

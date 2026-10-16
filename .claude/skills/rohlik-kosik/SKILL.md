---
name: rohlik-kosik
description: Připraví košík na Rohlik.cz a navrhne termín doručení podle toho, kdy jsme doma (Google Calendar). Použij, když chceme nakoupit na Rohlíku, doplnit košík nebo zopakovat nákup. Objednávku neodesílá.
---

Cíl: za pár minut mít na Rohlíku naplněný košík a navržený termín doručení, který stačí
v aplikaci jen zkontrolovat a odeslat. Řiď se společnými pravidly v `CLAUDE.md`.

Argumenty (volitelné): např. `jako minule + pivo`, `na víkend`, `do pátku`.

## 0. Ověř nástroje
- MCP server `rohlik` musí být připojený (jinak: „spusť `/mcp`, vyber `rohlik`, přihlas se“).
- Google Calendar konektor. Když chybí, zeptej se na termín ručně a pokračuj.
- Načti `domacnost.md` a `seznam.md`.

## 1. Kdy jsme doma
- Projdi kalendáře z `domacnost.md` na příštích 7 dní (nebo období z argumentu).
- Spočítej okna, kdy je doma aspoň jeden dospělý: vezmi „Běžně doma“ a odečti
  události, které podle pravidel z `domacnost.md` znamenají „mimo domov“.
- Události, u kterých nevíš, zda znamenají nepřítomnost, dej do bloku otázek.

## 2. Termín doručení
- Když Rohlík MCP nabízí sloty doručení, vyber 2–3 nejbližší, které padnou do oken
  z kroku 1 (preferuj „Preferovaná okna“), a nejlepší rezervuj/nastav, pokud to jde bez odeslání objednávky.
- Když sloty přes MCP dostupné nejsou, navrhni okna z kroku 1 a řekni, ať slot vyberu v aplikaci.

## 3. Košík
- Základ: `seznam.md` + položky z argumentu. Při „jako minule“ vezmi poslední objednávku
  z Rohlíku a ukaž rozdíly.
- Nabídni (v bloku otázek) věci, které kupujeme pravidelně a dlouho nebyly (historie objednávek).
- Výběr produktu: oblíbené z `domacnost.md` → dřív kupované → nejlevnější za jednotku se slušným hodnocením.
- Přidej do košíku. Hlídej rozpočet a minimální hodnotu objednávky.

## 4. Doptání
Jeden blok otázek (max. ~5), každá s navrženou odpovědí, např.:
> 1. Ve čtvrtek máte „Brno“ celý den – bereme to jako „nejsme doma“? *(navrhuju: ano)*
> 2. Oblíbený jogurt není skladem – vzít Olma bílý? *(navrhuju: ano)*

Po odpovědích uprav košík/termín.

## 5. Výstup
- **Termín:** navržený slot (+ záložní).
- **Košík:** tabulka položka ze seznamu → produkt, množství, cena, poznámka (náhrada/akce).
- **Celkem** a rozdíl vůči rozpočtu.
- Co zbývá udělat v aplikaci (typicky: zkontrolovat a odeslat).

Po potvrzení zapiš `historie/YYYY-MM-DD-rohlik.md` a odškrtni koupené položky v `seznam.md`.
**Objednávku neodesílej**, pokud to výslovně neřeknu.

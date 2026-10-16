---
name: rohlik-kosik
description: Připraví košík na Rohlik.cz, zarezervuje termín doručení podle toho, kdy jsme doma (Google Calendar), a dá odkaz na pokladnu. Použij, když chceme nakoupit na Rohlíku, doplnit košík nebo zopakovat nákup. Objednávku neodesílá.
---

Cíl: za pár minut mít naplněný košík, zarezervovaný termín a odkaz na pokladnu,
kde stačí objednávku odeslat. Řiď se společnými pravidly v `CLAUDE.md`.

Argumenty (volitelné): např. `jako minule + pivo`, `na víkend`, `do pátku`.

## Co Rohlík MCP umí (ověřeno 16. 10. 2026)
- Nástroje jsou z claude.ai konektoru `Rohlik` (`mcp__Rohlik__*`). Funguje i v cloudové session.
- **Objednávku odeslat neumí.** Konec je vždy `get_checkout_link` → odeslání dělám já.
- `get_cart` – obsah košíku; `submitConditionPassed` je false, dokud není vybraný termín.
- `get_typical_order` – nejčastěji kupované položky s frekvencí, mediánem množství, průměrnou
  cenou a datem posledního nákupu. **Nejlepší zdroj návrhů.** Volej bez `add_to_cart`
  (to by přidalo všechno bez ptaní).
- `get_timeslots_checkout` – sloty jen na dnes až 3 dny dopředu (`timeslots_day` 0–3).
  `capacityPercent` 100 neznamená plno (plné sloty mají „NO CAPACITY“ a žádné `slotId`).
  Vždy uveď cenu slotu, pokud není zdarma.
- `reserve_timeslot` – rezervace **vyprší za 60 minut**. Rezervuj až po potvrzení termínu
  a připomeň, do kdy je potřeba objednávku odeslat.
- `add_items_to_cart` – víc položek najednou (`productId`, `quantity`).
- `fetch_orders` s `order_type: upcoming` – ověření, že objednávka odešla.
- Po odeslání jde do objednávky ještě přidávat (Rohlík ukazuje do kdy) – nová položka do košíku
  a při placení „přidat k poslední objednávce“ (`set_checkout_as_suborder`).

## 0. Start
- Načti `domacnost.md` a `seznam.md`, pak `get_cart` (co už v košíku je, nemaž to).
- Když Rohlík nástroje chybí: „připoj konektor Rohlik na claude.ai/customize/connectors a otevři novou session“.

## 1. Návrhy do košíku
- Základ: `seznam.md` + argument. Při „jako minule“ vezmi poslední objednávku (`fetch_orders`).
- `get_typical_order` → seřaď podle frekvence, vyřaď, co už v košíku je (i jinou velikost
  stejného produktu), a nabídni **top 10**.
- U každé položky ukaž množství (medián), cca cenu, kolikrát koupeno a kdy naposledy.

## 2. Kdy jsme doma
- Google Calendar na období, pro které Rohlík nabízí sloty (dnes až +3 dny).
- Události s místem mimo domov / celodenní cesty = nejsme doma. Uveď je u návrhu termínu.

## 3. Doptání – formou výběru, ne textem
Použij `AskUserQuestion` (dobře se ovládá i na mobilu):
- **Položky:** multiSelect, rozdělit do 2–4 otázek podle kategorií (max 4 možnosti na otázku),
  emoji v nadpisu, popisek: „cca X Kč · koupeno N×, naposledy D. M.“.
- **Termín:** single select, 3 návrhy podle kalendáře + „zatím nerezervovat“, doporučený první.
- Odpověď může být i vlastní text (např. „zítra 7–8“) – respektuj ji.

## 4. Dokončení
1. `add_items_to_cart` s vybranými položkami.
2. `reserve_timeslot` na zvolený slot.
3. `get_checkout_link` a krátké shrnutí: termín (+ do kdy platí rezervace), košík
   (co už tam bylo / co je nové), celková cena, odkaz.
4. Po „odesláno“: ověř přes `fetch_orders` (upcoming), zapiš `historie/YYYY-MM-DD-rohlik.md`
   (číslo objednávky, termín, položky, cena – **bez adresy**) a odškrtni koupené v `seznam.md`.

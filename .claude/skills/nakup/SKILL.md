---
name: nakup
description: Naplní košík na Rohlik.cz podle seznam.md a preference.md. Použij, když chci nakoupit, doplnit košík nebo zopakovat nákup.
---

Postupuj podle sekce „Jak nakupovat" v `CLAUDE.md`.

Argumenty (volitelné): položky navíc nebo pokyn, např. `/nakup jako minulý týden + pivo`.
- „jako minule" / „zopakuj" → vezmi poslední objednávku z historie na Rohlíku jako základ
  a ukaž rozdíly oproti `seznam.md`.
- Položky v argumentu přidej k `seznam.md` jen pro tenhle nákup.

Nejdřív ověř, že MCP server `rohlik` je připojený. Pokud ne, napiš mi, ať spustím `/mcp`,
vyberu `rohlik` a přihlásím se.

Na konci vypiš tabulku košíku a celkovou cenu a **nečekej na nic jiného než moje potvrzení** –
objednávku sám neodesílej.

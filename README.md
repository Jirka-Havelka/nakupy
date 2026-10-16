# nakupy

Osobní nákupní agent pro Rohlik.cz postavený na Claude Code a [oficiálním Rohlík MCP serveru](https://www.rohlik.cz/stranka/mcp-server)
+ statický přehled cen (`index.html`).

## Zprovoznění
1. V tomhle adresáři spusť `claude`. Server `rohlik` se načte z `.mcp.json` (potvrď důvěru).
2. Spusť `/mcp`, vyber `rohlik` a přihlas se svým účtem Rohlíku (OAuth).
3. Vyplň `preference.md` a `seznam.md`.
4. Napiš `/nakup` (nebo třeba `/nakup jako minule + pivo`).

Agent naplní košík a vypíše shrnutí. Objednávku a platbu dokončuješ sám v aplikaci Rohlíku.

## Bez kódu
Stejný server jde přidat i v Claude Desktop / claude.ai: Nastavení → Konektory → Přidat vlastní
konektor, název `Rohlik`, URL `https://mcp.rohlik.cz/mcp`.

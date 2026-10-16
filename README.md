# nakupy

Agenti pro domácí nákupy postavení na Claude Code. Zatím jeden:

| Agent | Příkaz | Co dělá |
|---|---|---|
| Rohlík – košík | `/rohlik-kosik` | Navrhne top 10 často kupovaných věcí, z kalendáře zjistí, kdy jsme doma, zarezervuje termín a dá odkaz na pokladnu. Neobjednává. |

## Zprovoznění
1. Na https://claude.ai/customize/connectors připoj konektor `Rohlik` (URL `https://mcp.rohlik.cz/mcp`)
   a Google Calendar.
2. Otevři session nad tímhle repem (Claude Code na webu/mobilu i lokálně – konektory se načtou samy).
3. `/rohlik-kosik` (např. `/rohlik-kosik jako minule + pivo`).

## Přidání dalšího agenta
Nový skill v `.claude/skills/<obchod>-<úloha>/SKILL.md`, sdílený kontext bere z `domacnost.md`,
společná pravidla z `CLAUDE.md`. Řádek do tabulky výše.

Staré věci jsou v `archiv/` (kandidáti na smazání).

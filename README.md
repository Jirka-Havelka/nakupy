# nakupy

Agenti pro domácí nákupy postavení na Claude Code. Zatím jeden:

| Agent | Příkaz | Co dělá |
|---|---|---|
| Rohlík – košík | `/rohlik-kosik` | Zjistí z kalendáře, kdy jsme doma, navrhne termín doručení, připraví košík, doptá se. Neobjednává. |

## Zprovoznění
1. Lokálně v tomhle adresáři spusť `claude` (server `rohlik` se načte z `.mcp.json`, potvrď důvěru).
2. `/mcp` → `rohlik` → přihlásit se účtem Rohlíku.
3. Google Calendar: když jsi v Claude Code přihlášený účtem claude.ai s připojeným Google Calendar
   konektorem, je dostupný i tady (ověř v `/mcp`).
4. Vyplň `domacnost.md`, pak `/rohlik-kosik` (např. `/rohlik-kosik jako minule + pivo`).

## Přidání dalšího agenta
Nový skill v `.claude/skills/<obchod>-<úloha>/SKILL.md`, sdílený kontext bere z `domacnost.md`,
společná pravidla z `CLAUDE.md`. Řádek do tabulky výše.

Staré věci jsou v `archiv/` (kandidáti na smazání).

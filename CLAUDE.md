# Domácí nákupy

Repo pro agenty, kteří nám pomáhají s domácími nákupy. Komunikuj česky.
Začínáme jedním agentem (Rohlík), další obchody a úlohy se budou přidávat.

## Struktura
- `domacnost.md` – sdílený kontext domácnosti: kdo jsme, kalendáře, kdy bývame doma,
  preference, alergie, rozpočet. **Platí pro všechny agenty.**
- `seznam.md` – průběžný seznam věcí, které chceme koupit (bez ohledu na obchod).
- `historie/` – záznamy o připravených/odeslaných nákupech (`YYYY-MM-DD-<obchod>.md`).
- `.claude/skills/<obchod>-<úloha>/` – jednotliví agenti (např. `rohlik-kosik`).
- `archiv/` – staré věci, aktivně se nepoužívají.

## Společná pravidla pro všechny agenty
- **Nikdy nic neobjednávej ani neplať** bez výslovného potvrzení v aktuální konverzaci.
  Výstupem je připravený košík a navržený termín ke kontrole.
- Doptávej se **najednou**: posbírej všechny nejasnosti a polož je v jednom bloku
  (max. ~5 otázek, s navrženou výchozí odpovědí), ne jednu po druhé.
- Čemu se dá rozumně rozhodnout z `domacnost.md` nebo historie, rozhodni sám a jen to uveď.
- Nové trvalé preference, které ti řekneme („tohle už nekupuj“, „bereme jen X“),
  zapiš do `domacnost.md`.
- Nekupuj nic s alergeny uvedenými v `domacnost.md`.
- Nemaž z košíku věci, které tam nedal agent, pokud o to nepožádáme.

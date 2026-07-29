# CLAUDE.md - repo webu skladka-molitorov

## Klíčová fakta

- **Veřejná adresa webu: https://skladka-molitorov.cz** - výhradně tuto uvádět v článcích, dokumentech i sdílených odkazech. `skladka-molitorov.github.io` je jen název repa/hosting.
- Stack: MkDocs + Material theme, čeština. Deploy: GitHub Actions (`.github/workflows/static.yml`) publikuje **předgenerovaný adresář `site/`** - po každé změně v `docs/` nebo `mkdocs.yml` je nutné lokálně spustit `mkdocs build` a commitnout i `site/`.
- Kontext kauzy (skládka Molitorov, Kouřim) je v druhém repu `spolek`: číst `spolek/KONTEXT.md` a `spolek/CLAUDE.md`.

## Struktura

| Cesta | Obsah |
|---|---|
| `mkdocs.yml` | Konfigurace (nav, blog plugin, theme) |
| `docs/index.md` | Úvodní stránka |
| `docs/souhrn.md` | Souhrn kauzy |
| `docs/casova-osa.md` | Časová osa událostí - doplňovat při každém novém podání/odpovědi |
| `docs/o-webu.md` | O webu |
| `docs/info/prispevky/` | Blogové články, formát `YYYY-MM-DD-slug.md` (plugin blog, kategorie: Skládka, Město, Petice, KÚ, KHS, MŽP, DPP, Praha, Podání) |
| `docs/assets/info/files/` | Přílohy: PDF podání (zadost-106-*), protokoly KÚ (`106_ku/`), 106 z 27. 7. (`106_20260727/`), zápisy ZM, výřezy ÚP, petice, situační mapka |
| `docs/assets/img/`, `docs/assets/video/` | Fotky a videa z místa |
| `site/` | Vygenerovaný web (needitovat ručně) |

## Postup při novém článku

1. Vytvořit `docs/info/prispevky/YYYY-MM-DD-slug.md` (frontmatter s date a categories dle existujících článků).
2. Přílohy do `docs/assets/info/files/`.
3. Případně doplnit `docs/casova-osa.md`.
4. `mkdocs build` a commit včetně `site/`.

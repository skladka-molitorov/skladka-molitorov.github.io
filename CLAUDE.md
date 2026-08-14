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
| `docs/pribeh/index.html` | „Příběh skládky" - interaktivní veřejná osa s vrstvami a grafem. **Needitovat ručně**: generuje se v repu spolek (`mapa-vztahu/generuj_osu_web.py` z `data/08-osa-web.yaml`) a sem se jen kopíruje; v nav vedena absolutní URL |
| `docs/o-webu.md` | O webu |
| `docs/info/prispevky/` | Blogové články, formát `YYYY-MM-DD-slug.md` (plugin blog, kategorie: Skládka, Město, Petice, KÚ, KHS, MŽP, DPP, Praha, Podání) |
| `docs/assets/info/files/` | Přílohy: PDF podání (zadost-106-*), protokoly KÚ (`106_ku/`), 106 z 27. 7. (`106_20260727/`), zápisy ZM, výřezy ÚP, petice, situační mapka |
| `docs/assets/img/`, `docs/assets/video/` | Fotky a videa z místa |
| `site/` | Vygenerovaný web (needitovat ručně) |

## Postup při novém článku

1. Vytvořit `docs/info/prispevky/YYYY-MM-DD-slug.md` (frontmatter s date a categories dle existujících článků).
2. Přílohy do `docs/assets/info/files/`.
3. Případně doplnit `docs/casova-osa.md` - **a při každé úpravě časové osy zvážit i doplnění „Příběhu skládky"** (viz níže). Je-li událost vhodná pro laiky, doplnit vždy.
4. `mkdocs build` a commit včetně `site/`.

## Příběh skládky - aktualizace (docs/pribeh/index.html)

Zdroj dat je v repu **spolek**, tady se jen přijímá vygenerované HTML. Postup:

1. V repu spolek doplnit událost do `mapa-vztahu/data/08-osa-web.yaml` (laický text 1-2 věty, č. j. do `detail`, odkaz jen na publikovaný obsah webu - **ne na draft články**; embarga a nedoložené věci `skryto: true` - pravidla v hlavičce souboru).
2. `python3 mapa-vztahu/generuj_osu_web.py --kontrola`, pak `--vystup <toto-repo>/docs/pribeh/index.html`.
3. V tomto repu `mkdocs build` a commit včetně `site/`.

**Ruční kroky Zdeňka vždy explicitně vypsat na konci odpovědi** (sandbox je nesmí/neumí): `git commit` + `push` v obou repech; pokud Claude stavěl web v sandboxu přes /tmp (nemůže mazat v `site/`), doporučit před commitem lokální `mkdocs build` na vyčištění starých souborů.

Čekající úpravy příběhu (stav 14. 8. 2026): odkrýt `skryto` u ČIŽP/dodatku 101134 (po konci embarga ~15. 9.); k darům doplnit data podpisů a usnesení o přijetí z odpovědi na doplňující 106 na město; po publikaci draft článku `2026-08-12-odpoved-khs` přesměrovat provizorní odkaz u události k-khs-2026 (komentář v YAML); aktualizovat událost f-vklad-2026 po rozhodnutí katastru (lhůta 18. 8.). Článek o limitu publikován 14. 8. (`2026-08-14-limit-10000-tun`), odkazy v příběhu přesměrovány.

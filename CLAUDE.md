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

Čekající úpravy příběhu (stav 17. 8. 2026):

- odkrýt `skryto` u ČIŽP/dodatku 101134 - **po konci embarga ~15. 9.**;
- k darům doplnit data podpisů a usnesení o přijetí z odpovědi na doplňující 106 na město (odchází do 20. 8.);
- aktualizovat událost `f-vklad-2026` po rozhodnutí katastru o vkladu V-6690/2026 (**lhůta 18. 8.**);
- po publikaci článku o družicových snímcích (embargo do prvních dnů září) doplnit událost k rozsahu plochy a odkaz.

Hotovo: článek o limitu publikován 14. 8. (`2026-08-14-limit-10000-tun`), článek o hygieně 17. 8. (`2026-08-17-odpoved-khs`) - **odkaz u události `k-khs-2026` už na něj míří**, provizorní cíl přesměrován. Článek o zamítnutém podnětu MHMP publikován 18. 8. (`2026-08-18-magistrat-zamitl-podnet`, commit `f233d24`) - v Příběhu k němu vznikla událost `k-mhmp-podnet-2026` ve vrstvě Kontroly a **opraven duplicitní klíč `odkaz_text` u `k-khs-2026`** (zobrazovalo se „Časová osa s dokumenty" místo názvu článku). Reakce na článek Novinky.cz publikována 19. 8. (`2026-08-19-molitorov-na-novinkach`) - v Příběhu k ní vznikla **nová vrstva `media` („Kauza v médiích", #ad1457)** a v ní událost `m-novinky-2026` k datu **16. 8.** Vrstva je zatím jednoprvková, počítá se s Blažkovým textem; pokuta ČIŽP v události není (pravidlo v hlavičce `08-osa-web.yaml`).

Publikované články k 22. 8. 2026 (nepřepisovat zpětně, nové zprávy jako nové články): odpověď živnostenského úřadu 10. 8., plnění usnesení 45/2026 11. 8., odpověď města a stavebního úřadu 12. 8., zveřejnění dokumentů městem 13. 8., limit 10 000 tun 14. 8., odpověď KHS 17. 8., zamítnutý podnět MHMP 18. 8., reakce na článek Novinky.cz 19. 8. (`2026-08-19-molitorov-na-novinkach`; v časové ose k němu vznikla položka u data **16. 8.**, tedy u vydání článku, ne u naší reakce), pozvánka na zasedání ZM 22. 8. (`2026-08-22-zasedani-26-srpna`, commit `50ea5ba`, obrázek úřední pozvánky v `docs/assets/img/20260826-pozvanka-zm-kourim.png`, odkaz doplněn do bloku 26. 8. v časové ose; v Příběhu skládky událost **nevznikla** - pozvánka není událost kauzy). Opravy silnice III/33420 publikovány 23. 8. (`2026-08-23-silnice-kourim-molitorov`) - vydáno o dva dny dřív než plánovaných 25. 8., protože blokátor padl odesláním 106 na KSÚS a na 25. 8. míří článek o pokutě ČIŽP. V časové ose vznikl blok k 23. 8., v Příběhu skládky událost `o-silnice-2026` ve vrstvě „Občané se brání" (celkem 68 událostí). **Ceny a čísla objednávek nejsou ověřeny proti registru smluv**, jen proti interní rešerši z 22. 8. - viz `PUBLIKOVANO.md` ve `verejnost/web_k_publikaci/_vydane/silnice-kourim-molitorov/` v repu spolek.

**Pozor na URL článků:** blog plugin staví cesty jako `/info/RRRR/MM/DD/<slug>/`, ne `/info/prispevky/<slug>/`. Při odkazování na článek zvenčí (Facebook, podání, e-mail novinářům) používat tvar podle data, například `https://skladka-molitorov.cz/info/2026/08/22/2026-08-22-zasedani-26-srpna/`.

**Souhrn aktualizován 23. 8. 2026** na stav k témuž dni. Opravena věcná chyba (tvrdil, že o povolení požádala jako jediná ŠTOCHL GROUP recyklace - žadateli jsou dvě firmy, INVEST v SZ_130814 a RECYKLACE v SZ_130820), doplněno zamítnutí podnětu Magistrátem ze 14. 8., zveřejnění tří dokumentů městem 13. 8., nový oddíl „Kauza v médiích a rozbitá silnice" (Novinky 16. 8. + opravy silnice) a lhůty 8. 9. a 23. 9. Petice přepsána do minulého času. **OPRAVA téhož dne po upozornění Zdeňka: oddíl o roli města porušoval kázeň z 13. 8.** Věta o tom, že třicetidenní lhůta uplynula 7. 8. a na úřední desce k tomu nebyla žádná informace, kladla vedle sebe uplynulou lhůtu a prázdnou desku, čímž z nezveřejnění dělala zmeškání. **Bod V. usnesení 45/2026 přitom stanoví třicetidenní lhůtu jen pro bod II. odst. 2 až 5 a odst. 7, pro bod II. odst. 1 (vyžádání a zveřejnění informací o povoleních) lhůtu nestanoví** - viz `zastupitelstvo/20260813-zverejneni-plneni-45-2026/analyza-zverejneni-20260813.md` oddíl II. Oddíl přepsán tak, že obě skupiny úkolů rozlišuje, a těžiště přesunuto z včasnosti na obsah: k povolení dle § 21 zákona o odpadech a k povolenému rozsahu město nezveřejnilo nic. Stejně opravena otevřená otázka na město v závěru stránky.

**Druhá revize souhrnu téhož dne (Zdeněk zadal přečíst celou stránku a ověřit tvrzení).** Čtyři opravy: (1) vypuštěno **"jednatelé ŠTOCHL GROUP firem jsou bratři"** - doložené je jen totožné datum narození 27. 10. 1978 v OR, rodinný vztah doložen není a README podnětu na FÚ ho 18. 8. výslovně zamítl; (2) **"27 metrů navýšení terénu na ploše 32 603 m²" rozděleno na dva údaje** - 32 603 m² je rozsah řešeného území dle EIA a plocha, na kterou se vztahuje dodatečné povolení, **není to plocha navážky** (kázeň Zdeňka z 22. 8., v hlavičce `08-osa-web.yaml`); (3) Reality Molitorov už není "bez příjmů z nájmu", ale s přesným výčtem po letech včetně **95 tis. Kč za rok 2022** (táž oprava proběhla 16. 8. v podnětu na FÚ); (4) srovnány rozpory "čtvrtým rokem" proti "od roku 2022" - nahrazeno neurčitým "několik let" a doplněno, že vegetační kryt mizí na družicových snímcích od května 2020 a dodatečné povolení je ze srpna 2021. Dále upravena položka o povolení MHMP 1517437/2023, kde stálo "kopii jsme si vyžádali" - Magistrát provozní řády poskytl 11. 8. 2026 (MHMP 794441/2026). **Ponecháno beze změny:** odhad krajského úřadu ~640 000 tun (pochází z protokolů, Zdeněk potvrdil) a otázka na Metrostav a DPP, kolik materiálu z metra skončilo v Molitorově (rozhodnutí DPP z 3. 8. pokrývá jen 7,6 tis. t z roku 2021, což na odpověď nestačí). **Do souhrnu vědomě NEBYLA dána pravomocná pokuta ČIŽP** - na webu nikde není a její první publikací má být článek 25. 8., jehož spouštěčem je odeslání podnětu MHMP k § 25, který zatím napsaný není. Otevřená otázka „co ČIŽP udělala s protokoly" proto v souhrnu zůstává. Nedány tam ani žádosti na NSA a MŠMT k dotacím (linka dosud nepublikovaná) a oba podněty finanční správě (o těch se veřejně nemluví). **Souhrn se bude přepisovat znovu po 25. 8.** - přibude pokuta, odpovědi města a kraje a výsledek zastupitelstva.

**Úvodní stránka `docs/index.md` aktualizována 23. 8. 2026** ze stavu k 11. 8. **Peticiní box přepsán do minulého času** (sběr skončil 20. 8., po sečtení se petice předá kraji) - dřív vyzýval k podpisu. **Stavový box přepsán celý:** vyhozena věta, že lhůta usnesení 45/2026 uplynula 7. 8. a město nezveřejnilo nic (táž vada jako v souhrnu, viz výše - lhůta dopadá jen na bod II. odst. 2 až 5 a odst. 7, a město 13. 8. zveřejnilo), doplněno zamítnutí podnětu Magistrátem, zveřejnění města, silnice, Novinky a zasedání 26. 8. jako první položka. **V úvodním odstavci opraveny podhodnocené údaje** - stálo tam "odhadem tisíce tun materiálu a navážku vysokou desítky metrů", nahrazeno doloženými 425 389 t a až 27 metry dle PD. **Sjednocena vzdálenost k nejbližším domům na 300 až 400 m** (index dřív uváděl 400-1300 m, souhrn 300-400 m).

**Neopravené vady časové osy (stav 23. 8. 2026):** budoucí termíny jsou v nesprávném pořadí, 25. 8. stojí před 20. 8., a blok 20. 8. je stále veden jako budoucí (`tl-budouci`), přestože datum minulo. Články z 27. a 29. 7. pořád vyzývají k podpisu petice „do 20. srpna" (v souhrnu už opraveno). Vypořádá to petiční článek po sečtení podpisů, plánovaný po 24. 8. Drafty čekající na vydání jsou v repu spolek ve `verejnost/web_k_publikaci/`, vydané v jeho podsložce `_vydane/` - **do `docs/` se kopírují teprve v den publikace** (MkDocs kopíruje celé `docs/assets/` do `site/`, takže příloha nevydaného článku by byla živá na doméně).

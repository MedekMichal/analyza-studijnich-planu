# Server API endpoints

- `GET /{$}`
    - PARAM: žádné
    - domácí stránka = zvolený plán / vyhledávání
        - defaultně zvolený plán, pokud nemá, tak redirect na /search
    - detail plánu buď rovnou, nebo detaily lazy load
        - pro lazy load jsou potřeba další endpointy
- `GET /search`
    - PARAM: aktivni filtry + textový input, plán pro porovnání
    - výsledky vyhledávání plánů + aktualizované filtry
    - target musí být content
        - lze se sem dostat z /{$} nebo z detailu plánu
- `GET /search-by-code`
    - PARAM: aktivni filtry + textový input, kódy předmětů (, plán pro porovnání)
    - výsledky vyhledávání plánů podle kódů předmětů + relevantní předměty + aktualizované filtry
    - target musí být content
- `GET /plan/{code}`
    - PARAM: kód plánu (unikátní identifikátor)
    - zobrazení libovolného plánu
    - detail plánu buď rovnou, nebo detaily lazy load
        - pro lazy load jsou potřeba další endpointy
- `PATCH /user-plan/{code}`
    - PARAM: kód plánu (unikátní identifikátor)
    - uloží zobrazený plán jako zvolený
- `DELETE /user-plan`
    - PARAM: žádné
    - smaže informaci o zvoleném plánu uživatele
- `GET /compare/{code1}/{code2}`
    - PARAM: kód plánu 1, kód plánu 2
    - zobrazení porovnání dvou plánů
- `POST /assign-plan` (bude parametr z bp balíčku)
    - PARAM: kód plánu, přepsat/přidat
    - přiřadí doporučený průběh ze zvoleného plánu do uživatelova BP
    - lze rozdělit do dvou endpointů - přepsat a přidat
- `PUT /survey/rating/{rating}`
    - PARAM: hodnocení, kód plánu
    - uložení hodnocení plánu
- `PUT /survey/feedback`
    - PARAM: textová zpětná vazba, kód plánu
    - uložení zpětné vazby k plánu
- `DELETE /survey/rating`
    - PARAM: kód plánu
    - smazání hodnocení plánu
- `DELETE /survey/feedback`
    - PARAM: kód plánu
    - smazání zpětné vazby k plánu
- originální potřebné endpointy z RecSIS
    - add to BP, default 404

# Data

Celkový předpoklad:
- načtou se všechny plány co jsou aktivní na MFF
    - `select * from plany where obor in (select obor from fdoparam where splati is not null)`
    - přidají se vhodné filtry
- pro všechny plány se načtou data pomocí `study_plan.stud_plan(plan_code, year)` (rok nejnovější)
    - povinnosti, skupiny, doporučené průchody, atd.
- načtou se tabulky pro zobrazení metadat plánu
    - `plany`, `obor`, `nobor`, `fdoparam`
- načtou se tabulky pro zobrazení rekvizit
    - `preq`, `povinn`, `pskup`
- načtou se statistiky o studentech

Tato data se transformují do lokální databáze (PostgreSQL) RecSISu v ELT procesu.
Vypočítají se potřebné informace pro rychlé zobrazení:
- kreditové statistiky

V lokální databázi RecSISu se vytvoří tabulky pro ukládání:
- uživatelských dat
    - zvolený plán uživatele (nullable)
    - historie zobrazených plánů
- dat o plánech
    - hodnocení
    - komentáře

Doporučené předměty ke státnicím
- na tom se pracuje

# RecSIS struktura

všechny balíčky reprezentující stránku mají jednotnou strukturu:
- `view.templ` - frontend šablona
- `server.go` - router s handlery a jejich logikou
- `database.go` - databázové operace volané ze serveru
- `model.go` - datové struktury naplňované z databáze s jejich metodami
- `texts.go` - textové konstanty používané na stránce (lokalizace)

Někde je navíc:
- `search.go` - logika pro vyhledávání a filtrování pomocí Meilisearch

`server.go` obsahuje interfaces:
- ty jsou injektovány z `main.go`
- jsou v `Server` struktuře

# UC-001: Upozornění na rekvizity ve vlastním plánu

Jedná se o rozšíření upozornění na stránce vlastního plánu (= blueprint) v systému RecSIS.
Samotné zobrazení je už implementováno, stačí doplnit logiku pro kontrolu rekvizit a generování textu upozornění.
- balíček: `blueprint`, soubor: `webapp/blueprint/server.go`, funkce: `generateWarnings`

Data:
- tabulka `preq` - seznam rekvizit pro předměty
- tabulka `povinn` - předměty
    - sloupec `pskupina` - informace o tom, zda předmět zastupuje skupinu
- tabulka `pskup` - předmětové skupiny
- je vhodné načíst rekurzivní rekvizity rovnou k předmětu v ELT procesu
    - rekurzivní SQL dotaz
    - kontrolovat platnost pomocí sloupců 
        - `preq`: `ReqOd`, `ReqDo`
        - `pskup`: `PSOd`, `PSDo`
    - rekvizity se spárují s předmětem co je naplňuje v tabulce `povinn`
    - pokud libovolný předmět realizující rekvizitu má sloupec `pskupina == 'M'` (malá skupina), tak
        - nahradí se disjunkcí rekvizit z tabulky `pskup`
        - zkontroluje se, zda jsou tyto rekvizity platné pomocí sloupců `PSOd` a `PSDo`
        - rekvizity se spárují s předmětem co je naplňuje v tabulce `povinn`
        - tento krok se opakuje, dokud `pskupina IS NULL` (nebo `pskupina == 'V'`, což ale není používáno = ignorujeme tyto předměty)

Při načtení vlastního plánu se pro každý předmět:
1. načtou jeho prerekvizity, korekvizity a neslučitelnosti ze stejné tabulky
2. proběhne kontrola rekvizit
    - pro prerekvizity se zkontroluje, jestli je splňuje nějaký předmět naplánovaný v předchozích semestrech
    - pro korekvizity se zkontroluje, jestli je splňuje nějaký předmět naplánovaný ve stejném nebo předchozích semestrech
    - pro neslučitelnosti se zkontroluje, jestli je nesplňuje nějaký předmět naplánovaný v stejném nebo předchozích semestrech
3. pokud nějaká rekvizita není splněna, zobrazí se u předmětu:
    - ikona červeného vykřičníku
    - při najetí myší na ikonu se zobrazí detailní informace o nesplněných podmínkách s informacemi o tom, které předměty je můžou splnit

Pravidla:
- Prerekvizity - seznam předmětů, které musí mít student splněné, aby bylo možno provést zápis
- Korekvizity - seznam předmětů, které musí mít student zapsány nejpozději současně s daným předmětem
- Neslučitelnost - seznam předmětů, které nesmějí být zapsány současně nebo před daným předmětem

**Složitost**: střední
**Přínos**: střední
**Priorita**: vysoká

# UC-002: Vyhledávání plánů podle názvu
# UC-003: Vyhledávání plánů podle kódů
# UC-004: Filtrování plánů

Tyto požadavky budou řešeny společně, protože se jedná o kombinaci funkcí na stránce vyhledávání plánů.
Je potřeba implementovat FE:
- soubor `webapp/degreeplan/view.templ`
- design viz `wireframe.pdf`
V serveru je potřeba implementovat handler:
- soubor `webapp/degreeplan/server.go`
- endpoint `GET /search`

K filtrování i vyhledávání lze použít:
- SQL
    - pomalé a neškálovatelné
    - není to search engine
- Meilisearch
    - search engine
    - používá se v RecSISu
    - existuje infrastruktura
    - bude se používat

Je potřeba získat data o plánech:
- v elt procesu je potřeba přidat
    - tabulku `plany` s metadaty plánu
    - tabulku `obor` s informacemi o oborech
    - tabulku `nobor` s informacemi o oborech SIMS
    - tabulku `fdoparam` s informacemi o platnosti oboru
    - filtrované na relevantní plány
- seznam plánů:
    - získat pomocí: `select * from plany where obor in (select obor from fdoparam where splati is not null)`
    - omezit se na:
        - MFF UK (fakulta = 11320)
        - bakalářské a navazující magisterské programy
        - jazyk česky a anglicky
- data o studijních plánech pomocí package `study_plan.stud_plan(plan_code, year)`:
    - všechny kódy ze seznamu plánů
    - rok vždy jen nejnovější

Je třeba definovat filtry:
- fakulta (MFF)
    - `plany.fakulta`
- oblast vzdělávání (informatika, matematika, fyzika)
    - nejjednodušší je vzít kód oboru
        - pokud je 3. písmeno `U` pak učitelský obor
        - jinak podle prvního písmena
            - `I` = informatika
            - `M` = matematika
            - `F` = fyzika
        - identicky kód plánu, první písmeno je `N` = MFF, druhé písmeno podle oblasti vzdělávání
            - `I` = informatika
            - `M` = matematika
            - `F` = fyzika
            - `U` = učitelský obor
        - toto je konvence (ne pravidlo), ale dodržuje se na 100 %
    - u plánů je katedra
        - Jedelský: "To spíše náhodou může být plán příslušný k jedné katedře, ale obecně to tak není."
    - existuje filtr na oblast vzdělávání???
        - zjistit jak to získat, která tabulka to definuje a jak to navázat na plán
- druh studia (bakalářský, navazující magisterský)
    - `plany.druh`
- jazyk (čeština, angličtina)
    - `obor.jazyk`
- rok platnosti plánu
    - `plany.LOd` a `plany.LDo`
- obor
    - `plany.obor` = kód oboru
    - název v tabulce `obor`
- obor SIMS
    - `plany.oborSIMS` = kód oboru SIMS
    - název v tabulce `nobor`

U filtrů zobrazit počet odpovídajících plánů, pokud to dává smysl.

Vyhledávání je možné podle:
- názvu plánu (neunikátní)
    - `plany.nazev`
- kódu plánu (unikátní identifikátor)
    - `plany.kod`

U výsledků zobrazit:
- kód plánu (odkaz na detail `GET /plan/{code}`)
    - `plany.kod`
- název plánu (odkaz na detail `GET /plan/{code}`)
    - `plany.nazev`
- druh studia
    - `plany.druh`
- obor?
    - není nutné
    - `plany.obor` jen kód
- platnost od - do
    - `plany.LOd`, `plany.LDo` (alternativně `DOd`, `DDo` = datum)
- možnost vybrat pro porovnání

Vždy zobrazovat nějaké výsledky nebo informaci, že nic neodpovídá.
Pro víc výsledků než se vejde na stránku, implementovat stránkování (nebo nekonečný scroll).
- má smysl stránkovat, když uživatel prakticky musí vyhledávat nebo hodně filtrovat?
- nezajímají nás všechny plány, ale jen konkrétní

**Složitost**: vysoká
**Přínos**: vysoký
**Priorita**: vysoká

# UC-005: Zobrazení plánu

Je potřeba implementovat FE:
- soubor `webapp/degreeplan/view.templ`
- design viz `wireframe.pdf`
V serveru je potřeba implementovat handler:
- soubor `webapp/degreeplan/server.go`
- endpoint `GET /plan/{code}`

Samotné zobrazení povinných a povinně volitelných skupin již implementuje RecSIS.
- použít již existující infrastrukturu
- přidat název plánu a pokud plán není platný tak rozsah let platnosti
    - v tabulce `plany` všechna potřebná data
- u názvu svítí ikona, pokud je to zvolený plán uživatele
Je potřeba získat (ELT proces) a používat pouze aktuální data o studijních plánech:
- pomocí package `study_plan.stud_plan(plan_code, year)` se získají nejnovější data o plánech:
    - rok vždy jen nejnovější
- je možné použít `study_plan.stud_plan_tree(plan_code, year)` pro získání stromové struktury plánu
    - bohužel tato funkce nedává u všech plánů správné výsledky

Upravit databázi:
- uživatel má zvolený plán
    - pokud je sloupec `NULL`, tak uživatel nemá zvolený plán
- není potřeba ukládat rok, protože vždy se použijí nejnovější data

Ostatní detaily plánu jsou rozepsané v use-casech:
- UC-006: Úvodní text u plánu
- UC-007: Kreditové statistiky u detailu plánu
- UC-008: Detail předmětu v zobrazeném studijním plánu
- UC-013: Zobrazení statistik o studentech plánu
- UC-016: Zobrazení předmětů doporučených ke státnicím
- UC-017: Zobrazení mapy rekvizit
- UC-021: Zobrazení doporučeného průchodu plánu

Co je možné dělat v detailu plánu je popsáno v use-casech:
- UC-014: Procházení hodnocení a komentářů plánů
- UC-012: Označení plánu za zvolený
- přejít na vyhledávání plánů `GET /search`
- porovnat s jiným plánem `GET /search` s zobrazeným plánem jako parametr pro porovnání

**Složitost**: střední
**Přínos**: vysoký
**Priorita**: vysoká

# UC-006: Úvodní text u plánu

U detailu plánu je možné zobrazit úvodní text.
Tento text by byl napsán ručně ve dvou variantách
- pro bakalářské studium
- pro navazující magisterské studium

Text bude obsahovat informace o:
- na co je důležité si dát pozor
    - stihnout projekt a práci
    - práce lze navázat na projekt
    - existují doporučené předměty ke státnicím
- doporučený harmonogram studia
    - pro bakalářské studium 3 roky
    - pro navazující magisterské studium 2 roky
- jak všechno stihnout
- hardcoded odkazy na užitečné zdroje
    - Karolínka, ...
- definice plánu
    - P a PV skupiny
    - státnice (a jejich doporučené předměty)
    - projekt a práce
- je platné pouze pro plány na Informatice
    - jak odlišit
    - je možné sepsat texty a ty ručně přiřadit k plánům

**Složitost**: nízká
**Přínos**: nízký
**Priorita**: nízká

# UC-007: Kreditové statistiky u detailu plánu

Tímto je myšleno zobrazení počtu:
- celkových kreditů
- povinných kreditů
- povinně volitelných kreditů
- kolik zbývá

celkový počet kreditů
- bc = 180
- nmgr = 120

počty povinných kreditů
- sečtou se kredity všech předmětů v povinných skupinách
- sečtou se limity všech povinných skupin

počty povinně volitelných kreditů
- sečtou se limity všech povinně volitelných skupin
- toto je nutné dělat na nejvyšší úrovni, protože některé PV skupiny mají podskupiny

použít databázovou package `study_plan`:
- funkce `study_plan.stud_plan(plan_code, year)` vrací seznam předmětů s jejich kredity
- funkce `study_plan.stud_plan_tree(plan_code, year)` vrací stromovou strukturu plánu s limity skupin 
    - problém je, že v SIS datech je stromová struktura často chybná
    - aktuálně jsou data duplikátní
    - typicky je limit na více skupin najednou
    - možné řešení je udělat reverzní inženýrství
        - vzít skupiny, zjistit které patří do kterých nadřazených skupin (pomocí vlastní podmnožiny předmětů)
        - nakonec počítat jen neobsažené skupiny
        - tedy kredity na nejvyšší úrovni

vše je možné předpočítat při načtení plánu a uložit do databáze:
- tabulka `plany` přidat sloupce:
    - `TotalCredits` - celkové kredity plánu
    - `MandatoryCredits` - povinné kredity plánu
    - `ElectiveCredits` - limit povinně volitelných kreditů plánu

V datech existuje informace o procentu volitelných kreditů za úsek studia
- `plany` sloupec `ProcKredVP`

**Složitost**: střední
**Přínos**: vysoký
**Priorita**: střední

# UC-008: Detail předmětu v zobrazeném studijním plánu

Většina věcí je již implementována v RecSISu.
Je potřeba doplnit:
- zvýraznění předmětů doporučených ke státnicím

Zdali je předmět doporučen ke státnicím se řeší v UC-016.

**Složitost**: nízká
**Přínos**: vysoký
**Priorita**: vysoká

# UC-009: Zobrazení rozdílů mezi dvěma plány
# UC-010: Zobrazení společných předmětů mezi plány

Tyto požadavky budou řešeny společně, protože se jedná o kombinaci funkcí na stránce porovnání plánů.
- v zobrazení budou vidět jak rozdíly, tak společné předměty

Je potřeba implementovat handler v serveru:
- soubor `webapp/degreeplan/server.go`
- endpoint `GET /compare/{code1}/{code2}`
Je třeba implementovat FE:
- soubor `webapp/degreeplan/view.templ`
- kódy a názvy plánů nahoře vedle sebe
    - odkazy na detaily studijních plánů (`GET /plan/{code}`)
- pak kreditové statistiky a statistiky studentů pro oba plány
- možnosti designu:
    - plán vpravo a plán vlevo
        - nejprve stejné předměty - tabulka, zvýraznit povinné, povinně volitelné, ke státnicím
        - pak rozdíly - co je v jednom a v druhém není - vedle sebe
        - 4 tabulky pod sebou s 2 sloupci
            - povinné pro oba plány
            - povinné pro jeden, povinně volitelné pro druhý
            - povinně volitelné pro oba plány
            - je v jednom, není v druhém
                - seřadit podle povinnosti, vedle sebe bez vztahu
    - plány celé vedle sebe
        - se skupinami
        - zvýraznit co je stejné (barvou, ikonou)
            - stačí jedna barva pro stejné předměty - ignoruje se povinnost
            - při najetí se může předmět zvýraznit v obou plánech
    - jeden seznam, 3 barvy
        - zelená - v obou
        - modrá - jen v levém
        - žlutá - jen v pravém
        - zvolit něco lepšího než barvy
        - vhodné pro mobilní zařízení
    - budou se typicky porovnávat podobné plány
        - má smysl více řešit podobnosti než rozdíly
    - vhodné by bylo implementovat první dvě možnosti a uživatel by si mohl přepínat mezi zobrazeními
        - buď je plán strukturovaný, nebo je to jen seznam předmětů
        - třetí pro mobilní zařízení

Data:
- kódy a názvy plánů jsou v tabulce `plany`
- stačí načíst předměty obout plánů
    - s informacemi o tom, zda je předmět povinný, povinně volitelný, doporučený ke státnicím
    - kód a název předmětu (odkaz na detail předmětu `GET /course/{code}`)
    - použít databázovou package `study_plan`:
        - funkce `study_plan.stud_plan(plan_code, year)` vrací seznam předmětů s jejich povinností
            - rok vždy jen nejnovější
        - v databázi budou načtená data o plánech se všemi potřebnými informacemi
- načíst kreditové statistiky obou plánů
    - řeší se v UC-007
- načíst statistiky studentů obou plánů
    - řeší se v UC-013

**Složitost**: vysoká
**Přínos**: vysoký
**Priorita**: vysoká

# UC-011: Vyhledávání plánů podle předmětů

Design viz `wireframe.pdf`.
Je potřeba implementovat handler v serveru:
- soubor `webapp/degreeplan/server.go`
- endpoint `GET /search-by-code`

Požadavek rozšiřuje UC-004: Filtrování plánů.

Je potřeba zobrazit všechny plány, které odpovídají filtrům.
Zároveň se zobrazí relevantní předměty:
- všechny předměty, které jsou v zobrazených plánech
- seřazené podle počtu výskytů v plánech (nejméně časté nahoře)
- u každého předmětu zobrazit počet plánů, ve kterých se předmět vyskytuje
- jak bude student zaklikávat předměty pomocí checkboxů
    - aktualizují se výsledky
    - lze kombinovat s filtry
    - otázka jestli potvrdit tlačítkem nebo to bude live update
        - live update může být pomalé
        - ideálně tlačítko "Aktualizovat výsledky"
            - problém je, že se možná nic nezobrazí
- v předmětech je možné hledat pomocí textového inputu (název, kód)
    - filtruje se seznam relevantních předmětů
    - Meilisearch

- celkový problém s výkonem
    - je potřeba to otestovat na větším množství dat
    - ideálně použít Meilisearch
        - indexovat plány s jejich předměty
        - aplikovat filtry
        - pak dotaz na plány obsahující všechny zadané předměty

**Složitost**: vysoká 
**Přínos**: nízký
**Priorita**: nízká

# UC-012: Označení plánu za zvolený

U zobrazeného plánu je potřeba přidat tlačítko "Zvolit tento plán".
Po kliknutí na tlačítko se zavolá endpoint:
- `PATCH /user-plan/{code}`
    - PARAM: kód plánu (unikátní identifikátor)
    - uloží zobrazený plán jako zvolený
- po úspěšném uložení bude uživatel přesměrován na domovskou stránku `/{$}`, kde se zobrazí zvolený plán

Alternativně už měl plán zvolený a chce ho odznačit.
- v tom případě se zobrazí tlačítko "Smazat zvolený plán"
- po kliknutí na tlačítko se zavolá endpoint:
    - `DELETE /user-plan`
        - PARAM: žádné
        - smaže informaci o zvoleném plánu uživatele
        - dojde k přesměrování na detail daného plánu `/plan/{code}`

FE se upraví v zobrazení plánu, ale minimálně, v souboru:
- `webapp/degreeplan/view.templ`

Je třeba vytvořit zmíněné endpointy v serveru:
- soubor `webapp/degreeplan/server.go`

V databázi je potřeba vytvořit tabulku pro ukládání zvoleného plánu uživatele:
- RecSIS už podporuje, upravit podle potřeby
    - tabulka `studies`

**Složitost**: nízká 
**Přínos**: střední
**Priorita**: vysoká

# UC-013: Zobrazení statistik o studentech plánu

Je třeba získat data o studentech podle plánu.
V ELT procesu se načtou statistiky o studentech:
- počet studentů, kteří plán studují v daném akademickém roce
- počet studentů, kteří plán dokončili v daném akademickém roce
- průměrný počet let studia plánu
- pro bc kam studenti pokračují do nmgr
- pro nmgr odkud studenti přišli z bc

Tato data se uloží do lokální databáze RecSISu k metadatům plánu.

Na FE se zobrazí v detailu plánu:
- jako tabulka s sloupci pro každý akademický rok
- řádky pro studující a dokončující
- pak průměrný počet let studia
- pak
    - pro bc kam pokračují do nmgr (seznam plánů a počet studentů)
    - pro nmgr odkud přišli z bc (seznam plánů a počet studentů)

Je možné implementovat jako vlastní endpoint v serveru:
- soubor `webapp/degreeplan/server.go`
- lazy load v detailu plánu
- zbytečné, je to málo dat, zbytečná komplikace

Alternativně se to může načítat rovnou s detailem plánu:
- data budou uložená s metadaty plánu
- není jich moc
- vhodné řešení

**Složitost**: střední
**Přínos**: střední
**Priorita**: střední

# UC-014: Procházení hodnocení a komentářů plánů

Samotný vznik hodnocení a komentářů je řešen v UC-018.

Je třeba implementovat FE:
- soubor `webapp/degreeplan/view.templ`

Design jako u detailu předmětu v RecSISu:
- Hodnoceni                 X.Y (počet hodnocení)
- progress bar s průměrným hodnocením
- seznam komentářů seřazených podle data přidání (nejnovější nahoře)
    - uživatelé anonymní
    - datum přidání
    - text komentáře
    - teoreticky možnost nahlásit nevhodný komentář (mimo rozsah)

Aby komentáře nezabraly moc místa, je možné je načítat lazy loadem:
- nejprve se načte jen prvních 5 komentářů
- pak buď stránkování, nebo tlačítko "Načíst další komentáře"
    - načíst další jen pokud je to na konci stránky
    - pravděpodobně bude potřeba přidat endpointy pro lazy load/stránkování

Data budou získána z databáze RecSISu:
- tabulka pro hodnocení plánu
- tabulka pro komentáře k plánu

Je možné implementovat jako vlastní endpoint v serveru:
- soubor `webapp/degreeplan/server.go`
- lazy load v detailu plánu
- pokud bude hodně dat, tak to má smysl
- lazy load dalších komentářů

Vhodné řešení:
- vlastní endpoint pro načtení hodnocení a pár komentářů
- pak stránkování komentářů
    - další endpoint pro načtení komentářů s parametry offset a limit

**Složitost**: nízká
**Přínos**: nízký
**Priorita**: nízká

# UC-015: Vložení doporučeného průchodu do vlastního plánu

Zobrazení doporučeného průchodu plánu je řešeno v UC-021:
- řeší se i jak získat data o doporučeném průchodu
- data dostupná v datech studijního plánu

Je potřeba implementovat FE:
- soubor `webapp/degreeplan/view.templ`
- tlačítko "Vložit doporučený průchod do mého plánu/Blueprintu"
    - po kliknutí se zobrazí dialog s možnostmi:
        - přepsat stávající plán
        - přidat k stávajícímu plánu
- po potvrzení se zavolá endpoint:
    - `POST /assign-plan`
        - PARAM: kód plánu, přepsat/přidat

V serveru je potřeba implementovat handler:
- soubor `webapp/degreeplan/server.go`
- endpoint `POST /assign-plan`
- je třeba použít interface `BlueprintAddButton`
    - upravit pro potřeby tohoto požadavku
    - je možné použít metodu `Action` opakovaně pro všechny semestry doporučeného průchodu
    - problém se smazáním stávajícího plánu uživatele před přidáním nového
    - problém s nastavením počtu let studia
        - je třeba zjistit, jak přesně pracuje aktuální implementace v RecSISu

Přepsat znamená:
- smazat stávající plán uživatele v RecSISu
- vložit doporučený průchod plánu jako nový plán uživatele
    - nastavit vhodný počet let studia

Přidat znamená:
- vložit doporučený průchod plánu do stávajícího plánu uživatele v RecSISu
    - potenciálně zvětšit počet let studia
- ošetřit konflikty předmětů
    - pokud je předmět již v plánu uživatele, tak ho nepřidávat znovu

Pokud není doporučený průchod dostupný, tak se tlačítko nezobrazuje.

Pokud je vlastní plán uživatele (blueprint) prázdný:
- po stisknutí tlačítka se doporučený průchod automaticky přidá (ne přepíše)
- problém s race condition, pokud uživatel mezitím něco přidá do plánu
- problém s načtením předchozího stavu stránky, kde jsou neaktuální data

**Složitost**: střední
**Přínos**: vysoký
**Priorita**: vysoká

# UC-016: Zobrazení předmětů doporučených ke státnicím

Data o doporučených předmětech ke státnicím nejsou strojově dostupná.

Jsou 3 řešení získání dat:
- Je možné vzít zdrojové kódy, ze kterých vzniká Karolínka:
    - ty vytěžit
    - napsat parser
    - uložit do databáze
    - bylo by nutné získat data pro všechny plány
        - problém je, že Karolínka je pro studijní obory, ne pro konkrétní plány
        - je nutné spárovat
        - je nutné sehnat data pro všechny plány
            - bc i nmgr
            - všechny oblasti vzdělávání
            - zdá se, že doporučené předměty ke státnicím má jen Informatika
                - lze se omezit jen na ni
- Komunikace s Petrem Jedelským:
    - slíbená tabulka v MFF databázi, kam dáme data jen pro pár plánů
    - napojit se na ni v ELT procesu
    - získat data
    - sloupce tabulky:
        - kód plánu
        - kód předmětu
- ruční zadání dat do lokální databáze RecSISu:
    - není to ideální řešení
        - není udržovatelné
    - ale je nejjednodušší

Data se uloží do lokální databáze RecSISu:
- tabulka s doporučenými předměty ke státnicím
    - sloupce:
        - kód plánu
        - kód předmětu

Na FE se v detailu plánu označí předměty doporučené ke státnicím:
- ikona (hvězdička, diplom, ...)

**Složitost**: vysoká
**Přínos**: vysoký
**Priorita**: střední

# UC-017: Zobrazení mapy rekvizit

Pro daný plán se vezmou všechny předměty a jejich rekvizity (prerekvizity, korekvizity, neslučitelnosti).
Neformální prerekvizity není možné sehnat, viz komunikace s Petrem Mikešem.

Zobrazovat jen rekvizity které jsou v plánu?
- je možné udělat toggle (filtr) ano/ne
- logické je zobrazit všechny rekvizity
- je možné zvýraznit ty, které jsou v plánu
- může vést rekvizita na předmět mimo plán?
- neslučitelnosti stačí zobrazit jen ty, které jsou v plánu
- korekvizity a prerekvizity je lepší zobrazit všechny

Vytvořit graf
- uzly jsou předměty
- hrany jsou rekvizity
    - jsou orientované
    - různé typy rekvizit různá barva/typ čáry

Grafů bude nejspíše hodně, protože rekvizity tvoří menší komponenty.

Možnost filtrovat hrany podle typu rekvizity
- nezobrazovat samotné uzly bez hran

U uzlů zobrazit kód a název předmětu
- možnost kliknout - detail předmětu `GET /course/{code}`

Na zobrazení grafu použít nějakou JS knihovnu:
- např. D3.js, Cytoscape.js, Vis.js, ...
- diskuze o vhodné knihovně
- diskuze proč JS a ne nějaké jiné řešení
- diskuze proč je lepší použít graf než tabulku

Cytoscape.js se jeví jako vhodná knihovna:
- automatický výpočet rozložení grafu bez nutnosti ručního určování pozic uzlů
- přímá podpora orientovaných grafů vhodná pro reprezentaci rekvizit
- možnost vizuálně odlišit jednotlivé typy rekvizit pomocí stylů hran (barva, typ čáry, šipky)
- interaktivní zobrazení umožňující přibližování, posun grafu a kliknutí na uzly
- okamžité filtrování hran podle typu rekvizity bez nutnosti znovunačtení stránky
- možnost automatického skrytí izolovaných uzlů pro zvýšení přehlednosti
- jasné oddělení serverové a klientské logiky (server poskytuje data, klient zajišťuje vizualizaci)
- snížení zátěže serveru díky vykreslování grafu na straně klienta
- dobrá škálovatelnost pro grafy tvořené menšími nezávislými komponentami
- snadná integrace do stávající webové aplikace bez zásadních architektonických změn

**Složitost**: střední
**Přínos**: střední
**Priorita**: střední

# UC-018: Hodnocení a komentování plánů

Na přidávání a mazání hodnocení a komentářů je potřeba implementovat handlery:
- soubor `webapp/degreeplan/server.go`
- `PUT /survey/rating/{rating}`
    - PARAM: hodnocení, kód plánu
    - uložení hodnocení plánu
- `PUT /survey/feedback`
    - PARAM: textová zpětná vazba, kód plánu
    - uložení zpětné vazby k plánu
- `DELETE /survey/rating`
    - PARAM: kód plánu
    - smazání hodnocení plánu
- `DELETE /survey/feedback`
    - PARAM: kód plánu
    - smazání zpětné vazby k plánu

FE bude implementován společně s UC-014:
- soubor `webapp/degreeplan/view.templ`
- přístup bude jen u zvoleného plánu
- je třeba napsat podporu pro:
    - přidání/úpravu existujícího hodnocení
    - přidání/úpravu existujícího komentáře
    - mazání hodnocení
    - mazání komentáře

Data:
- vzniknou dvě tabulky v databázi RecSISu:
    - hodnocení
        - uživatel, kód plánu, hodnocení (1-10)
    - komentáře
        - uživatel, kód plánu, text komentáře, datum přidání, počet nahlášení

Problém je moderace komentářů:
- vhodné přidat funkci, která bude kontrolovat nevhodný obsah
- možné použít externí službu pro detekci nevhodného obsahu
- důležité je obsah escapovat, aby nešlo vložit škodlivý kód
- možné řešení
    - escapovat obsah
    - jednoduchý filtr zakázaných slov
    - uživatelé mohou nahlásit nevhodný komentář (tlačítko "Nahlásit")
    - programátor může ručně smazat nevhodné komentáře
    - komentáře se nepublikují okamžitě, ale až po schválení (moderování)
        - to lze přes OpenAI Moderation API
    - omezit délku komentáře na rozumnou hodnotu (např. 1000 znaků)

Pokud nebude implementovaný tento požadavek, nemá smysl implementovat UC-014.

**Složitost**: vysoká
**Přínos**: střední
**Priorita**: nízká

# UC-019: Zobrazení zvoleného plánu

Pokud má uživatel zvolený plán, tak se na domovské stránce `/{$}` zobrazí tento plán.
Pokud uživatel nemá zvolený plán, tak se přesměruje na stránku vyhledávání plánů `/search`.

Tato informace se získá z databáze RecSISu:
- tabulka `studies`
- `NULL` znamená, že uživatel nemá zvolený plán
- kód plánu se použije pro načtení detailu plánu pomocí existující logiky pro zobrazení plánu

Zobrazí se detail plánu stejně jako v UC-005:
- navíc možnost hodnotit a komentovat plán (UC-018)
- navíc možnost vložit doporučený průchod do vlastního plánu (UC-015)
- u názvu svítí ikona, že je to zvolený plán
- je možné to zjednodušit a u každého zobrazení povolit všechny funkce

**Složitost**: nízká
**Přínos**: vysoký
**Priorita**: vysoká

# UC-020: Historie zobrazených plánů

Ve vyhledávání plánů se zobrazí historie zobrazených plánů uživatele.
Seřadit podle data zobrazení (nejnovější nahoře).

Odkaz na detail plánu `GET /plan/{code}`.
Data se ukládají do databáze RecSISu:
- tabulka `studies_search_history`
    - sloupce: uživatel, kód plánu, datum zobrazení

Při zobrazení detailu plánu:
- endpoint `GET /plan/{code}` nebo `GET /{$}`
- ať už z vyhledávání nebo zvoleného
- se uloží do historie zobrazených plánů
    - pokud již záznam existuje, tak se aktualizuje datum zobrazení na aktuální čas
    - pokud záznam neexistuje, tak se vytvoří nový záznam
    - omezit počet záznamů na posledních 5
        - pokud by byl limit překročen, tak smazat/přepsat nejstarší záznam

**Složitost**: nízká
**Přínos**: střední
**Priorita**: nízká

# UC-021: Zobrazení doporučeného průchodu plánu

Tato data jsou již dostupná v datech studijního plánu:
- funkce `study_plan.stud_plan(plan_code, year)` vrací seznam předmětů s jejich doporučeným semestrem
    - `bloc_grade`, `bloc_semester` určují doporučený ročník a semestr

Podle toho postavit zobrazení doporučeného průchodu plánu:
- podobně jako v Blueprintu v RecSISu
- tabulka se semestry a předměty v nich
    - detail předmětu jako v ostatních tabulkách

Vhodné načíst rovnou s detailem plánu:
- data budou uložená přímo u plánu, takže se vždy načtou
- není jich moc

**Složitost**: střední
**Přínos**: vysoký 
**Priorita**: vysoká
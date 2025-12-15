# Zainteresované strany

Student
= člověk, který studuje Informatiku na MFF UK v češtině

Nerozhodnutý student
= student, který si ještě nevybral specializaci

Rozhodnutý student
= student, který si vybral specializaci/má daný studijní obor a plánuje si studium

# Problémy

Plánování celého studia najednou (RecSIS)  
Upozornění na prerekvizity ve vlastním plánu = blueprintu

Možnost vyhledávat studijní plán podle názvu/kódu a roku zápisu

Filtrování plánů podle typu (Bc./Mgr.), roku zápisu, studia (informatika/matematika/fyzika) a jazyku (cs/en)

Úvodní text **NEŘEŠITELNÉ?**
- definice studijního plánu (povinné, povinně volitelné, ke státnicím)
- doporučený harmonogram
- práce může navazovat na projekt

Při výběru možnost zobrazit průnik/XOR mezi dvěma zvolenými studijními plány
- průnik pro rozdíl
- XOR pro společné když se nemůže rozhodnout

Možnost vybírat plán podle zvolených předmětů - student zakliká (jen ty, co nejsou společné pro všechny plány/podle státnicových) a systém mu najde plány, které tyto předměty obsahují

Zobrazení daného studijního plánu:
- Jsou vidět skupiny předmětů (povinné, povinně volitelné)
- Je možné ho označit za vybraný - pak je možné s ním pracovat dále
- Zobrazení doporučeného průchodu studiem
- Je možné zvýraznit (přidat) předměty doporučené ke státnicím
- Možnost porovnat s jiným studijním plánem (rozdíly, společné předměty)
- Je vidět mapka prerekvizit (přidat neformální - komunikace se SKAS)
- Je vidět počet povinných a povinně volitelných kreditů a kolik zbývá do požadovaného minima
- Zobrazení statistiky - kolik lidí se zapíše, kolik ukončí, po kolika letech
- Anketa specializace/programu (možnost přidat hodnocení a komentáře od studentů)

Pokud má student vybraný studijní plán:
- Identické jako zobrazení daného studijního plánu
- Může vložit doporučený průchod do blueprintu
- Bude mít pohled jednoho studenta
    - ušetří čas
    - co nejvíce informací na jednom místě
    - po tom co vybral se nemusí proklikávat všude možně
    - plus všechny výhody RecSISu

U předmětů zobrazovat:
- skutečný semester výuky
- garanta/y
- zdali se už nevyučuje
- je poviný/volitelný
- je ke státnicím

## NEŘEŠITELNÉ: 

rozcestník informací - karolínka, informace o uznávání kreditů, o státnících, diplomce, ...

# Vize

## Kdo jsou zainteresované strany?

Uživateli systému jsou studenti Informatiky na MFF UK. Ti se dělí na dvě klíčové skupiny:
- Nerozhodnutý student – student, který si ještě nevybral specializaci a chce prozkoumat možnosti, porovnat a pochopit rozdíly mezi specializacemi.
- Rozhodnutý student – student, který již má zvolenou specializaci/studijní obor a chce efektivně plánovat studium, hlídat prerekvizity a optimalizovat si průchod.

## Jaké problémy řešíme?

Systém pomáhá studentům s rozhodováním o volbě specializace tím, že umožňuje porovnání různých možností a zobrazení hlavních relevantních informací přehledně a na jednom místě. Mimo to zajišťuje přehledné hlídání prerekvizit. Studenti tak mají jasný přehled o požadavcích jednotlivých studijních plánů a mohou plánovat své studium přímo v systému, aniž by museli přeskakovat mezi SISem, Karolínkou a dalšími zdroji informací. Systém navíc umožňuje plánovat přímo z doporučeného průchodu specializací, zobrazuje statistiky, které informují o počtu studentů zapisujících či ukončujících danou specializaci, o průměrné délce studia a dalších relevantních ukazatelích a počítá povinné a povinně volitelné kredity a kolik kreditů zbývá do požadovaného minima.

## Jaké jsou přínosy tohoto řešení?

Navrhované řešení poskytuje jednotný systém pro plánování studia, kde jsou všechny informace dostupné na jednom místě – studijní plány, plánování studia, detaily předmětů, doporučené průchody i statistiky. Výsledné řešení nabízí pohled přizpůsobený konkrétnímu studentovi, nikoli pouhý soupis informací pro přehled a výběr, jako je tomu například v Karolínce. To výrazně šetří čas, minimalizuje potřebu proklikávání a umožňuje okamžitě vložit doporučený průchod do vlastního studijního plánu. Díky tomu student získává co nejvíce informací na jednom místě a může se rychle a efektivně rozhodovat o svém studiu.

## Proč by měli zainteresované strany tento systém používat?

Studenti získají nástroj, který odpovídá jejich skutečným potřebám – umožňuje plánování celého studia najednou, rozhodování, kontrolu prerekvizit a přehled o hlavních aspektech studia na jednom místě. Snadněji a dříve se rozhodnou pro specializaci a vyhnou se chybám v plánování. Nerozhodnutí studenti ocení rychlé porovnání specializací a filtrování na základě vybraných předmětů, zatímco rozhodnutí studenti mohou pohodlně plánovat celé studium podle sebe, ale i přímo podle doporučeného průchodu a sledovat kredity a prerekvizity.

# Funkční požadavky

## Uživatelské příběhy (user-stories)

```
Jako [KDO] chci [CO] abych [PROČ].
```

### Úvodní požadavky

1. Jako student chci být upozorněn na nesplněné prerekvizity, korekvizity a nedodržené neslučitelnosti ve vlastním plánu abych mohl plnit všechny naplánované předměty v naplánovaném ročníku.

2. Jako student chci vyhledávat studijní plány podle jejich názvu a mého roku zápisu abych si mohl rychle najít plán, který mě zajímá.

3. Jako student chci vyhledávat studijní plány podle jejich kódu a mého roku zápisu abych si mohl jednoznačně najít plán, který mě zajímá.  
**Q**: není samotný kód jednoznačný?

4. Jako student chci filtrovat studijní plány podle typu (Bc./Mgr.), roku zápisu, studia (informatika/matematika/fyzika) a jazyku (cs/en), abych mohl snadno najít pro mě relevantní plány.  
**Q**: je tohle vůbec možné? nenabízí ani SIS, je jen v Karolínce

5. Jako student chci mít možnost zobrazit si libovolný studijní plán se všemi detaily (povinné a povinně volitelné skupiny, doporučený průchod, prerekvizity, statistiky, kredity, atd.) abych měl všechny potřebné informace přehledně na jednom místě.

6. Jako student chci u zobrazeného studijního plánu vidět úvodní text upozorňující na předměty doporučené ke státnicím, doporučený harmonogram studia a možnost navázat bakalářskou/diplomovou práci na ročníkový/týmový projekt abych měl všechny důležité informace přehledně na jednom místě.

7. Jako student chci u zobrazeného studijního plánu vidět počet povinných a povinně volitelných kreditů a kolik mi zbývá do požadovaného minima abych věděl jakou volnost daný plán nabízí a mohl si lépe plánovat studium.

8. Jako student chci u předmětů v zobrazeném studijním plánu vidět skutečný semestr výuky, garanta/y, informaci o tom, zda se předmět stále vyučuje, zda je povinný/volitelný a zda je doporučený ke státnicím abych měl všechny potřebné informace pro plánování svého studia.

### Požadavky pro nerozhodnuté studenty

9. Jako nerozhodnutý student chci být schopen zobrazit rozdíly mezi dvěma studijními plány abych se mohl lépe rozhodnout, který studijní plán zvolit.

10. Jako nerozhodnutý student chci být schopen zobrazit společné předměty mezi dvěma studijními plány abych mohl vidět, jak moc se studijními plány liší a co bych musel splnit v obou případech.

11. Jako nerozhodnutý student chci vyhledávat studijními plány podle označených předmětů abych mohl najít studijní plány, které obsahují předměty, jež mě zajímají.

12. Jako nerozhodnutý student chci označit studijní plán jako zvolený abych měl k tomuto plánu rychlý přístup, mohl s ním dále pracovat a plánovat si podle něj studium.

13. Jako nerozhodnutý student chci vidět statistiky o studijním plánu (počet zapsaných studentů, počet ukončených studentů, průměrná délka studia, atd.) abych měl přehled o úspěšnosti daného studijního plánu a mohl se lépe rozhodnout o jeho volbě.

14. Jako nerozhodnutý student chci procházet komentáře a hodnocení studijních plánů od ostatních studentů abych získal další pohledy a zkušenosti, které mi pomohou při výběru specializace.

20. Jako nerozhodnutý student chci vidět historii zobrazených studijních plánů, abych je nemusel pokaždé vyhledávat a měl k nim tak rychlý přístup.

### Požadavky pro rozhodnuté studenty

15. Jako rozhodnutý student chci vložit doporučený průchod studijním plánem do svého vlastního plánu abych mohl snadno plánovat své studium podle doporučeného průchodu.

16. Jako rozhodnutý student chci mít možnost zobrazit/zvýraznit předměty doporučené ke státnicím ve studijním plánu abych mohl plánovat své studium s ohledem na přípravu ke státnicím.

17. Jako rozhodnutý student chci mít možnost zobrazit mapu prerekvizit, korekvizit a neslučitelností studijního plánu abych mohl lépe pochopit závislosti mezi předměty a plánovat své studium efektivněji.

18. Jako rozhodnutý student chci mít možnost komentovat a hodnotit studijní plány abych mohl sdílet své zkušenosti s ostatními studenty a pomoci jim při výběru studijního plánu.

19. Jako rozhodnutý student chci mít přímý přístup ke svému zvolenému studijnímu plánu abych mohl rychle a efektivně plánovat své studium bez nutnosti vyhledávání a proklikávání.

20. Jako nerozhodnutý student chci vidět historii zobrazených studijních plánů, abych je nemusel pokaždé vyhledávat a měl k nim tak rychlý přístup.

21. Jako student chci u zobrazeného studijního plánu vidět doporučený průchod studiem abych věděl, jaké předměty bych měl absolvovat v jednotlivých semestrech, abych předešel komplikacím při plnění prerekvizit a mohl efektivněji plánovat své studium.

## Případy užití (use-cases)

```md
### UC-NNN: Jméno případu užití

## Aktéři

[uveďte seznam aktérů]

## Předpoklady

- [uveďte předpodmínky]

## Základní tok (Basic Flow)

N. [uveďte základní tok jako lineární sekvenci kroků]

## Alternativní toky (Alternative Flows)

Na. [uveďte alternativu ke kroku N]  
Na.1. [uveďte alternativní tok jako lineární sekvenci kroků]

## Výsledný stav (Postconditions)

- [uveďte výsledný stav]
```

### UC-001: Upozornění na rekvizity ve vlastním plánu

## Aktéři

Student

## Související user stories

#1

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_001)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L10))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student má ve svém vlastním plánu (blueprintu) naplánované předměty.

## Základní tok (Basic Flow)

1. Student otevře svůj vlastní plán (blueprint) v systému RecSIS.
2. Systém analyzuje naplánované předměty a jejich prerekvizity, korekvizity a neslučitelnosti.
3. U předmětů, jejichž prerekvizity, korekvizity nebo neslučitelnosti nejsou splněny, systém zobrazí upozornění ve formě ikony u řádku předmětu.
4. Při najetí myší na ikonu se zobrazí detailní informace o nesplněných prerekvizitách, korekvizitách nebo neslučitelnostech pro daný předmět.

## Alternativní toky (Alternative Flows)

2a. Předmět nemá žádné prerekvizity, korekvizity nebo neslučitelnosti.  
2a.1. Systém přeskočí analýzu tohoto předmětu

3a. Systém nezjistí žádné nesplněné prerekvizity, korekvizity nebo neslučitelnosti.  
3a.1. Systém nezobrazí žádná upozornění o nesplněných prerekvizitách, korekvizitách nebo neslučitelnostech a student pokračuje v plánování bez omezení.

## Výsledný stav (Postconditions)

- Systém zobrazí upozornění na nesplněné prerekvizity, korekvizity nebo neslučitelnosti ve vlastním plánu studenta.
- Student je informován o tom, které prerekvizity, korekvizity nebo neslučitelnosti musí splnit.

### UC-002: Vyhledávání plánů podle názvu

## Aktéři

Student

## Související user stories

#2

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_002)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L11))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce pro správu studijních plánů.

## Základní tok (Basic Flow)

1. Student klikne na možnost vyhledávání studijních plánů.
2. Systém zobrazí vyhledávací pole.
3. Student vybere svůj rok zápisu.
4. Student zadá název studijního plánu nebo jeho část.
5. Systém automaticky aktualizuje výsledky vyhledávání podle zadaných kritérií.

## Alternativní toky (Alternative Flows)

4a. Student nezadal název studijního plánu.  
4a.1. Systém nezobrazí žádné výsledky vyhledávání.

5a. Student zadal neplatný rok zápisu.  
5a.1. Systém zobrazí chybovou zprávu  
5a.2  Systém neprovede vyhledávání, dokud student nezadá platný rok zápisu.  
5a.3. Student zadá platný rok zápisu a pokračuje v kroku 4.

5b. Systém nenalezl žádné studijní plány odpovídající zadaným kritériím.  
5b.1. Systém zobrazí zprávu informující studenta, že nebyly nalezeny žádné odpovídající studijní plány.

## Výsledný stav (Postconditions)

- Systém zobrazil seznam studijních plánů odpovídajících zadaným kritériím vyhledávání.
- Student našel studijní plán(y), který hledal.

### UC-003: Vyhledávání plánů podle kódu

## Aktéři

Student

## Související user stories

#3

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_003)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L12))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce pro správu studijních plánů.

## Základní tok (Basic Flow)

1. Student klikne na možnost vyhledávání studijních plánů.
2. Systém zobrazí vyhledávací pole.
3. Student vybere svůj rok zápisu.
4. Student zadá kód studijního plánu.
5. Systém automaticky aktualizuje výsledky vyhledávání podle zadaných kritérií.

## Alternativní toky (Alternative Flows)

4a. Student nezadal kód studijního plánu.  
4a.1. Systém nezobrazí žádné výsledky vyhledávání.

5a. Student zadal neplatný rok zápisu.  
5a.1. Systém zobrazí chybovou zprávu  
5a.2  Systém neprovede vyhledávání, dokud student nezadá platný rok zápisu.  
5a.3. Student zadá platný rok zápisu a pokračuje v kroku 4.

5b. Systém nenalezl žádné studijní plány odpovídající zadaným kritériím.  
5b.1. Systém zobrazí zprávu informující studenta, že nebyly nalezeny žádné odpovídající studijní plány.

## Výsledný stav (Postconditions)

- System zobrazil seznam studijních plánů odpovídajících zadaným kritériím vyhledávání.
- Student našel studijní plán(y), který hledal.

### UC-004: Filtrování plánů

## Aktéři

Student

## Související user stories

#4

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_004)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L13))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce pro správu studijních plánů.

## Základní tok (Basic Flow)

1. Student klikne na možnost filtrování studijních plánů.
2. Systém zobrazí dostupná filtrační kritéria (typ, rok zápisu, studium, jazyk).
3. Student vybere požadovaná filtrační kritéria.
4. Systém automaticky aktualizuje výsledky zobrazených studijních plánů podle zvolených filtrů.

## Alternativní toky (Alternative Flows)

3a. Student nevybere žádná filtrační kritéria.  
3a.1. Systém nezobrazí žádné výsledky filtrování.

4a. Systém nenalezl žádné studijní plány odpovídající zadaným kritériím.  
4a.1. Systém zobrazí zprávu informující studenta, že nebyly nalezeny žádné odpovídající studijní plány.

## Výsledný stav (Postconditions)

- Systém zobrazil seznam studijních plánů odpovídajících zadaným filtračním kritériím.
- Student obdržel seznam pro něj relevantních studijních plánů.

### UC-005: Zobrazení plánu

## Aktéři

Student

## Související user stories

#5

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_005)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L14))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce pro správu studijních plánů.
- Student vybral studijní plán k zobrazení./Student má zvolený studijní plán.

## Základní tok (Basic Flow)

1. Student klikne na studijní plán, který chce zobrazit.
2. Systém načte a zobrazí detaily studijního plánu, včetně povinných a povinně volitelných skupin, doporučeného průchodu, prerekvizit, statistik a kreditů.

## Alternativní toky (Alternative Flows)

2a. Systém nemůže načíst detaily studijního plánu (např. kvůli technické chybě).  
2a.1. Systém zobrazí chybovou zprávu informující studenta o problému.  
2a.2. Student pokračuje v kroku 1 nebo opustí zobrazení plánů.

2b. Studijní plán neobsahuje nějaké detaily (např. doporučený průchod nebo statistiky).  
2b.1. Systém zobrazí dostupné informace a upozorní studenta na chybějící detaily.

## Výsledný stav (Postconditions)

- Systém zobrazil kompletní detaily zvoleného studijního plánu.
- Student má přístup ke všem sekcím studijního plánu na jednom místě, jasně strukturovaným způsobem, který umožňuje rychlou orientaci.

### UC-006: Úvodní text u plánu

## Aktéři

Student

## Související user stories

#6

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_006)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L15))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce zobrazeného studijního plánu.
- Student vybral studijní plán k zobrazení./Student má zvolený studijní plán.

## Základní tok (Basic Flow)

1. Systém načte a zobrazí úvodní text studijního plánu, který obsahuje informace o předmětech doporučených ke státnicím, doporučeném harmonogramu studia a možnosti navázání bakalářské/diplomové práce na ročníkový/týmový projekt.

## Alternativní toky (Alternative Flows)

N/A

## Výsledný stav (Postconditions)

- Systém zobrazil úvodní text studijního plánu.
- Student je informován o doporučených předmětech ke státnicím, harmonogramu studia a možnostech navázání bakalářské/diplomové práce.

### UC-007: Kreditové statistiky u detailu plánu

## Aktéři

Student

## Související user stories

#7

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_007)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L16))_
    
## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce zobrazeného studijního plánu.
- Student vybral studijní plán k zobrazení./Student má zvolený studijní plán.

## Základní tok (Basic Flow)

1. Systém spočítá součet povinných a povinně volitelných kreditů ve studijním plánu.
2. Systém určí, kolik minimálních kreditů je požadováno pro daný studijní plán.
3. Systém vypočítá, kolik kreditů studentovi zbývá do požadovaného minima.
4. Systém zobrazí tyto informace studentovi.

## Alternativní toky (Alternative Flows)

2a. Systém nemůže určit minimální požadované kredity.
2a.1. Systém nevypočítá zbývající kredity.
2a.2. Systém zobrazí pouze dostupné kreditové informace.

## Výsledný stav (Postconditions)

- Systém zobrazil kreditové statistiky studijního plánu.
- Student má přehled o kreditové volnosti daného studijního plánu. 

### UC-008: Detail předmětu v zobrazeném studijním plánu

## Aktéři

Student

## Související user stories

#8

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_008)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L17))_
    
## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce zobrazeného studijního plánu.
- Student vybral studijní plán k zobrazení./Student má zvolený studijní plán.

## Základní tok (Basic Flow)

1. Systém načte detaily každého předmětu ve studijním plánu, včetně skutečného semestru výuky, garanta/y, informace o tom, zda se předmět stále vyučuje, zda je povinný/volitelný a zda je doporučený ke státnicím.
2. Systém zobrazí tyto informace u každého předmětu ve studijním plánu ve formě tabulky.

## Alternativní toky (Alternative Flows)

1a. Libovolná informace o předmětu není dostupná (např. garant).  
1a.1. Systém zobrazí pouze dostupné informace.

## Výsledný stav (Postconditions)

- Systém zobrazil detaily předmětů ve studijním plánu.
- Student má přístup ke všem relevantním informacím o předmětech ve studijním plánu.

### UC-009: Zobrazení rozdílů mezi dvěma plány

## Aktéři

Nerozhodnutý student

## Související user stories

#9

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_009)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L18))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na možnost porovnání studijních plánů.
2. Systém nabídne vyhledávací pole pro výběr prvního studijního plánu.
3. Nerozhodnutý student vybere první studijní plán.
4. Systém nabídne vyhledávací pole pro výběr druhého studijního plánu.
5. Nerozhodnutý student vybere druhý studijní plán.
6. Nerozhodnutý student potvrdí výběr obou plánů pro porovnání.
7. Systém analyzuje oba studijní plány a identifikuje rozdíly mezi nimi. Specificky identifikuje předměty, které jsou unikátní pro každý plán a počet povinných a povinně volitelných kreditů.
8. Systém přehledně zobrazí specifické rozdíly mezi oběma studijními plány a jejich statistiky o studentech a kreditech.

## Alternativní toky (Alternative Flows)

1a. Nerozhodnutý student měl zobrazený již jeden plán a chce porovnat s jiným.  
1a.1. Nerozhodnutý student klikne na možnost porovnání studijních plánů.  
1a.2. Systém pokračuje v kroku 4 základního toku.

4a. Nerozhodnutý student se rozhodne změnit první vybraný plán.  
4a.1. Systém vrátí nerozhodnutého studenta zpět ke kroku 2.

6a. Nerozhodnutý student se rozhodne změnit druhý vybraný plán.  
6a.1. Systém vrátí nerozhodnutého studenta zpět ke kroku 4.

7a. Systém nemůže načíst detaily jednoho nebo obou studijních plánů (např. kvůli technické chybě).  
7a.1. Systém zobrazí chybovou zprávu informující studenta o problému.  
7a.2. Nerozhodnutý student pokračuje v kroku 2 nebo opustí zobrazení plánů.

7b. Plány jsou identické.  
7b.1. Systém zobrazí zprávu informující studenta, že oba plány jsou identické.

7c. Plány jsou kompletně odlišné (žádné společné předměty).  
7c.1. Systém zobrazí zprávu informující studenta, že oba plány jsou kompletně odlišné.

## Výsledný stav (Postconditions)

- Systém identifikoval a přehledně prezentoval rozdíly mezi studijními plány.
- Nerozhodnutý student má přehled o rozdílech mezi dvěma studijními plány, což mu pomáhá při rozhodování o volbě specializace.

### UC-010: Zobrazení společných předmětů mezi plány

## Aktéři

Nerozhodnutý student

## Související user stories

#10

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_010)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L19))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů.

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na možnost zobrazení společných předmětů mezi studijními plány.
2. Systém nabídne vyhledávací pole pro výběr prvního studijního plánu.
3. Nerozhodnutý student vybere první studijní plán.
4. Systém nabídne vyhledávací pole pro výběr druhého studijního plánu.
5. Nerozhodnutý student vybere druhý studijní plán.
6. Nerozhodnutý student potvrdí výběr obou plánů pro zobrazení společných předmětů.
7. Systém analyzuje oba studijní plány a identifikuje předměty, které jsou společné pro oba plány.
8. Systém přehledně zobrazí seznam společných předmětů mezi oběma studijními plány.

## Alternativní toky (Alternative Flows)

1a. Nerozhodnutý student měl zobrazený již jeden plán a chce porovnat s jiným.  
1a.1. Nerozhodnutý student klikne na možnost zobrazení společných předmětů mezi studijními plány.  
1a.2. Systém pokračuje v kroku 4 základního toku.

4a. Nerozhodnutý student se rozhodne změnit první vybraný plán.  
4a.1. Systém vrátí nerozhodnutého studenta zpět ke kroku 2.

6a. Nerozhodnutý student se rozhodne změnit druhý vybraný plán.  
6a.1. Systém vrátí nerozhodnutého studenta zpět ke kroku 4.

7a. Systém nemůže načíst detaily jednoho nebo obou studijních plánů (např. kvůli technické chybě).  
7a.1. Systém zobrazí chybovou zprávu informující studenta o problému.  
7a.2. Nerozhodnutý student pokračuje v kroku 2 nebo opustí zobrazení plánů.

7b. Plány nemají žádné společné předměty.  
7b.1. Systém zobrazí zprávu informující studenta, že oba plány nemají žádné společné předměty.

7c. Plány jsou identické.  
7c.1. Systém zobrazí zprávu informující studenta, že oba plány jsou identické.

## Výsledný stav (Postconditions)

- Systém identifikoval a přehledně prezentoval společné předměty mezi studijními plány.
- Nerozhodnutý student má přehled o společných předmětech mezi dvěma studijními plány, což mu pomáhá při rozhodování o volbě specializace.

### UC-011: Vyhledávání plánů podle předmětů

## Aktéři

Nerozhodnutý student

## Související user stories

#11

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_011)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L20))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů.

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na možnost vyhledávání studijních plánů podle předmětů.
2. Systém zobrazí možnost filtrovat studijní plány podle detailů studia studenta.
3. Nerozhodnutý student nepovinně zvolí detaily studia (typ, rok zápisu, studium, jazyk).
4. Systém zobrazí všechny předměty dostupné ve zvolených studijních plánech.
5. Nerozhodnutý student vybere jeden nebo více předmětů, které ho zajímají.
6. Systém automaticky aktualizuje seznam předmětů podle studijních plánů obsahujících vybrané předměty.
7. Systém automaticky aktualizuje výsledky vyhledávání podle zadaných kritérií.

## Alternativní toky (Alternative Flows)

5a. Nerozhodnutý student zvolí možnost vybírat podle předmětům doporučeným ke státnicím.  
5a.1. Systém zobrazí pouze předměty doporučené ke státnicím ve studijních plánech.  
5a.2. Systém pokračuje v kroku 5 základního toku.

## Výsledný stav (Postconditions)

- Systém zobrazil seznam studijních plánů obsahujících vybrané předměty.
- Nerozhodnutý student obdržel seznam studijních plánů, které obsahují předměty, jež ho zajímají.

### UC-012: Označení plánu za zvolený

## Aktéři

Nerozhodnutý student

## Související user stories

#12

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_012)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L21))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů
- Nerozhodnutý student má zobrazený studijní plán, který chce označit jako zvolený.

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na tlačítko "Označit jako zvolený" u zobrazeného studijního plánu.
2. Systém uloží informaci o zvoleném studijním plánu do profilu nerozhodnutého studenta.
3. Systém nerozhodnutého studenta přesměruje na stránku se zvoleným studijním plánem.

## Alternativní toky (Alternative Flows)

2a. Systém nemůže uložit informaci o zvoleném studijním plánu (např. kvůli technické chybě).  
2a.1. Systém zobrazí chybovou zprávu informující studenta o problému.  
2a.2. Nerozhodnutý student může zkusit znovu označit plán jako zvolený nebo opustit zobrazení plánů.

## Výsledný stav (Postconditions)

- Systém uložil zvolený studijní plán do profilu nerozhodnutého studenta.
- Nerozhodnutý student má rychlý přístup ke svému zvolenému studijnímu plánu.

### UC-013: Zobrazení statistik o studentech plánu

## Aktéři

Nerozhodnutý student

## Související user stories

#13

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_013)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L22))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů.
- Nerozhodnutý student má zobrazený studijní plán, jehož statistiky chce zobrazit.

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na možnost zobrazení statistik o studentech plánu.
2. Systém načte a zobrazí statistiky o studijním plánu, včetně počtu zapsaných studentů, počtu ukončených studentů a průměrné délky studia.

## Alternativní toky (Alternative Flows)

2a. Systém nemůže načíst statistiky studijního plánu (např. kvůli technické chybě).  
2a.1. Systém zobrazí chybovou zprávu informující studenta o problému.  

2b. Statistické údaje nejsou dostupné pro daný studijní plán.  
2b.1. Systém zobrazí zprávu informující studenta, že statistiky nejsou dostupné.

## Výsledný stav (Postconditions)

- Systém zobrazil statistiky o studijním plánu.
- Nerozhodnutý student má přehled o počtu zapsaných studentů, počtu ukončených studentů a průměrné délce studia pro daný studijní plán.

### UC-014: Procházení hodnocení a komentářů plánů

## Aktéři

Nerozhodnutý student

## Související user stories

#14

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_014)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L23))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů.
- Nerozhodnutý student má zobrazený studijní plán, jehož hodnocení a komentáře chce procházet.

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na možnost procházení hodnocení a komentářů studijního plánu.
2. Systém načte a zobrazí hodnocení a komentáře k danému studijnímu plánu.

## Alternativní toky (Alternative Flows)

2a. Systém nemůže načíst hodnocení a komentáře (např. kvůli technické chybě).  
2a.1. Systém zobrazí chybovou zprávu informující studenta o problému.  

2b. Nejsou dostupná žádná hodnocení nebo komentáře pro daný studijní plán.  
2b.1. Systém zobrazí zprávu informující studenta, že nejsou dostupná žádná hodnocení nebo komentáře.

## Výsledný stav (Postconditions)

- Systém zobrazil hodnocení a komentáře k danému studijnímu plánu.
- Nerozhodnutý student má přehled o pohledech a zkušenostech od ostatních studentů.

### UC-015: Vložení doporučeného průchodu do vlastního plánu

## Aktéři

Rozhodnutý student

## Související user stories

#15

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_015)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L24))_

## Předpoklady

- Rozhodnutý student je přihlášen do systému RecSIS.
- Rozhodnutý student má zvolený studijní plán.
- Rozhodnutý student je na stránce zvoleného studijního plánu.

## Základní tok (Basic Flow)

1. Rozhodnutý student klikne na tlačítko "Vložit doporučený průchod do vlastního plánu".
2. Systém zobrazí možnost přepsat existující plán nebo přidat doporučený průchod k již existujícímu plánu.
3. Rozhodnutý student zvolí požadovanou možnost (přepsat nebo přidat).
4. Systém zkopíruje doporučený průchod studijním plánem do vlastního plánu rozhodnutého studenta a provede případné úpravy podle zvolené možnosti.

## Alternativní toky (Alternative Flows)

1a. Plán nemá žádný doporučený průchod.  
1a.1. Systém nenabídne možnost vložení doporučeného průchodu.

2a. Vlastní plán rozhodnutého studenta je prázdný.  
2a.1. Systém automaticky vloží doporučený průchod do vlastního plánu bez nutnosti volby.

4a. Dojde ke konfliktu mezi existujícími předměty ve vlastním plánu a předměty v doporučeném průchodu.  
4a.1. Systém nevloží konfliktní předměty.

## Výsledný stav (Postconditions)

- Doporučený průchod studijním plánem byl úspěšně vložen do vlastního plánu rozhodnutého studenta.
- Rozhodnutý student může nyní plánovat své studium podle doporučeného průchodu.

### UC-016: Zobrazení předmětů doporučených ke státnicím

## Aktéři

Rozhodnutý student

## Související user stories

#16

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_016)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L25))_

## Předpoklady

- Rozhodnutý student je přihlášen do systému RecSIS.
- Rozhodnutý student má zvolený studijní plán.
- Rozhodnutý student je na stránce zvoleného studijního plánu

## Základní tok (Basic Flow)

1. Rozhodnutý student klikne na možnost zobrazení předmětů doporučených ke státnicím.
2. Systém zobrazí seznam předmětů doporučených ke státnicím ve studijním plánu.
3. Rozhodnutý student může zvýraznit tyto předměty v studijním plánu pro lepší přehlednost.

## Alternativní toky (Alternative Flows)

2a. Studijní plán neobsahuje žádné předměty doporučené ke státnicím.  
2a.1. Systém zobrazí zprávu informující studenta, že nejsou dostupné žádné předměty doporučené ke státnicím.

## Výsledný stav (Postconditions)

- Systém zobrazil a zvýraznil předměty doporučené ke státnicím.
- Rozhodnutý student má přehled o předmětech doporučených ke státnicím ve svém studijním plánu pro lepší plánování studia.

### UC-017: Zobrazení mapy rekvizit

## Aktéři

Rozhodnutý student

## Související user stories

#17

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_017)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L26))_

## Předpoklady

- Rozhodnutý student je přihlášen do systému RecSIS.
- Rozhodnutý student má zvolený studijní plán.
- Rozhodnutý student je na stránce zvoleného studijního plánu

## Základní tok (Basic Flow)

1. Rozhodnutý student klikne na možnost zobrazení mapy rekvizit studijního plánu.
2. Systém načte a zobrazí vizuální mapu prerekvizit, korekvizit a neslučitelností pro předměty ve studijním plánu.
3. Rozhodnutý student si může nechat zobrazit i neformální prerekvizity mezi předměty.
4. Rozhodnutý student může filtrovat co chce na mapě vidět (prerekvizity, korekvizity, neslučitelnosti, neformální prerekvizity).

## Alternativní toky (Alternative Flows)

2a. Studijní plán neobsahuje žádné prerekvizity, korekvizity nebo neslučitelnosti.  
2a.1. Systém zobrazí zprávu informující studenta, že nejsou dostupné žádné rekvizity pro zobrazení na mapě.

3a. Neformální prerekvizity nejsou dostupné.  
3a.1. Systém zobrazí pouze formální prerekvizity mezi předměty.

## Výsledný stav (Postconditions)

- Systém zobrazil vizuální mapu rekvizit.
- Rozhodnutý student má přehled o prerekvizitách, korekvizitách a neslučitelnostech, pro lepší pochopení vztahů mezi předměty ve studijním plánu.

### UC-018: Hodnocení a komentování plánů

## Aktéři

Rozhodnutý student

## Související user stories

#18

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_018)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L27))_

## Předpoklady

- Rozhodnutý student je přihlášen do systému RecSIS.
- Rozhodnutý student má zvolený studijní plán.
- Rozhodnutý student je na stránce zvoleného studijního plánu

## Základní tok (Basic Flow)

1. Rozhodnutý student klikne na možnost hodnocení a komentování studijního plánu.
2. Systém zobrazí formulář pro zadání hodnocení (např. škála 1-10) a komentáře.
3. Rozhodnutý student vyplní hodnocení a komentář.
4. Rozhodnutý student odešle hodnocení a komentář.
5. Systém uloží hodnocení a komentář do databáze.

## Alternativní toky (Alternative Flows)

2a. Uživatel už dříve hodnotil a komentoval tento studijní plán.  
2a.1. Systém zobrazí předchozí hodnocení a komentář s možností je upravit nebo smazat.  
2a.2. Rozhodnutý student upraví nebo smaže své předchozí hodnocení a komentář.  
2a.3. Rozhodnutý student odešle aktualizované hodnocení a komentář.  
2a.4. Systém uloží aktualizované hodnocení a komentář do databáze.

4a. Rozhodnutý student nezadá žádné hodnocení ani komentář.   
4a.1. Systém zobrazí chybovou zprávu informující studenta, že hodnocení nebo komentář musí být zadány před odesláním.

4b. Rozhodnutý student nezadá hodnocení nebo komentář.  
4b.1. Systém uloží pouze zadané informace (hodnocení nebo komentář) do databáze.

5a. Systém nemůže uložit komentář kvůli nevhodného obsahu (např. nevhodný jazyk).  
5a.1. Systém zobrazí chybovou zprávu informující studenta o problému a požádá ho o úpravu komentáře.

5b. Systém nemůže uložit hodnocení a komentář (např. kvůli technické chybě).  
5b.1. Systém zobrazí chybovou zprávu informující studenta o problému.  
5b.2. Rozhodnutý student může zkusit znovu odeslat hodnocení a komentář nebo opustit zobrazení plánů.

## Výsledný stav (Postconditions)

- Systém uložil hodnocení a komentář do databáze.
- Rozhodnutý student může vidět své hodnocení a komentáře u studijního plánu.
- Ostatní studenti mohou vidět hodnocení a komentáře k danému studijnímu plánu.

### UC-019: Zobrazení zvoleného plánu

## Aktéři

Rozhodnutý student

## Související user stories

#19

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_019)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L28))_

## Předpoklady

- Rozhodnutý student je přihlášen do systému RecSIS.
- Rozhodnutý student má zvolený studijní plán.

## Základní tok (Basic Flow)

1. Rozhodnutý student se naviguje na stránku se studijními plány.
2. Systém automaticky načte a zobrazí zvolený studijní plán rozhodnutého studenta.
3. Systém načte možnosti pro správu zvoleného studijního plánu

## Alternativní toky (Alternative Flows)

N/A

## Výsledný stav (Postconditions)

- Rozhodnutý student vidí svůj zvolený studijní plán spolu s možnostmi pro jeho správu.

### UC-020: Historie zobrazených plánů

## Aktéři

Nerozhodnutý student

## Související user stories

#39 

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_020)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L29))_

## Předpoklady

- Nerozhodnutý student je přihlášen do systému RecSIS.
- Nerozhodnutý student je na stránce pro správu studijních plánů.
- Nerozhodnutý student si v minulosti zobrazil nějaké studijní plány.

## Základní tok (Basic Flow)

1. Nerozhodnutý student klikne na možnost zobrazení historie zobrazených plánů.
2. Systém načte a zobrazí seznam pěti naposledy zobrazených studijních plánů nerozhodnutého studenta.

## Alternativní toky (Alternative Flows)

N/A

## Výsledný stav (Postconditions)

- Systém zobrazil historii zobrazených plánů.
- Nerozhodnutý student má přehled o svých nedávno zobrazených studijních plánech pro snadný přístup.

### UC-021: Zobrazení doporučeného průchodu plánu

## Aktéři

Student

## Související user stories

#41

## Související diagramy

![Use Case Diagram](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/use-case-diagram.svg#elem_UC_021)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/2329876530b71f0e725a455d2d47774e21708991/documentation/use-case-diagram.plantuml#L30))_

## Předpoklady

- Student je přihlášen do systému RecSIS.
- Student je na stránce pro správu studijních plánů.
- Student má zobrazený studijní plán, jehož doporučený průchod chce zobrazit.

## Základní tok (Basic Flow)

1. Student klikne na možnost zobrazení doporučeného průchodu plánu.
2. Systém načte a zobrazí doporučený průchod studijním plánem, včetně pořadí a rozložení předmětů v jednotlivých semestrech.

## Alternativní toky (Alternative Flows)

2a. Studijní plán neobsahuje žádný doporučený průchod.  
2a.1. Systém zobrazí zprávu informující studenta, že doporučený průchod není dostupný.

2b. Systém nemůže načíst doporučený průchod (např. kvůli technické chybě).  
2b.1. Systém zobrazí chybovou zprávu informující studenta o problému.

## Výsledný stav (Postconditions)

- Systém zobrazil doporučený průchod studijním plánem.
- Student má přehled o doporučeném průchodu a může si podle něj naplánovat své studium.

# Kvalitativní požadavky

Rozšíření musí být navrženo tak, aby nový student zvládl zobrazit studijní plán a základní porovnání bez nutnosti číst dokumentaci.
Metrika: 90 % testovaných uživatelů musí být schopno zobrazit svůj plán do 60 sekund.

Uživatel musí být schopen dostat se k hlavním funkcím (zobrazení plánu, porovnání, úprava blueprintu) nejvýše přes 2–3 kroky.

Rozšíření musí mít:
- vysvětlivky ke zkratkám (hover nebo info ikonka),
- konzistentní vizuální styl pro předměty, kredity a upozornění,
- jasné vysvětlení významu formátování (např. tučné = povinné, kurzíva = volitelné).

Základní funkce – vyhledávání a zobrazení plánu s jeho detaily a základními funkcionalitami musí být dostupné na mobilu v responzivním layoutu. Nemusí být dostupné porovnávání.

CRUD operace nad blueprintem musí být atomické, aby nemohlo dojít k částečně uloženému nebo nevalidnímu stavu.

Uživatel musí být přihlášen přes CAS UK.

Blueprint studijního plánu je přístupný pouze jeho autorovi; totéž platí pro data o jeho studiu (nikdo jiný je nesmí číst).

Systém umožňuje logovat základní operace (zobrazení plánu, porovnání plánů, ...).

Logy nesmí obsahovat žádné osobní ani citlivé údaje.

# Omezení (Constraints)

## Technické a architektonické omezení

### 1. Rozšíření existujícího systému RecSIS
Nově navrhované řešení musí být implementováno jako rozšíření stávající aplikace RecSIS.  
Z toho vyplývá nutnost:
- využívat existující datové modely a infrastrukturu,
- respektovat současnou architekturu backendu a frontendu,
- integrovat se do již existujícího způsobu autentizace a práce s uživatelskými účty,
- nepřepisovat nesouvisející funkce RecSIS.

### 2. Technologický stack RecSIS
Rozšíření musí používat stejné technologie jako hlavní systém:
- **backend:** Go  
- **databáze:** PostgreSQL  
- **frontend:** Go Templ (server-side), doplněné pouze o nezbytné minimum JavaScriptu (např. pro vizualizace) primárně pomocí Alpine.js.

Je zakázáno zavádět nový framework či technologii, pokud by nešla integrovat se stávající architekturou.

### 3. Dostupnost a kvalita dat ze SIS
RecSIS využívá data synchronizovaná z databáze SIS, nicméně:
- **ne všechna relevantní data jsou v SIS dostupná**,  
- některé informace mohou být neúplné, neaktuální nebo závislé na interpretaci.

Nové řešení s tím musí počítat a nesmí předpokládat úplnost nebo plnou konzistenci dat.

## Provozní omezení

### 4. Bezpečnostní a přístupová pravidla UK
Systém musí respektovat pravidla univerzitních služeb, zejména:
- autentizaci přes CAS UK,
- správu uživatelských dat v souladu s interními směrnicemi,
- přístup pouze k datům, která jsou univerzitou zpřístupněna.

## Organizační omezení

### 6. Rozšíření nesmí negativně ovlivnit stávající funkce RecSIS
Nové moduly nesmí měnit chování současných funkcí:
- plánování po semestrech,
- vyhledávání a filtrování předmětů,
- práce s blueprintem,
- zobrazování detailů předmětů.

### 7. Časové omezení
Návrh i implementace musí být realizovány v rámci diplomové práce a běžné evoluce RecSIS; nelze připravovat dlouhodobě neudržitelné nebo extrémně náročné změny architektury.

# Doménový model

![Domaine Model](https://raw.githubusercontent.com/MedekMichal/analyza-studijnich-planu/refs/heads/main/documentation/class-diagram.svg)  
_(viz [zdroj](https://github.com/MedekMichal/analyza-studijnich-planu/blob/171c07f35b2f21fdff9303fdbc2981637265c367/documentation/class-diagram.plantuml))_

## Třídy

### Student

Člověk, který studuje Informatiku na MFF UK v češtině.

### Studijní plán

Třída, která reprezentuje studijní plán na MFF UK.

### Komentář

Třída, která reprezentuje komentář uživatele k danému studijnímu plánu.

### Hodnocení

Třída, která reprezentuje hodnocení uživatele k danému studijnímu plánu.

### Statistika

Třída, která reprezentuje informace o počtu studentů a absolventů daného studijního plánu.

### Skupina

Třída, která reprezentuje základní stavební kámen studijního plánu, specifikující povinné a povinně volitelné předměty.

### Předmět ve skupině

Třída, která reprezentuje základní stavební kámen skupiny, specifikující pozici předmětu a jeho doporučený ročník.

### Předmět

Třída, která reprezentuje předmět vyučovaný na MFF UK.

### Blueprint

Třída, která reprezentuje vlastní studijní plán uživatele, který si může upravovat a kde plánuje své studium.

### Skupina blueprintu

Třída, která reprezentuje základní stavební kámen blueprintu, specifikující vlastnosti skupiny v uživatelském plánu.

### Předmět ve skupině blueprintu

Třída, která reprezentuje základní stavební kámen skupiny blueprintu, specifikující pozici předmětu.

### Složitá rekvizita

Třída, která reprezentuje složité (rekurzivní) vztahy mezi předměty, založené na logických výrazech AND a OR a postavené nad jednoduchými rekvizitami.

### Jednoduchá rekvizita

Třída, která reprezentuje jednoduché vztahy mezi předměty - přímé prerekvizity, korekvizity a neslučitelnosti.
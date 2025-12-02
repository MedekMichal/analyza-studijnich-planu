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
- Je možné ji označit za vybranou - pak je možné s ní pracovat dále
- Zobrazení doporučeného průchodu studiem
- Je možné zvýraznit (přidat) předměty doporučené ke státnicím
- Možnost porovnat s jinou specializací
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

Jako [KDO] chci [CO] abych [PROČ].

### Úvodní požadavky

Jako student chci plánovat celé studium najednou abych měl přehled o svém studiu, měl jistotu, že můj plán pokryje všechny studijní požadavky a stihl dostudovat v řádném termínu.  
**Q**: tohle plní RecSIS, psát to sem?

Jako student chci být upozorněn na nesplněné prerekvizity ve vlastním plánu abych mohl plnit všechny naplánované předměty v naplánovaném ročníku.

Jako student chci vyhledávat studijní plány podle jejich názvu a mého roku zápisu abych si mohl rychle najít plán, který mě zajímá.

Jako student chci vyhledávat studijní plány podle jejich kódu a mého roku zápisu abych si mohl jednoznačně najít plán, který mě zajímá.  
**Q**: tohle plní RecSIS, psát to sem?  
**Q**: není samotný kód jednoznačný?

Jako student chci u vybraného studijního plánu vidět úvodní text upozorňující na předměty doporučené ke státnicím, doporučený harmonogram studia a možnost navázat bakalářskou/diplomovou práci na ročníkový/týmový projekt abych měl všechny důležité informace přehledně na jednom místě.  
**Q**: Toto lze řešit manuálním vložením daného textu, není to ovšem škálovatelné. Má to smysl řešit?

Jako student chci mít možnost zobrazit si libovolný studijní plán se všemi detaily (povinné a povinně volitelné skupiny, doporučený průchod, prerekvizity, garanti, statistiky, kredity, atd.) abych měl všechny potřebné informace přehledně na jednom místě.

Jako student chci u předmětů vidět skutečný semestr výuky, garanta/y, informaci o tom, zda se předmět stále vyučuje, zda je povinný/volitelný a zda je doporučený ke státnicím abych měl všechny potřebné informace pro plánování svého studia.

Jako student chci filtrovat studijní plány podle typu (Bc./Mgr.), roku zápisu, studia (informatika/matematika/fyzika) a jazyku (cs/en), abych mohl snadno najít pro mě relevantní plány.  
**Q**: je tohle vůbec možné? nenabízí ani SIS, je jen v Karolínce

### Požadavky pro nerozhodnuté studenty

Jako nerozhodnutý student chci zobrazit rozdíly mezi studijními plány abych se mohl lépe rozhodnout, kterou specializaci zvolit.

Jako nerozhodnutý student chci zobrazit společné předměty mezi dvěma studijními plány abych mohl vidět, jak moc se studijními plány liší a co bych musel splnit v obou případech.

Jako nerozhodnutý student chci vyhledávat studijními plány podle označených předmětů abych mohl najít studijní plány, které obsahují předměty, jež mě zajímají.

Jako nerozhodnutý student chci označit studijní plán jako vybraný abych mohl s tímto plánem dále pracovat a plánovat si podle něj studium.

Jako nerozhodnutý student chci vidět statistiky o studijním plánu (počet zapsaných studentů, počet ukončených studentů, průměrná délka studia, atd.) abych měl přehled o úspěšnosti daného studijního plánu a mohl se lépe rozhodnout o jeho volbě.

Jako nerozhodnutý student chci procházet komentáře a hodnocení studijních plánů od ostatních studentů abych získal další pohledy a zkušenosti, které mi pomohou při výběru specializace.  
**Q**: má tento požadavek smysl?

### Požadavky pro rozhodnuté studenty

Jako rozhodnutý student chci vložit doporučený průchod studijním plánem do svého vlastního plánu abych mohl snadno plánovat své studium podle doporučeného průchodu.

Jako rozhodnutý student chci mít možnost zobrazit/zvýraznit předměty doporučené ke státnicím ve studijním plánu abych mohl plánovat své studium s ohledem na přípravu ke státnicím.

Jako rozhodnutý student chci mít možnost zobrazit mapu prerekvizit studijního plánu abych mohl lépe pochopit závislosti mezi předměty a plánovat své studium efektivněji.

Jako rozhodnutý student chci vidět počet povinných a povinně volitelných kreditů a kolik mi zbývá do požadovaného minima abych měl přehled o svém postupu ke splnění studijních požadavků a mohl si lépe plánovat studium.

Jako rozhodnutý student chci mít možnost komentovat a hodnotit studijní plány abych mohl sdílet své zkušenosti s ostatními studenty a pomoci jim při výběru studijního plánu.  
**Q**: má tento požadavek smysl?

## Případy užití (use-cases)

**TODO**:
- budou napsány na základě uživatelských příběhů

# Kvalitativní požadavky

**TODO**:
- něco o pěkné vizualizaci
- něco o málo proklikávání
- musí to být strojově zpracovatelné aby to bylo použitelné do budoucnosti
- vysvetlivky u zkratek
- vysvetleni ze tucne je povinne, kurziva volitelne, ...

# Omezení (constraints)

Řešení musí být implementováno jako rozšíření stávajícího systému RecSIS, aby bylo možné využít jeho existující infrastrukturu a data.
- databáze je PostgreSQL
- backend je napsaný v Go
- frontend využívá Go Templ pro generování HTML

**TODO**:
- data jsou ze SIS databáze, ne všechno tam prostě je
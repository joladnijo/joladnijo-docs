# Funkcionális specifikáció

### A fejlesztés célja

A fejlesztés célja a [vízió dokumentumban](vizio.md) van rövidebben összefoglalva, ütemezést a [mérföldkövek](merfoldkovek.md) tartalmaz.

### Projekt fejlesztői szótár

Az egyszerűbb megértés érdekében bevezetünk néhány - a projekten belül értelmezett - kifejezést, amit a dokumentációban
és a szoftverfejlesztés során megpróbálunk hűen követni.

Minden itt külön nem definiált kifejezés az IT zsargonban használt - jellemzően angol - szakszó.

| Kifejezés                 | Fogalom                 | Rövid definíció                                                                                                          |
|---------------------------|-------------------------|--------------------------------------------------------------------------------------------------------------------------|
| ac-admin                  | gyűjtőpont kezelője     | gyűjtőpont adatait, adománykéréseit kezelő felhasználó                                                                   |
| aid center / ac           | gyűjtőhely, gyűjtőpont  | hely, ahová a gyűjtők meghatározott adományokat fogadnak                                                                 |
| asset                     | adomány típus           | pontosított típus, pld.: pelenka, babaruha 2 éves korig, tápszer, stb.                                                   |
| asset category / category | adomány kategória       | adomány főcsoport, adomány típusok magas szintű kategorizálásához (pld: Gyermek, Ruházat, Élelmiszer, Önkéntesség)       |
| feed                      | adomány kérések listája | adomány kérések hisztorikus listája                                                                                      |
| jaj-admin                 | adminisztrátor          | szuperadmin, minden művelethez joga van más jogosultság nélkül is (jelenleg: Elek László)                                |
| org-admin                 | szervezet kezelője      | legmagasabb pozíció külső regisztrált felhasználónak, gyűjtőpontokért és szervezet adataiért felel, azokat szerkesztheti |
| organization / org        | szervezet, intézmény    | jogi entitás, ami alá a gyűjtőpontok csoportosulnak                                                                      |

# Definíciók

### Asset

Egyszerű szöveg, kategorizálást segítendő pontos adomány típus. Ezek lehetnek, pld: babakocsi, pelenka, dezodor,
ágynemű, stb. Ez a szöveg mindig megjelenik a feed elemben, asset-request létrehozáskor, szerkesztéskor,
csak `jaj-admin` által vehető fel új, a meglévőek szerkeszthetőek, módosíthatóak.

### Asset category

Névvel ellátott `asset` gyűjtemény. Az adomány típusokat összefoglaló névvel és grafikával (ikonnal) ellátott kategória.
`jaj-admin` által a név szerkeszthető, a csoport elemeit módosíthatja, újat vehet fel.

### Asset request - adomány kérés / túlcsordulás

Egy meghatározott kategóriájú adomány típus, amire egy gyűjtőhelynek szüksége / túl sok van. A kéréshez tartozik:

- Rögzítés időpontja
- Asset Category
- Asset (adomány típus)
- Jegyzet, amivel a gyűjtőhely kezelő pontosíthatja az adományt (pld: speciális élelmiszer típusban: Lisztérzékenyeknek
  is fogyaszható gluténmentes termékek)
- Státusz, hogy éppen szükség van-e arra vagy akár túl sok is van belőle
    - `urgent` : nagy szükség van rá, kérik hogy azonnal hozzanak
	- `requested`: szükség van rá, jó lenne ha hoznának
	- `not_required`: kérjük, hogy ebből ne hozzanak (többet)! (Akár azért mert már túl sok is van, akár azért mert eleve sem tudtak mit csinálni vel.)
  
Ezek mindegyike megjelenik a 'feed'-ben valamilyen formában.

### Feed

Történelmi listája a gyűjtőpontok által rögzített `asset requestek` valamennyi változásának. Gyakorlatilag egy log. Bármi történik egy `asset requesttel` létrejön egy `feed item`, mely többé nem áll közvetlen összeköttetésben az eredeti `asset requesttel`.

Megjelenítése képernyőnként eltérő lehet. 
- Egy `aid center` nézetben egyszerű, végtelen / limitált / lapozható lista. De nagyon sűrű és ráadásul oda-vissza változtatások esetén valami csoportosítás / összevonás szükséges lehet.
- Közös feed esetén (pl. címlap, vagy valamilyen szűrős lista) az azonos gyűjtőponthoz tartozó rövid időn belüli (egy óra?) változásokat csoportosítva jelenítjük meg.

Egy feedet (legyen az konkrét `aid center` saját feedje, vagy közös feed például adott `asset category`-ra szűrve) meg lehet osztani, annak változásaira fel lehet majd (MVP+) iratkozni.

### Feed Item

Egy-egy `feed` sok-sok ilyen elemből áll.

Tartozik hozzá:
- Aid Center Id, amihez tartozik
- Asset Category, amit a szülő `asset requesttől` másoltunk ide.
- Asset (adomány típus), amit a szülő `asset requesttől` másoltunk ide.
- Jegyzet (note), amit a szülő `asset requesttől` másoltunk ide.
- Az esemény (tehát önmaga létrejöttének) időpontja
- Az esemény valamilyen megnevezése. Ezek lehetnek:
	- `urgent`: sürgős státusszal jött létre, vagy sürgős státuszra módosult azaz: _"Nagy szükség van banánra!"_
	- `requested`: szükség van erre státusszal jött létre, vagy `not_required` státuszból `requested` státuszra változott, azaz: _"Szükség van banánra."_
	- `changed to requested from urgent`: eddig a státusza `urgent` volt, de most már csak `requested` azaz _Most már nem sürgős a banán, de szükség van még rá._
	- `not_required`: úgy jött létre, hogy ne hozzanak, vagy azzá lett, azaz: _"Banánt ne hozzatok!"_
	- `deleted`: eddig `urgent` vagy `requested` volt, de most már törölve lett azaz _"Már nem gyűjtünk  banánt."_
	- `changed to deleted from not_required`: eddig nem szabadott hozni, de most már hallgatunk róla azaz: _"Többé nem tilos banánt hozni."_
- (Lehet hogy jó, ha tartozik hozzá egy string ami a szülő `asset request` egyedi azonosítóját tartalmazza, hogy a rövid időn belüli oda-vissza módosításokat biztosan helyen tudjuk csoportosítani.)

Note: a `changed to` események léte, száma még formálódás alatt van.


### Organization / szervezet

A gyűjtőpontokat összefogó - jellemzően jogi entitásként is működő - szervezet. A szervezethez lehet rögzíteni:

- Szervezet teljes neve
- Adószám (ha van)
- Fogad-e pénzadományokat
- A pénzadományok pontos típusa (átutalás / revolut / bitcoin, stb)
- Szervezet adatai megerősítettek a `jaj-admin`ok által (megbízható, ellenőrzött szervezet)

### Aid-center / gyűjtőpont

Hely, ahol az `asset-request`-ben várt adományokat fogadják. Tartozik hozzá:

- Gyűjtőpont megnevezése
- Szervezet
- Gyűjtőpont néhány szavas bemutatása, jegyzet, mit érdemes tudni róluk (hogyan kapcsolódnak a szervezethez, hogy jut el
  a segítség a célhoz, kiknek gyűjtenek elsősorban, stb.)
- Irányítószám, pontos cím (részben strukturáltan: irsz, helység, közterület - házszám)
- Megközelíthetőséghez jegyzet, nyitvatartás, stb.
- GPS koordináta (térképen megjeleníthető)
- Kapcsolattartó személy, kapcsolattartási adatok
- Aktuálisan érvényes feed, `asset-request` lista

## Felhasználók által elérhető funkciók

### Publikus felületek, nem regisztrált felhasználó

#### Kezdőlap

Nem regisztrált felhasználó meg tudja nyitni a kezdőlapot, azon számára megjelenik a győjtőhelyek által generált feed,
amin a legfrissebb rögzített igények jelennek meg gyűjtőhelyenként csoportosítva A gyűjtőhely nevére, vagy a kérés
leírására kattintva a felhasználó a gyűjtőpont képernyőre navigál el.

#### Gyűjtőhely oldala
Minden az adott `aid-center`-hez tartozó adat megjelenik.

### Adminisztrációs felületek, tegisztrált felhasználó (ac-admin, org-admin, jaj-admin)

MVP utáni funkciók, átmenetileg ezek adatbázisból közvetlenül, kézzel szerkeszthetőek.

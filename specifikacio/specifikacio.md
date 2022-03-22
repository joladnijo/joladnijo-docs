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
	- `fulfilled`: kérjük, hogy ebből ne hozzanak (többet)! (Akár azért mert már túl sok is van, akár azért mert eleve sem tudtak mit csinálni vel.)
  
Ezek mindegyike megjelenik a 'feed'-ben valamilyen formában.

### Feed

Lista, amiben a gyűjtőpontok által rögzített `asset requestek` megjelennek. A feed adattartalma és megjelenési formája
képernyőnként eltérő lehet, de minden esetben egy vagy több kérést csoportosít / rendez.

A feed maga közösségi platformon megosztható legkisebb elem, ami tartalmazhatja egy gyűjtőpont alapadatait, adott
szükségleteit, illetve azok közelmúltbeli változásait.

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

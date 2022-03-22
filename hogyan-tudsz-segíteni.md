# Hogyan tudsz segíteni?
Javasoljuk, kezd a dokumentációkkal:

* [A projekt rövid leírása](specifikacio/vizio.md) az aktuális célunk
* [Specifikáció](specifikacio/specifikacio.md) ami részletesebben írja, mit hogyan szeretnénk látni a következő kiadásban
* [Mérföldkövek](specifikacio/merfoldkovek.md) pedig az ütemezés, mikorra szeretnénk ezt látni
* Előkészületben - az összes funkció amit kitaláltunk és implementálni fogunk a projekt során

#### Szervezési folyamat
A jelenlegi folyamatunk még elég hektikus, az alábbi váz alakult ki, ami alapján iterálunk:

1. Ötletelés, megvalósítandó funkciók összeírása, mérföldkő (sprint) feladatainak kijelölése, dokumentáció
2. GitHub Issue gyártás
3. Fejlesztés, standupok
4. Tesztelés, javítás (Staging környezeten)
5. Release (Teljesen publikus felületre helyezés)
6. Kezdjük újra # 1

#### Mérföldkő fejlesztésének folyamata (workflow)
- Aktuális feladatok, todolist, folyamatban lévő történések és a következő mérföldkőig tartó feladatok mint a szervezeti oldalunkon láthatóak: https://github.com/orgs/joladnijo/projects/1 (Ha 404-es hibával kidob, akkor küldj [nekem](https://github.com/borazslo) egy Github felhasználónevet és meghívlak.)
- Az egyes csapatoknak Team Leaderei vannak, akik koordinálják és következő lépéseket és döntéseket hoznak a maguk területein. A slacken megtaláljátok őket és szívesen látnak titeket.
- TL mítingek általában hétfőn este kilenckor vannak a teljes csapat terhelés nélkül, de be lehet nézni. Olykor beszámolunk az egész csapatnak hogy hogyan állunk és mindig lehet akár PM-ben javasolni nekem (PO), hogy hogyan lehetne jobban segítenem a munkátokat.
- Itt vannak fülek a feladatoknak. Most épp: _Frontend feladatok_ és _Backend feladatok_. Itt nézegessétek, hogy mi hol tart. Most csak az _alapok_ és az _MVP_ milestonba tartozókat figyelgetjük. A többi mintha ott sem volna.
- A _Todo_ oszlopban vannak azok a feladatok amikért eljött az idő. Válassz belőle, assign-al vedd magadhoz és átrakva az _In Progress_ viheted is a munkát.
- Ha kész vagy mehet a _Test_-be ahol így-úgy átnézik tesztelőink is,
- és akkor irány a _Done_.
- Ha _Done_-ba tettél valamit, akkor légyszi nézd meg a _No Status_-ban várakozó feladatokat, hogy van-e ott valami remek dolog, ami eddig blokkolva volt, de most hogy egy másikkal kész lettél így felszabadult. Ha igen, akkor tedd be a _Todo_-ba.
- Közben szükség van sok-sok [Pull Requestre ami Review-ra vár](https://github.com/pulls?q=is%3Aopen+is%3Apr+archived%3Afalse+user%3Ajoladnijo+), mert minden PR-t több szem kell lásson. Nézz és támogass!

Ha nincs a _Todo_-ban semmi, akkor szólj be a slack-re #general -ba, hogy "hahó, nincs mit csinálnom. kérek issue-t" és segítünk rajtad.
Légy bátor és vállalj issue-t.
PR Review-t meg vállalj mindig!

# A projekt

A projekt nyílt forrású (jelenleg lustaságból MIT licensz alatti), szabadon felhasználható kódokból áll. Kérlek az általad
felhasznált külső megoldások igénybevételénél ellenőrízd az támogatja-e az ilyen irányú felhasználást!

# Tech
* Open source, Github alapú, CD/CI pipeline
* API: REST Django API + JWT Bearer-Token alapú autentikáció és autorizáció
* Publikus frontend: Next.js - NodeJS - React
* Backoffice: Angular - NgRX - Nx [Fejlesztői leírás](https://github.com/joladnijo/joladnijo-backoffice/blob/main/docs/contributing.md)

| Alkalmazás modul                                           | Technológia              | Repository                                        |                                                                          |
|------------------------------------------------------------|--------------------------|---------------------------------------------------|--------------------------------------------------------------------------|
| Backend – REST API                                         | Django                   | https://github.com/joladnijo/joladnijo-backend    | [Feladatok](https://github.com/joladnijo/joladnijo-backend/issues)       |
| Frontend – Webapp (publikus oldal)                         | NodeJS - Next.js - React | https://github.com/joladnijo/joladnijo-webapp     | [Feladatok](https://github.com/joladnijo/joladnijo-webapp/issues)        |
| Frontend – Backoffice (szervezetek regisztrált segítőinek) | Angular 13               | https://github.com/joladnijo/joladnijo-backoffice | [Feladatok](https://github.com/joladnijo/joladnijo-backoffice/issues)    |

# Kóddal szemben támasztott követelmények
* Angol kód, funkciónevek, magyar kommentek
* JSON: camelCase

### Korábbi dokumentáció, ami még nem került feldolgozásra
Elavult vázlatok: [Nézetek / Wireframe](wireframes.md), [Adatstruktúra](adatstruktura.md), [Jogosultsági szintek](jogosultsagok.md)

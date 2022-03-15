# Jól adni jó - Koordinált gyűjtés

https://joladnijo.jmsz.hu

Egy minimalista honlap amin a segélyszervezetek és a velük együttműködő gyűjtőpontok (plébániák, önkormányzatok, klubbok, stb) tudják jelezni (és a jelzést frissen tartani) hogy mire van és mire nincs szükségük, igényük.

__Probléma amire válaszolunk__: Az Ukrajnából menekülők okán (is) nagyon sok helyen zajlik aktuális pillanatban nagyon sokféle gyűjtés. Sokszor már nem is tudjuk követni, hogy hol és mit gyűjtenek. Ráadásul állandóan változik a helyzet, hogy mire van szükség és mire nincs. Ezért készülhetne egy honlap ami összefogja azokat, akik szeretnék közösen kezelni a gyűjtendő dolgokat.

## __Célközönség__:
* __Adományokat gyűjtő pontok felelősei__. Első sorban a másodvonali, kisebb gyűjtőket célozzuk. Ők azok akik a hátországban gyűjtenek, akár a már befogadottak számára. Általában sokkal kisebb apparátussal és gyakorlattal. Lehetnek ők plébánia, önkormányzat, cserkész csapat, klubb, bármi. A nagy szolgálatok határmenti pontjairól feltételezzük hogy van nekik valamilyen raktárkészlet követő programjuk. (Igény szerint csatlakozhatnak persze.)
* __Kis, civil adományozók__. Rengetegen jószándékkal visznek adományokat lehetőleg egy közeli pontra. Nekik segítség hogy adott felajánlást melyik pont fogad el a közelben leginkább.

## __Scope__:
- Mobiltelefonon is normálisan működő minimalista honlap.
- Ahol a regisztrált gyűjtőpontról kiderül, hogy
    - mit gyűjt adományt / emberi erőforrást / egyebet
    - és mi az amit semmiképp nem gyűjt
    - mik az elérhetőségei a pontnak
    - milyen nagy szervezetekkel van kapcsolatban
    - valamint historikus adatok, hogy követni lehessen ha valamit gyűjtött de már nem
- Van kereshető és szűrhető lista a gyűjtpontokról 
- Van térkép a gyűjtópontokról
- Gyűjtőpontokat fenntartók intézményeket regisztrálhatnak regisztrált felhasználók és ők egyszerű felületen pár kattintással frissíthetik a listákat
- Fontos a változások jó nyomonkövetése ezért
    - fel lehet iratkozni konkrét vagy szűrt listára és a változásokról értesít emailben (messengeren is?)
    - bármelyik gyűjtópont adatlapja könnyen megosztható a facebookon amihez összesítő ábrát is csinál (akár automatikusan?) 

## __Ami nem scope__:
- Nem native mobil app
- Nem cél egy pontos raktárkészletnyilvántartó. (Még ha esetleg lehessen jelezni benne azt amiből már tényleg sok van valahol.)
- Nem cél az adományozó pontok közötti kapcsolat biztosítása. Azt a helyiek a nagy szolgálatokkal telefonon, vagy ahogy eddig is szokták csinálhatják.
- Nem cél hogy az adományozó "lefoglalhasson" vinni kívánt dolgokat. (Komoly ellenőrző munka lenne, hogy melyik ígéret valósul meg és melyik nem.)
- Nem cél konkrét szállás és/vagy fuvar feljánlásának kezelés. (Azt megteszi a segitsunk.com). Nálunk csak jelöli a gyűjtőpont hogy hozzá is be lehet küldeni ilyen információkat.
- Felajánló - felajánlás konkrét összekötés, összefűzés, összeegyeztetés nem cél.

## A csapat
- Project Owner (féle): Elek Laci SJ (elek.laszlo@jezsuita.hu)
- Önkéntes csapatunk elsődleges kommunikációs csatornája a [slack](https://joladnijo.slack.com/)en. ([Itt lehet bejutni](https://join.slack.com/t/jladnij/shared_invite/zt-14o2v6u1d-E3XUeqiP3IZAmPFIgxLqvw)). Beköszönésre lehetőség [a #4-es issunál](../../issues/4)!
- Az egyes csapatoknak Team Leaderei vannak, akik koordinálják és következő lépéseket és döntéseket hoznak a maguk területeink. A slacken megtaláljátok őket és szívesen látnak titeket.
- TL mítingek általában hétfőn este kilenckor vannak a teljes csapat terhelés nélkül, de be lehet nézni. Olykor beszámolunk az egész csapatnak hogy hogyan állunk és mindig lehet akár PM-ben javasolni nekem (PO), hogy hogyan lehetne jobban segítenem a munkátokat.
- Helye van köztük junior és senior backend, frontend, fullstack, ux, tester és szinte bármilyen más fejlesztőnek és segítőnek. Gyere bátran akár csak egy-egy fícsör fejlesztésére. Ha kevés a tapasztalatod akkor köztünk szerezhetsz bőven. 

## Hogyan segíthetsz? - Működésünk
Miután csatlakoztál a projecthez (és akár a slackhez):
- Aktuális feladatok, todolist, folyamatban lévő történések és a következő mérföldkőig tartó feladatok mint a szervezeti oldalunkon láthatóak: https://github.com/orgs/joladnijo/projects/1 (Ha 404-es hibával kidob, akkor küldj nekem egy github felhasználónevet és meghívlak.)
- Itt vannak fülek a feladatoknak. Most épp: _Frontend feladatok_ és _Backend feladatok_. Itt nézegessétek, hogy mi hol tart. Most csak az _alapok_ és az _MVP_ milestonba tartozókat figyelgetjük. A többi mintha ott sem volna.
- A _Todo_ oszlopban vannak azok a feladatok amikért eljött az idő. Válassz belőle, assign-al vedd magadhoz és átrakva az _In Progress_ viheted is a munkát.
- Ha kész vagy mehet a _Test_-be ahol így-úgy átnézik tesztelőink is, 
- és akkor irány a _Done_.
- Ha _Done_ba tettél valamit, akkor légyszi nézd meg a _No Status_-ban várakozó feladatokat, hogy van-e ott valami remek dolog, ami eddig blokkolva volt, de most hogy egy másikkal kész lettél így felszabadult. Ha igen, akkor tedd be a _Todo_ba.
- Közben szükség van sok-sok [Pull Request ami Review-ra vár](https://github.com/pulls?q=is%3Aopen+is%3Apr+archived%3Afalse+user%3Ajoladnijo+), mert minden PR-t több szem kell lásson. Nézz és támogass!

Ha nincs a _Todo_-ban semmi, akkor szólj be a slack-re #general -ba, hogy "hahó, nincs mit csinálnom. kérek issue-t" és segítünk rajtad. 
Légy bátor és vállalj issue-t.
PR Review-t meg vállalj mindig!

## Specifikáció

* open source, github alapú, CD/CI pipeline
* Elavult vázlatok: [Nézetek / Wireframe](wireframes.md), [Adatstruktúra](adatstruktura.md), [Jogosultsági szintek](jogosultsagok.md)
* backend: django - https://github.com/joladnijo/joladnijo-backend
* frontend-webapp: nodejs - https://github.com/joladnijo/joladnijo-webapp
* frontend-backoffice: auth0
* (belső) API: REST, JWT auth, verziószám nélkül. Soruce of truth: backend
* angol kód, akár magyar kommentek
* json: camelCase
* github: munka az issue branch-én, majd merghez request review a githubon, majd merge a master branch-re és így automatikus deploy a staging-en. Ha minden jó, akkor merge a production brench-be és onnan automatikusan megy a deploy.

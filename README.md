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

PO (féle): Elek Laci SJ (elek.laszlo@jezsuita.hu)

Bejelentkezésre lehetőség [a #4-es issunál](../../issues/4)!

Slack csatornánkba [itt lehet bejutni](https://join.slack.com/t/jladnij/shared_invite/zt-14o2v6u1d-E3XUeqiP3IZAmPFIgxLqvw).

## Specifikáció
* open source, github alapú, CD/CI pipeline
* Részletes [Nézetek / Wireframe](wireframes.md)
* Előkészített [Adatstruktúra](adatstruktura.md)
* További [Feature Requestek](../../issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement)

## Gyere segíteni nekünk!
Keresünk önkéntes IT szakembereket, akikkel közösen megalkothatjuk, fejleszthetjük és fenntarthatjuk ezt a projektet.
- Be lehet csatlakozni akár csak egy-egy sprintre is
- Szükség esetén online rövid status megbeszéléseket is tudunk csinálni, hogy hatékonyabban dolgozzunk együtt.
- Különösen fontos az elején olyan szakember aki az alapokat segítségünkkel felállítja
- Scrum Master féle és PM féle önkéntes pozíciókban is lehet segíteni
- Jelentkezés itt a githubon [a #4-es issunál](../../issues/4)!

## Első lépések
* specifikáció pontosítása
* [keretrendszer meghatározása](../../issues/1) (a teljesen egyedi fejlesztés túl nehéz, nem?)
* [szerver megtalálása](../../issues/3)
* CD/CI pipeline felállítása
* Valósítsuk meg!

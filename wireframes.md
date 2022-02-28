# WireFrames azaz nézetek

A nézetek wireFrame struktúrája magyarázatokkal megtalálható itt: https://miro.com/app/board/uXjVOJJy3tU=/

## Gyűjtőhely nézete
Egy konkrét gyűjtőhely adatlapja
![alt text](https://raw.githubusercontent.com/borazslo/koordinaltgyujtes/main/viewGyujtopont.jpg "Egy gyűjtőpont nézete")

## Listanézet
Különféle szűrökkel ellátott listanézet
![alt text](https://raw.githubusercontent.com/borazslo/koordinaltgyujtes/main/viewList.jpg "Lista nézet")

## Új gyűjtőhely létrehozása
__Az intézményválasztó részhez:__
- default érték a felhasználó ABC-ben első intézménye
- normálisan választható a felhasználó valamennyi intézménye
- utána van egy "új intézmény felvitele" gomb. Ekkor minden szükséges adatot kitöltve létrejön egy új intézmény. Ki kell pipálnia, hogy "ehhez az intézményhez tartozik a felhasználó legalább mint kapcsolattartó?" és létrejön a felhasználó-intézmény relation a lookup table-ban, de validated = false
- esetleg ott lehet az összes többi intézmnény is szükrével lejjebb. ha azok közül választ akkor feldobja az üzenetet: "legalább kapcsolattartó vagy az intézménnyel"? Ha igent válaszol akkor jön csak létre a dolog és akkor létrejön a felhasználó-intézmény relation is szintén validated= false értékkel.

__Cím:__

Lehessen koordinátát választani húzogatott pointerrel is valami térképen.

## Térkép nézete
Lehetne ilyen is

## Menü
![alt text](https://raw.githubusercontent.com/borazslo/koordinaltgyujtes/main/viewMenu.jpg "Menü")

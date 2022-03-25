# Jogosultság rendszer

A jogosultság meghatározása három részből áll:

- Felhasználó saját jogosultságai, melyet a belépés során kap (Pld: "saját" gyűjtőpontot szerkeszthet)
- Felhasználó a rendszer objektumaihoz kapcsolása által (pld: jogosultságot szerez egy gyűjtőponton)
- Objektum saját egyénileg szabályozott jogosultságai (pld: ne törölhessen szervezetet, ha van alatta gyűjtőpont)

## Jogosultsági token felépítése

A jogosultsági token 3 részből áll, ami szabályozza, hogy egy-egy erőforráshoz az adott felhasználónak milyen
jogosultsága van: `Erőforrás`, `Művelet (CRUDA)`, `Szkóp`, ezeket a [JWT Token](belepes-auth.md) `permissions` része
tartalmaz.

### Felépítése

A permision token egy string lista, amelyben minden string három részre bomlik, ami `:` karakterrel van összefűzve, ezek
rendre:
`(Erőforrás):(Művelet):(Szkóp)`

Ez a string nem különböztet meg kis és nagybetűt, konvenció alapján végig kisbetűs, de a hiba kizárási lehetősége miatt
célszerű kisbetűssé alakítani vizsgálat előtt.

Az erőforrás minden esetben egy 1 vagy több karakter hosszú string, míg a `Művelet` és `Szkóp` minden esetben csak egy
karakter lehet.

#### Erőforrás

Jellemzően endpointokhoz köthető, de a felületen megjelenő elemekre is hatással lehet, egy adott erőforrás típusát
határozza meg.

Ezek pld: `aid-center`, `org`, `asset-request`, `sms` stb.

#### Művelet (CRUDA)

Minden esetben 1 karaktert tartalmaz, amelyek az alábbiak valamelyike:

- `C`: Create, létrehozhatja
- `R`: Olvashatja / megtekintheti
- `U`: Módosíthatja (törlés nélkül)
- `D`: Törölheti (módosítás nélkül)
- `A`: Mind a 4 műveleti jog (CRUD)

#### Szkóp

A jogosultságok szkpója meghatározza, hogy az adott jogosultság minden erőforráson (minden erőforráson értelmezett) vagy
kapcsolt (örökölt) jogosultságokat takar (self).

- Minden `a` - All, művelet engedélyezhető kapcsolattól függetlenül
- Csak saját `s` - Self, kapcsolat vizsgálat szükséges 

Az adott erőforráson `a` - minden joggal rendelkező felhasználó **korlátozás nélkül** hajthat végre az adott erőforráson
műveleteket.

Az erőforráson `s` saját / jogosult joggal rendelkező esetén **meg kell vizsgálni**, hogy az elérni kívánt erőforráshoz
kapcsolódó jogosultságok lehetővé teszik-e az adott erőforráson az adott műveletet.


| Erőforrás     | Művelet (CRUD) | Szkóp | Claim string (JWT)   | Publikus? | Leírás                                       |
|---------------|----------------|-------|----------------------|-----------|----------------------------------------------|
| org           | a              | a     | `org:a:a`            | -         | Szervezetek Adminisztrátora                  |
| org           | r              | a     | `org:r:a`            | +         | Megtekintheti a szervezeteket                |
| org           | c              | s     | `org:c:s`            | -         | Saját szervezetet létrehozhat                |
| org           | u              | s     | `org:u:s`            | -         | Saját szervezetet módosíthat                 |
| org           | d              | s     | `org:d:s`            | -         | Saját szervezetet törölhet                   |
| aidcenter     | a              | a     | `aidcenter:a:a`      | -         | Gyűjtőpontok Adminisztrátora                 |
| aidcenter     | r              | a     | `aidcenter:r:a`      | +         | Gyűjtőpontokat megtekinthet                  |
| aidcenter     | c              | s     | `aidcenter:c:s`      | -         | Saját szervezetben gyűjtőpontot létrehozhat  |
| aidcenter     | u              | s     | `aidcenter:u:s`      | -         | Saját szervezetben gyűjtőpontot módosíthat   |
| aidcenter     | d              | s     | `aidcenter:d:s`      | -         | Saját szervezetben gyűjtőpontot törölhet     |
| asset-request | a              | a     | `asset-request:a:a`  | -         | Bármilyen gyűjtőponton kezelheti a kéréseket |
| asset-request | r              | a     | `asset-request:r:a`  | +         | Bármilyen kérést megtekinthet                |
| asset-request | c              | s     | `asset-request:c:s`  | -         | Saját gyűjtőponton létrehozhat kérést        |
| asset-request | u              | s     | `asset-request:u:s`  | -         | Saját gyűjtőponton módosíthat kérést         |
| asset-request | d              | s     | `asset-request:d:s`  | -         | Saját gyűjtőponton törölhet kérést           |


## Javasolt döntési fa API endpoint esetén

Legyen egy `aid-center` endpoint ahol a felhasználó létre szeretne hozni egy új `asset-request` -et:

- A BE megvizsgálja, hogy az AccesTokenben van-e `assset-request:a:a` jog vagy `asset-request:c:s` jog, ha nincs,
  megtagadja a kérést.
- Amennyiben csak `asset-request:c:s` joga van, megvizsgálja, hogy valamilyen módon kapcsolódik-e az adott `aid-center`
  hez (`org` vagy `aid-center`en keresztül van-e rá joga?), ha nincs megtagadja a kérést.
- Mivel vagy `asset-request:c:s` és kapcsolt felhasználó vagy `asset-request:a:a` és adminisztrátor, így végrehajtja a
  kérést.


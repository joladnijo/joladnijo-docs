# Az adatstruktúra

## Address (Cím)
* __aid_center__ (_foreign key (1:1)_): 
* __country_code__ (_varchar(3)_): kétbetűs ISO kódja az országnak
* __postal_code__ (_varchar(10)_): irányítószám (külföld miatt sokféle lehet)
* __city__ (_varchar(50)_): város neve (hely nyelven?)
* __address__ (_varchar(100)_): utca, házszám, vagy ami van
* __note__ (_varchar(255)_): pl. "a Thököly út felől"

## AidCenters (Gyűjtőhelyek)
Például: pirpócsi Kovács Tihamér Művelődésiház
* __id__ (_uuid_)*:  teljesen egyedi UUID azonosító
* __name__ (_string_)*: név
* __photo__ (_string_): fénykép jpg fájl relatív elérhetősége adott képek mappához képest
* __slug__ (_string_)*: url kompatibilis rövid név
* __organization__ (_int_)*: foreign key az _Organizations_ táblához
* MVP után: __nationalOrganizations__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.)
* __address__ (_foreignKey_): _Address.aid_center_
* __geoLocation__ (_point_)*: koordináták, hogy odataláljunk
* __contact__ (_foreignKey__): nyilvános kapcsolatartói adatok. _Contacts_ táblával összeközve
* __lastUpdate__ (_timestamp_)*: frissítettség időntja
* __callRequired__ (_enum('required','suggested',false,'denied')_): Adomány szállítás előtt szeretnék-e ha felvínák őket telefonon. Mindenkép / Lehetőleg / N/A / Légyszi ne.
* __assetsRequested__ (_look up table, multiple_): az _Assets_ táblával van összekötve. Amire szükség van.
* __assetsFulfilled__ (_look up table, multiple_): az _Assets_ táblával van összekötve. Amire már nincs szükség (de azért legyen kiírva)
* __assetsOverloaded__ (_look up table, multiple_): az _Assets_ táblával van összekötve. Amiből már annyi van mint a csuda. Vihetik mások is. 
* __moneyAccepted__ (_boolean_): fogad-e pénzadományt
* __moneyDescription__ (_longText_): egybe html formázva újsorokkal akár linkekkel bankszámlaszám meg amit akartok (_vagy legyen több külön mező?_)
* __note__ (_string_): bármilyen további leírás. pl hogy hánytól hányig, vagy valami egyéb
* __campaignEnding__ (_timestamp_): Meg lehet adni, hogy a gyűjtés lejárjon magától. Vagy amikor kikapcsolják, akkor a leállítás időpőntját adja meg zárásnak és így leáll.

unique('_slug_') -> viszont változáskor meg kellene őriznünk a régit is talán, hogy az oldalra mutató linkek ne törjenek el?

unique('_name_') -> biztos?

## AssetRequests
Például: Pirpócsi gyűjtőpontnak élelmiszer kategóriában műzli szelet fajta adomány kell, a leírásban az van, hogy "kifejzetten kókuszos a menő"
* __id__ (_int_):  azonosító
* __aidCenterId__ (foreign key, _int_): hogy melyik gyűjtőponthoz tartozik ez a konkrét szükség
* __category__ (_enum_): többféle típus lehet - tárgyi adomány, emberi erőforrás keresése/ajánlása, szállás típusú adomány, stb.
* __name__ (_enum_): jó sokféle dolog lehet ez: asztal, ágy, cipő, ruha, stb.
* __icon__ (_string_): a hozzátartozó ikon elérhetősége (ha a type-nak nem volt ikonja, akkor a categoriból szerzi)
* __note__ (_string_): a részletes leírás, ami már nem kereshető. pl: "kifejezetten narancsosat keresünk és jó sokat"
* __urgent__ (_boolean_): ha fontos, kiemelt, sürgős akkor kipipálható. MVP után: Ennek változása azonnali üzenetet eredményez felirakozónak / fb-ra / stb.

Megjegyzés: lehetne hogy mindig össze legyen kötve az Asset-el, de így jobban meg tudjuk őrizni a történelemnek, hogy mik voltak akkor is ha pár Asset kifut a forgalomból.

unique('_aidCenterId-category-type_')

## Assets & AssetCategories
Például: szappantartó
* __id__ (_int_):  azonosító
* __name__ (_enum_): jó sokféle dolog lehet ez: asztal, ágy, cipő, ruha, stb.
* __icon__ (_string_): a hozzátartozó ikon elérhetősége (ha a type-nak nem volt ikonja, akkor a categoriból szerzi)
* __isCategory__ (_booelan_): az asset kategóriák (pl élelmiszer) és az assetek (pl: műzli szelet) ugyan olyanok csak kiemeltek a kategóriák
* __parentId__ (_int_): ha ő valami alá tartozik. általában if isCategory ? parentId = false : parentId = true

## Contacts
* __organization*__ (_foreign key_)
* __aid_center__ (_foreign key (1:1, nullable)_)
* __phone__ (_varchar(20)_): telefonszám, vagy telefonszámok (pontosvesszővel elválasztva)
* __email__ (_varchar(255)_): email cím
* __facebook__ (_varchar(255)_): facebook teljes vagy uri elérhetőség
* __url__ (_varchar(255)_): http-vel vagy anélkül. Ha nincs eleje, akkor feltételezzük, hogy https 
* __name__ (_varchar(255)_): kapcsolattartó neve akit nyilvánosan fel lehet hívni (nekünk van egy felhasználónk is általában)
* __note__ (_varchar(255)_): a hellyel való kapcsolathoz kiegészítő infó. 


## Organizations (Intézmény, vagy akár országos szervezet)
Például: Piripócsi Önkormányzat
* __id__ (_int_):  azonosító
* __name__ (_string_): név
* (MVP után: __logo__ (_string_): url a logójához)
* __contact__ (_foreignKey__): nyilvános kapcsolatartói adatok. _Contacts_ táblával összeközve
* __note__ (_string_): a hellyel való kapcsolathoz kiegészítő infó. 
* MVP után: __isNational__ (_boolean_): ő maga nagy szervezet-e annyira, hogy a _nationalOrganizations_ be belekerülhessen
* (MVP után: __nationalOrganizations__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.))
* __note__ (_string_): bármilyen további leírás. pl ősi szervezet vagy mi.
* (__users__ (_look up table, multiple_): a _Users_ csatlakozhatnak egy-egy intézményhez és akkor az ő elérhetőségeik a fontosak.)


## Users
* __id__ (_int_)*:  azonosító
* __username__ (_string_)*: felhasználónév
* __name__ (_string_)*: hivatalos név
* __phone__ (_string_)*: telefonszám. legyen kötelező.
* __email__ (_string_)*: email cím
* (__organizations__ (_look up table, multiple_): a _Felhasználók_ csatlakozhatnak egy-egy intézményhez. Az intézmény oldaláról van definiálva?)
* __isadmin__ (_boolean__)*: nincs túl sok szintű felhasználó. admin vagy intézményhez tartozó valaki
* __validated__ (_enum(0,1,2_): azonosítva van-e a felhasználó? 0 = nem; 1 = email alapján (regisztrációkor); 2 = fel is hívtuk kézzel telefonon

## Feed
A változtatásokat követni szeretnék minden gyűjtőhelyen.
Kérdés: lehet hogy a lookup gyűjtőpont-adomány igazából egyben van ezzel a táblával?
* __id__ (_int_):  azonosító
* __userId__ (_int_): foreignKey a Users táblához
* __assetRequestId__ (_int_): foreignKey az assetRequest táblához
* __date__ (_timestamp_)
* __event__ (_enum_): hogy mi történt pl. addedAdomány, removedAdomány, modPénzügyek, modCímadatok, stb.


## (MVP után!) lookUp: Organizations
* __organizationId__ (_int_):  Intézmények azonosító
* __nationalOrganizationId__ (_int_): Az országos intézmény azonosítója ahova az intézmény tartozik
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről
( * __affiliation__ (_string_): Le lehet írni a kötődés milyenségét, de opcionális )

unique('_organizationId_-_nationalOrganizationId_')

## lookUp: Users
* __userId__ (_int_):  _Users_ azonosító
* __type__ (_enum('aidCenter','organization')_): Hogy a kapcsolat csak gyűjtőponthoz vagy intézményhez tartozik
* __foreignId__ (_int_):  _aidCenter_ vagy _organization_ azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről
* __affiliation__ (_string_): Ide lehet írni, hogy "hivatalos kapcsolattartó" vagy "önkéntes" vagy "munkatárs"

unique('_userId_-_type_-_foreignId_')


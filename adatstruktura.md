# Az adatstruktúra

## AidPoints (Gyűjtőhely)
Például: pirpócsi Kovács Tihamér Művelődésiház
* __id__ (_int_)*:  azonosító
* __name__ (_string_)*: név
* __slug__ (_string_)*: url kompatibilis rövid név
* __organization__ (_int_)*: foreign key az _Organizations_ táblához
* MVP után: __nationalOrganizations__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.)
* __addressCountryCode__ (_string(2)_): kétbetűs ISO kódja az országnak
* __addressPostalCode__ (_string_): irányítószám (külföld miatt sokféle lehet)
* __addressCity__ (_string_): város neve (hely nyelven?)
* __addressStreet__ (_string_): utca, házszám, vagy ami van
* __addressNote__ (_string_): pl. "a Thököly út felől"
* __geoLocation__ (_point_)*: koordináták, hogy odataláljunk
* __phone__ (_string_): telefonszám, vagy telefonszámok (pontosvesszővel elválasztva)
* __email__ (_string_): email cím
* __facebook__ (_string_): facebook teljes vagy uri elérhetőség
* __url__ (_string_): http-vel vagy anélkül. Ha nincs eleje, akkor feltételezzük, hogy https 
* __contactName__ (_string_): kapcsolattartó neve akit nyilvánosan fel lehet hívni (nekünk van egy felhasználónk is általában)
* __contactNote__ (_string_): a hellyel való kapcsolathoz kiegészítő infó. 
* __lastUpdate__ (_timestamp_)*: frissítettség időntja
* __assetsRequested__ (_look up table, multiple_): az _Assets_ táblával van összekötve. Amire szükség van.
* __assetsFulfilled__ (_look up table, multiple_): az _Assets_ táblával van összekötve. Amire már nincs szükség (de azért legyen kiírva)
* __assetsOverloaded__ (_look up table, multiple_): az _Assets_ táblával van összekötve. Amiből már annyi van mint a csuda. Vihetik mások is. 
* __moneyAccepted__ (_boolean_): fogad-e pénzadományt
* __moneyDescription__ (_longText_): egybe html formázva újsorokkal akár linkekkel bankszámlaszám meg amit akartok (_vagy legyen több külön mező?_)
* __note__ (_string_): bármilyen további leírás. pl hogy hánytól hányig, vagy valami egyéb
* __campaignEnding__ (_timestamp_): Meg lehet adni, hogy a gyűjtés lejárjon magától. Vagy amikor kikapcsolják, akkor a leállítás időpőntját adja meg zárásnak és így leáll.

unique('_slug_') -> viszont változáskor meg kellene őriznünk a régit is talán, hogy az oldalra mutató linkek ne törjenek el?
unique('_name_') -> biztos?

## Assets
Például: szappantartó
* __id__ (_int_):  azonosító
* __category__ (_enum_): többféle típus lehet - tárgyi adomány, emberi erőforrás keresése/ajánlása, szállás típusú adomány, stb.
* __type__ (_enum_): jó sokféle dolog lehet ez: asztal, ágy, cipő, ruha, stb.
* __icon__ (_string_): a hozzátartozó ikon elérhetősége (ha a type-nak nem volt ikonja, akkor a categoriból szerzi)
* __name__ (_string_): amire tényleg szükség van (egyesszám)
* __note__ (_string_): a részletes leírás, ami már nem kereshető. pl: "kifejezetten narancsosat keresünk és jó sokat"


## Organization (Intézmény, vagy akár országos szervezet)
Például: Piripócsi Önkormányzat
* __id__ (_int_):  azonosító
* __name__ (_string_): név
* __logo__ (_string_): url a logójához
* __phone__ (_string_): telefonszám, vagy telefonszámok (pontosvesszővel elválasztva)
* __email__ (_string_): email cím
* __facebook__ (_string_): facebook teljes vagy uri elérhetőség
* __contactName__ (_string_): nyilvános kapcsolattartó neve. (nekünk van általában egy felhasználónk is)
* __contactNote__ (_string_): a kapcsolati móddal való kapcsolathoz kiegészítő infó. 
* __note__ (_string_): a hellyel való kapcsolathoz kiegészítő infó. 
* MVP után: __isNational__ (_boolean_): ő maga nagy szervezet-e annyira, hogy a _nationalOrganizations_ be belekerülhessen
* (MVP után: __nationalOrganizations__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.))
* __note__ (_string_): bármilyen további leírás. pl ősi szervezet vagy mi.
* (__users__ (_look up table, multiple_): a _Users_ csatlakozhatnak egy-egy intézményhez és akkor az ő elérhetőségeik a fontosak.)

## Felhasználó
* __id__ (_int_)*:  azonosító
* __username__ (_string_)*: felhasználónév
* __name__ (_string_)*: hivatalos név
* __phone__ (_string_)*: telefonszám. legyen kötelező.
* __email__ (_string_)*: email cím
* (__intezmenyek__ (_look up table, multiple_): a _Felhasználók_ csatlakozhatnak egy-egy intézményhez. Az intézmény oldaláról van definiálva?)
* __isadmin__ (_boolean__)*: nincs túl sok szintű felhasználó. admin vagy intézményhez tartozó valaki
* __validated__ (_enum(0,1,2_): azonosítva van-e a felhasználó? 0 = nem; 1 = email alapján (regisztrációkor); 2 = fel is hívtuk kézzel telefonon

## feed / watchdog
A változtatásokat követni szeretnék minden gyűjtőhelyen.
Kérdés: lehet hogy a lookup gyűjtőpont-adomány igazából egyben van ezzel a táblával?
* __id__ (_int_):  azonosító
* __date__ (_timestamp_)
* __user__ (_int_): foreignKey az Felhasználóhoz
* __type__ (_enum_): hogy mi történt pl. addedAdomány, removedAdomány, modPénzügyek, modCímadatok, stb.
* __log__ (_string_): hogy mi is történt. Pl: "nem fogad már több pokrócot"

## lookUp: Gyűjtőhelyek - OrszágosSzervezetek
* __helyId__ (_int_):  Gyűjtőhelyek azonosító
* __országosId__ (_int_):  OrszágosSzervezetek azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről

unique('_helyId_-_orszagosId_')

## lookUp: Intézmények - OrszágosSzervezetek
* __intézményId__ (_int_):  Intézmények azonosító
* __országosId__ (_int_):  OrszágosSzervezetek azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről

unique('_intézményId_-_orszagosId_')

## lookUp: Felhasználók - Intézmények
* __intézményId__ (_int_):  Intézmények azonosító
* __userId__ (_int_):  Felhasználók azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről

unique('_intézményId_-_userId_')

## lookup: Gyűjtőhelyek - Gyűjtenivelók
Kérdés: lehet hogy a feed/watchdoggal igazából egyben van ezzel a táblával?
* __helyId__ (_int_):  Gyűjtőhelyek azonosító
* __adomanyId__ (_int_):  Gyűjtenivaló azonosító
* __type__ (_enum_): várják / nem várják / teli készlet
* __note__ (_string_): részletesebb leírás, vagy mennyiség, vagy bármi
* __flag__ (_boolean_): lehessen kiemelni / sürgőssé tenni gyűjtenivalót. (Kérdés: akár elavulhasson automatikusan. vagy a type-ba beleépíteni?)

unique('_helyId_-_adomanyId_-_type_')

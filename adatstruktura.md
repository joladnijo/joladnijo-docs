#Az adatstruktúra

## Gyűjtőhely
Például: pirpócsi Kovács Tihamér Művelődésiház
* __id__ (_int_)*:  azonosító
* __name__ (_string_)*: név
* __intezmeny__ (_int_)*: foreign key az _Intézmény_ táblához
* __addressCountryCode__ (_string(2)_): kétbetűs ISO kódja az országnak
* __addressPostalCode__ (_string_): irányítószám (külföld miatt sokféle lehet)
* __addressCity__ (_string_): város neve (hely nyelven?)
* __addressStreet__ (_string_): utca, házszám, vagy ami van
* __geoLocation__ (_point_)*: koordináták, hogy odataláljunk
* __phone__ (_string_): telefonszám, vagy telefonszámok (pontosvesszővel elválasztva)
* __email__ (_string_): email cím
* __facebook__ (_string_): facebook teljes vagy uri elérhetőség
* __orszagosSzervezetek__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.)
* __lastUpdated__ (_timestamp_)*: frissítettség idpntja
* __adományokJöhetnek__ (_look up table, multiple_): a _Gyűjtenivalók_ közül mik vannak itt beikszelve
* __adományokNeJöjjenek__ (_look up table, multiple_): a _Gyűjtenivalók_ közül mik vannak itt beikszelve
* __pénzAdományok__ (_boolean_): fogad-e pénzadományt
* __pénzAdományokLeírás__ (_longText_): egybe html formázva újsorokkal akár linkekkel bankszámlaszám meg amit akartok (_vagy legyen több külön mező?_)
* __comment__ (_string_): bármilyen további leírás. pl hogy hánytól hányig, vagy valami egyéb
* __endDate__ (_timestamp_): Meg lehet adni, hogy a gyűjtés lejárjon magától. Vagy amikor kikapcsolják, akkor a leállítás időpőntját adja meg zárásnak és így leáll.

## Gyűjtenivalók
Például: szappantartó
* __id__ (_int_):  azonosító
* __name__ (_string_): név (egyesszám)
* __type__ (_enum_): 3 féle típus - tárgyi adomány, emberi erőforrás keresése/ajánlása, szállás típusú adomány
* __icon__ (_string_): a hozzátartozó ikon elérhetősége

## Intézmény
Például: Piripócsi Önkormányzat
* __id__ (_int_):  azonosító
* __name__ (_string_): név
* __phone__ (_string_): telefonszám, vagy telefonszámok (pontosvesszővel elválasztva)
* __email__ (_string_): email cím
* __facebook__ (_string_): facebook teljes vagy uri elérhetőség
* __orszagosSzervezetek__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.)
* __comment__ (_string_): bármilyen további leírás. pl hogy hánytól hányig, vagy valami egyéb
* __contacts__ (_look up table, multiple_): a _Felhasználók_ csatlakozhatnak egy-egy intézményhez és akkor az ő elérhetőségeik a fontosak.


## OrszágosSzervezet
Például: Magyar Máltai Szeretetszolgálat
* __id__ (_int_):  azonosító
* __name__ (_string_): név
* __contactName__ (_string_): kapcsolattartó neve akit az adminok felhívhatnak hogy adott tagszervezet hozzájuk tartozik-e
* __contactPhone__ (_string_): előző telefonszáma
* (__Intézmények__ (_look up table, multiple_): melyek azok az al-intézmények akikkel együttműködnek. Definiálva az _Intézmény_ felől van. Itt csak megjelenik.)

## Felhasználó
* __id__ (_int_)*:  azonosító
* __username__ (_string_)*: felhasználónév
* __name__ (_string_)*: hivatalos név
* __phone__ (_string_)*: telefonszám. legyen kötelező.
* __email__ (_string_)*: email cím
* (__intezmenyek__ (_look up table, multiple_): a _Felhasználók_ csatlakozhatnak egy-egy intézményhez. Az intézmény oldaláról van definiálva?)
* __isadmin__ (_boolean__)*: nincs túl sok szintű felhasználó. admin vagy intézményhez tartozó valaki

## watchdog
A változtatásokat követni szeretnék minden gyűjtőhelyen.
* __id__ (_int_):  azonosító
* __date__ (_timestamp_)
* __user__ (_int_): foreignKey az Felhasználóhoz
* __type__ (_enum_): hogy mi történt pl. addedAdomány, removedAdomány, modPénzügyek, modCímadatok, stb.
* __log__ (_string_): hogy mi is történt. Pl: "nem fogad már több pokrócot"

## lookUp: Gyűjtőhelyek - OrszágosSzervezetek
* __helyId__ (_int_):  Gyűjtőhelyek azonosító
* __országosId__ (_int_):  OrszágosSzervezetek azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről

## lookUp: Intézmények - OrszágosSzervezetek
* __intézményId__ (_int_):  Intézmények azonosító
* __országosId__ (_int_):  OrszágosSzervezetek azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről

## lookUp: Felhasználók - Intézmények
* __intézményId__ (_int_):  Intézmények azonosító
* __userId__ (_int_):  Felhasználók azonosító
* __validated__ (_boolean_): hogy jó van-e hagyva a felsőbb szervet részéről
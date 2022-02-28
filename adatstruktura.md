#Az adatstruktúra

## Gyűjtőhely
* __id__ (_int_):  azonosító
* __name__ (_string_): név
* __intezmeny__ (_int_): foreign key az _Intézmény_ táblához
* __addressCountryCode__ (_string(2)_): kétbetűs ISO kódja az országnak
* __addressPostalCode__ (_string_): irányítószám (külföld miatt sokféle lehet)
* __addressCity__ (_string_): város neve (hely nyelven?)
* __addressStreet__ (_string_): utca, házszám, vagy ami van
* __geoLocation__ (_point_): koordináták, hogy odataláljunk
* __orszagosSzervezetek__ (_look up table, multiple_): melyek azok az országos szervezetek akikkel együttműködnek vannak (pl. Málta, Ökumenikus, stb.)
* __lastUpdated__ (_timestamp_): frissítettség idpntja
* __adományokJöhetnek__ (_look up table, multiple_): a _Gyűjtenivalók_ közül mik vannak itt beikszelve
* __adományokNeJöjjenek__ (_look up table, multiple_): a _Gyűjtenivalók_ közül mik vannak itt beikszelve
* __pénzAdományok__ (_boolean_): fogad-e pénzadományt
* __pénzAdományokLeírás__ (_longText_): egybe html formázva újsorokkal akár linkekkel bankszámlaszám meg amit akartok (_vagy legyen több külön mező?_)


## Gyűjtenivalók

## Intézmény

## OrszágosSzervezet

## Felhasználó

## watchdog
változtatások

## lookUp: Gyűjtőhelyek - OrszágosSzervezetek
# Mérföldkövek

[Aktuális állás - projekt board](https://github.com/orgs/joladnijo/projects/1)

# MVP

Tervezett kiadás: 2022. április 1.

---

### Tervezés
- Architektúra és célok meghatározása
- MVP funkcionalitás meghatározása
- Dokumentáció

### Build rendszer
- Build rendszerek kialakítása amivel az alkalmazást Github-on beolvasztott PR-ok után egyből lehet staging és production környezetre tenni

### Alkalmazások
#### Webapp
- Kezdőlap összes gyűjtőpont feedjével
- Gyűjtőpontok landing oldalai

#### Backend
- Adatbázis struktúra kialakítása a Webapp kéréseinek kiszolgálására
- API kialakítása

# (Később)
Itt azok a specifikációba illő elemek és információk vannak, amik még nincsenek konkrét mérföldkőbe besorolva. Ha innen valami elkerül az aktuális mérföldkőhöz, akkor a specifikáció megfelelő részeibe is bele kell kerüljön.

### Aid-center
- Fotót is megjelenít az aid-centerről (feltölthető, törölhető, stb.)
- Tartoznak hozzá a pénzbeli adományok fogadásához szükséges adatok mezői, valamint egy flad / boolean hogy éppen fogad-e pénzadományokat vagy sem.
- Fel lehet iratkozni az aid-center változásaira, azaz elsőre a hozzátartozó feed változásaira.
- Facebook megosztás gombra kattintva félig előkészített posztot lehet csinálni az összefoglaló adatokból.
- Az aid-center aktuális szükségleteit összefoglaló jpg kép készül frissítettség időpontjával és rövid assetrequest.name szövegekkel (.note nélkül).
- widgetként beilleszthetőek a szükségletek és alap aid-center adatok más honlapokba
- Kikapcsolható ill. dátummal határidőre kikapcsolható a teljes adománygyűjtés egy aid-centernél az asset-requestek törlése nélkül. De legyen belőle feed-item.

### Contact 
- `affiliation`: A kapcsolattartó adatainál megadható, hogy milyen viszonyban van az adott intézménnyel / gyűjtőponttal

### Feed
- A feedet hozzá lehet kötni facebook oldalhoz vagy csoporthoz és akkor a változásokat (rövid időn belüliket összevonva) oda is posztolja.
- Fel lehet iratkozni emailes értesítésre bármely feedhez (azonnali / napi / heti)
- Fel lehet iratkozni SMS értesítésre bármely feedhez (azonnali / napi / heti)
- Fel lehet iratkozni facebook messenger bot értesítésre bármely feedhez (azonnali / napi / heti)
- AssetRequest változásokon kívül másféle FeedItemek is lehetséges azaz egyféle értesítés / posztolás. Pl.: _"Köszönjük az eddigi támogatásokat, hálából szombaton nyílt nap lesz."_
- paging (info a headerekben)

### FeedItem
- ac-admin (minimum) tud törölni hozzá tartozó aid-centerekhez tartozó feedItemeket (pl, ha oda-vissza állítgatott pár másodpercen belül is így sok a zaj)

### egyéb
- i18n 
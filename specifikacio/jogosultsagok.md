# Jogosultságok

**Alapvetően minden jogosultság tiltott, ha nincs külön engedélyezve.**

Jelenleg három nagy csoportba soroljuk a jogosultságokat:

- Publikus (korlátozás, autentikáció nélküli) elérhető erőforrások
- Szervezeti adminisztrátorok által elérhető erőforrások
- JAJ-Admin által elérhető erőforrások

Ezek később tovább finomodnak (osztódnak szét), így a jogosultság kezelés kialakításánál figyelembe kell ezt venni.

# Publikus jogosultságok

Megtekinthet:
- publikus feedeket (ami nem járt le)
- szervezeteket
- gyűjtőpontokat
- azok adatait (hozzárendelt felhasználók kivételével)
- feedjeit

## Az`ac-admin` jogosultságok

Minden publikus jogosultság, illetve Létrehozhat / módosíthat:

- Szervezetet (1-et hozhat létre, annak jogosultságait megörökli)
- Gyűjtő központot (azon szervezet alá, ahova jogosult)
- Adomány kérést a gyűjtőközponthoz (azon szervezet alá tartozó, vagy központhoz kapcsolt joggal, ahova jogosult)
- Láthatja a jogosult szervezethez / központhoz tartozó felhasználókat

Későbbiekben a szervezet, központ, központ kezelői jogosultságot szeretnénk szétbontani, így ezeknek a jogoknak a
finomhangolására fel kell készülnünk.

## Az`jaj-admin` jogosultságok

A `jaj-admin`-nak mindent lehet amit a korábban felsorolt jogosultságokkal lehetséges annyi kivétellel, hogy minden
központon, gyűjtőponton korlátozás nélkül. 

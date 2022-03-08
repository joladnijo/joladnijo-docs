# Jogosultsági szintek 
Eleinte minimalista a jogrendszer és jó sok mindent még az adatbázisba nyúlva kell megoldani. Aztán fejlődünk majd.

## Adminok (users.isAdmin)
Egyszerű flag amivel valaki adminná válik és mindent tehet:
- módosíthat (MVP után létrehozhat) AidCenter-t
- módosíthat (MVP után létrehozhat) Organization-t
- módosíthat bármely AidCenterhez tartozó AssetRequesteken (ezáltalán létrehozhat, módosíthat, törölhet AssetRequest-et)
- még ő sem nyúlhat Assets táblához, nem törölhet AidCenter-t se Organization-t, nem módosíthat az lookup_users-en 

Későbbiekben
- létrehozhat AidCenter-t (ne törölhessen)
- létrehozhat Organization-t (ne törölhessen)
- létrehozhat, törölhet, és módosíthat a lookup_users-en
- létrehozhat, törölhet, és módosíthat a lookup_organizations-ön
- módosíthat az Users-en bizonyos részeket

## Karbantartók (lookup_users)
Egyes felhasználó több Organization-höz és több AidCenterhez is tartozhat.

Aki hozzá van rendelve egy Organization-höz ő valamennyi oda tartozó AidCenterhez hozzáférhet.

- módosíthat sok mindent az AidCenteren
- módosíthat minden az AidCenterhez tartozó AssetRequest-en (ezáltalán létrehozhat, módosíthat, törölhet AssetRequest-et)
- a saját Organization-én (ha van) módosíthat a legtöbb mindent
- láthatja hogy az egyes feediItemeket melyik felhasználó hozta létre

Későbbiekben
- létrehozhat AidCenter-t a saját Organizationjain belül (ne törölhessen)
- láthatja az általa elért Organization-ökhöz és AidCenter-ekhez tartozó többi felhasználót

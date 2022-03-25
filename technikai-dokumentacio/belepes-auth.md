# Belépés, autorizáció, autentikáció

A belépéshez és a jogosultsági szabályozásokhoz OAuth2-es megoldást választottunk, így egy központi szerveren lehet a
jogosultságok jelentős részét menedzselni.

Fejlesztői [Auth0](https://auth0.com) account hozzáférésekért Slack-en keresd Fibinger Ádámot vagy Elek Lacit.

#### Végtelenül leegyszerűsítve a belépési folyamat:

- A felhasználó elnavigál az adminisztrációs felületre
- A felület észleli, hogy nincs érvényes ID és Access tokenje, amivel lehet a backendnél kopogtatni, elzavarja a
  belépésre
- `Auth0` -ra átirányítva a felhasználó valamilyen módon belép (social login, user / pass, stb), visszairányítja a
  felületre egy ID tokennel
- A felület látva, hogy megjött a felhasználó egy szép ID tokennel, bekérdez az Auth0 fele, hogy a usernek szerezzen egy
  Access Tokent
- Az Access Tokennel pedig boldogan elkezd kommunikálni a BE-vel, mivel az tartalmazza a jogosultságokat ami a
  munkájához szükséges

https://oauth.net/id-tokens-vs-access-tokens/

# ID token

FE által használt token, tovább nem küldi, ezzel kér az Auth0-tól Access Token-t.

# Access Token struktúra

```json 
{
  "token_valid": true,
  "token_data": {
    "iss": "https://dev-ulmlyx6h.eu.auth0.com/",
    "sub": "google-oauth2|10114942668193141514199",
    "aud": [
      "https://joladnijo.jmsz.hu/api/",
      "https://dev-ulmlyx6h.eu.auth0.com/userinfo"
    ],
    "iat": 1648055759,
    "exp": 1648142159,
    "azp": "QnHVeivYr9bzbsRzbADhrYQb4SoKE9Md",
    "scope": "openid profile email",
    "permissions": [
      "aidcenter:c:s",
      "aidcenter:d:s",
      "aidcenter:r:a",
      "aidcenter:u:s",
      "asset-request:c:s",
      "asset-request:d:s",
      "asset-request:r:a",
      "asset-request:u:s",
      "org:r:a",
      "org:u:s"
    ]
  },
  "decoded": null
}
```

Itt a `permissions` blokk fogja tartalmazni a felhasználó jogosultságait.

## Hogyan tudom meg egy jogosultság mire való?

Elolvasod a specifikáció [jogosultságok](./../specifikacio/jogosultsagok.md) részét majd megnézed
a technikai dokumentáció [jogosultságok](jogosultsagok.md) dokumentációt, ahol ez le van bontva.

## Hogyan validálom az Access Tokent?

OAuth2 OIDC protokoll definiál egy Discovery Document nevű JSON struktúrát, ahol megmondja, hogy mit hol találsz.

Ez fejlesztői domain esetében itt található: https://dev-ulmlyx6h.eu.auth0.com/.well-known/openid-configuration.

Itt lesz a token digitális aláírását hitelesítő publikus kulcs is:
https://dev-ulmlyx6h.eu.auth0.com/.well-known/jwks.json

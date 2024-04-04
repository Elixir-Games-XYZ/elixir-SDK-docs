---
description: API protocol description and utilities for Desktop integration
---

# 🖥️ Desktop Auth

## Launcher AUTH

Each game will receive a `rei key` when launched under the `-rei` field. This `rei key` will be required to get the user session `JWT` on a separate request. The player session will be kept alive by the Game Developer using the `Get Refresh Token` request.  `JWT` will be required  `Bearer Token` on every request.

The following methods will be used only for `Elixir Launcher Games` to keep a user session.

## Development Only

As described above, some will notice a dependency on Elixir Launcher to test the complete integration. But for local development, we facilitate the following endpoint, restricted only for **Development** Keys. That allows game developers to generate verifiable **reikeys** for development purposes.

### Use your account

Note that the **reikey** generated with this endpoint will grant access to the **Game Owner account**. So any modification applied to this account (new username, new wallet, friends...) will be accessible in development mode. This accelerates integration and removes dependencies.

### Support extra accounts

You can also log in with different accounts. To do so, you'll need to ask the **Support Team** to whitelist any of your developers and provide you with their `playerId` . Two use cases can be extrapolated from this utility:

* For those games that need to log in several users to **test multiplayer features** or have an anti-cheat system that uses OpenID.
* For bugs and tickets from your community. You'll be able to **log in with bugged accounts** to fix the issue.



## Generate Reikey

<mark style="color:blue;">`GET`</mark> `https://kend.elixir.app/sdk/auth/v2/dev/reikey`

Please be aware that this endpoint is only accessible with a **DEVELOPMENT KEY**. The purpose of this endpoint is to ease an agile usage of the API, providing an endpoint that allows generating valid reikeys.

#### Query Parameters

| Name     | Type   | Description                      |
| -------- | ------ | -------------------------------- |
| playerId | String | Player ID of an alternative user |

#### Headers

| Name                                        | Type   | Description                                     |
| ------------------------------------------- | ------ | ----------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark> | String | Public Key available on the Developer Dashboard |

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "reikey": "508b12d4-1e98-4534-bfc0-6554178ebb8e",
        "playerId": "aea...5d36"
    }
}
```
{% endtab %}

{% tab title="400 A reikey must be generated in a space of 10 seconds if the reikey has not been activated ( get user credential). If the reikey is activated, must wait 5 minutes to generate a new one." %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1001,
        "message": "Invalid API Key"
    }
}
```
{% endtab %}
{% endtabs %}

## Auth Endpoints



## &#x20;Get User Credentials

<mark style="color:blue;">`GET`</mark> `https://kend.elixir.app/sdk/auth/v2/session/reikey/:reikey`

The `reikey` param will be sent by the launcher when the game is executed as a `-rei` field.\
With this endpoint, the reikey will be activated, and the user credentials will be provided. With them, the game will be able to maintain in the background the user session alive, in order to avoid bugs and impersonation.

#### Path Parameters

| Name                                     | Type   | Description                               |
| ---------------------------------------- | ------ | ----------------------------------------- |
| reikey<mark style="color:red;">\*</mark> | string | Rei key received when the game is started |

#### Headers

| Name                                        | Type   | Description                                     |
| ------------------------------------------- | ------ | ----------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark> | string | Public Key available on the Developer Dashboard |

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "token": "eyJhbGciOiJIU...",
        "tokenExpiry": 1703311143769,
        "tokenLifeMS": 31557600000,
        "refreshToken": "be3...388",
        "user": {
            "_id": "aea...d36",
            "status": "ACTIVE",
            "banReason": ""
        }
    }
}
```
{% endtab %}

{% tab title="400: Bad Request " %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1000,
        "message": "Not an activable reikey"
    }
}
```
{% endtab %}
{% endtabs %}

## Refresh User token

<mark style="color:green;">`POST`</mark> `https://kend.elixir.app/sdk/auth/v2/session/refresh`

Each JWT will have an expiration time, to extend the session it will be required to ask for a new token. To do so, it will be needed the `refresh token` and the last active `jwt`. For example, if the game makes 3 times a request to this service, the `jwt` to provide for the third call will be the `jwt` and `refreshToken` received in the second one. If the `refreshToken` is lost, it will be necessary to generate a new reikey.\
As time expiry may change several times, we recommend requesting a `refreshToken` few seconds after the `tokenExpiry` timestamp is reached.

#### Headers

| Name                                        | Type   | Description                                     |
| ------------------------------------------- | ------ | ----------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark> | string | Public Key available on the Developer Dashboard |

#### Request Body

| Name                                           | Type   | Description                    |
| ---------------------------------------------- | ------ | ------------------------------ |
| refreshToken<mark style="color:red;">\*</mark> | String | Latest refresh token alive     |
| reikey                                         | Stirng | Reikey used to launch the game |

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "token": "ey...",
        "tokenExpiry": 1703311143769,
        "tokenLifeMS": 31557600000,
        "refreshToken": "be...8",
        "user": {
            "_id": "aea...36",
            "status": "ACTIVE",
            "banReason": ""
        }
    }
}
```
{% endtab %}

{% tab title="400: Bad Request " %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1000,
        "message": "Not an activable reikey"
    }
}
```
{% endtab %}
{% endtabs %}

## Close Session

<mark style="color:green;">`POST`</mark> `https://kend.elixir.app/sdk/auth/v2/session/closerei/:reikey`

This endpoint should be executed when the user closes the game: It will terminate the session credentials (jwt and reikey). The usage of this endpoint is similar to a refresh token endpoint, but jsut requires a valid JWT as an authorization header.

#### Path Parameters

| Name                                     | Type   | Description                    |
| ---------------------------------------- | ------ | ------------------------------ |
| reikey<mark style="color:red;">\*</mark> | String | Reikey used to launch the game |

#### Headers

| Name                                            | Type   | Description                                     |
| ----------------------------------------------- | ------ | ----------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark>     | string | Public Key available on the Developer Dashboard |
| Authorization<mark style="color:red;">\*</mark> | string | "Bearer + JWT"                                  |

{% tabs %}
{% tab title="200 " %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "closed": true
    }
}
```
{% endtab %}

{% tab title="400: Bad Request " %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1001,
        "message": "Invalid API Key"
    }
}
```
{% endtab %}
{% endtabs %}


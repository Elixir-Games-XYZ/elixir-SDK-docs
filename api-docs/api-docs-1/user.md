---
description: Obtaining Elixir User information
---

# 🧔 User

## Overview

The user info provides information about the user's public profile in Elixir. This endpoint can validate the Elixir JWT as an OpenID system. Besides, the game can get the wallets of the user in case they are needed.\


{% swagger method="get" path="/sdk/v2/userinfo" baseUrl="https://kend.elixir.app" summary="Userinfo/Open ID" %}
{% swagger-description %}
Method to provide all Elixir User-related info. Works as an OpenId to validate the user JWT.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key available on the Developer Dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="String" required="true" %}
A string containing the JWT as follows: "Bearer \<jwt>"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success Response" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "sub": "aea...36",
        "wallets": [
            "BINANCE:0xB...8",
            "SOLANA:Eb...1w"
        ],
        "nickname": "rega",
        "picture": "https://...",
        "status": "ACTIVE",
        "email": "user@email.com",
        "email_verified": true,
        "aud": "game:production",
        "iss": "gameId",
        "iat": 1675127300,
        "exp": 1675386500
    }
}

```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1001,
        "message": "The argument 'encoding' is invalid for data of length 1151. Received 'hex'"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/sdk/v2/friends/" baseUrl="https://kend.elixir.app" summary="User Friend List" %}
{% swagger-description %}
Get the Friend List for a given user. Friend information is provided so it can be displayed with avatars. Each friend `ElixirId` is available on the `friendId` field
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
Public Key available on the Developer Dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="String" required="true" %}
A string containing the JWT as follows: "Bearer \<jwt>"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}


```json
{
    "code": 1,
    "success": true,
    "data": [
        {
            "friendId": "9ce7916c-de8e-44c8-b4aa-455385c601a6",
            "username": "sniper-4015",
            "name": "Sniper",
            "avatar": "https://d1udajbuf50cfc.cloudfront.net/avatar/9ce7916c-de8e-44c8-b4aa-455385c601a6/1675145810918_screenshot_2023_01_18_at_14_52_08_png",
            "isVerifiedNFTAvatar": false,
            "friendStatus": "ACCEPTED",
            "status": "OFFLINE",
            "playStatus": {
                "playing": false
            }
        },
        {
            "friendId": "a2a1f018-c836-4041-bd2d-95a7c4734d36",
            "username": "gunner-8634",
            "name": "Gunner",
            "avatar": "https://d1udajbuf50cfc.cloudfront.net/avatar/aea1f008-c8a6-4041-bd2d-95a7c4735d36/greenie.gif",
            "isVerifiedNFTAvatar": true,
            "friendStatus": "ACCEPTED",
            "status": "OFFLINE",
            "playStatus": {
                "playing": false
            }
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

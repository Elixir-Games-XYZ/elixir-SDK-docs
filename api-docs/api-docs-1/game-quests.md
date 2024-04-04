---
description: >-
  Discover the API to support Quests inside your Game and take the best out of
  the Season Pass!
---

# ❓ Game Quests

The Quest System API serves as the backbone for enabling games to seamlessly integrate and participate in the platform's Quest system. This API provides a standardized interface for game developers to report user progress.

This endpoint is protected with an RSA signature system, adding an extra layer of security to prevent unauthorized users from submitting progress reports without verification.

* The endpoint requires all requests to be signed with RSA signatures generated using private keys known only to authorized game developers.
* Upon receiving a progress report request, the API server verifies the authenticity and integrity of the request by validating the RSA signature against the corresponding public key associated with the game developer.

{% content-ref url="rsa-signature/" %}
[rsa-signature](rsa-signature/)
{% endcontent-ref %}

This robust security measure mitigates the risk of unauthorized data manipulation and maintains the reliability of the Quest System API, fostering trust and confidence among game developers and platform users alike.

## Submit Game Stat

<mark style="color:green;">`POST`</mark> `https://kend.elixir.app/sdk/v2/game-stats`

Submit game stat to progress an Elixir Quests. This endpoint is protected using the Elixir RSA Signature.

#### Headers

| Name                                              | Type   | Description                                     |
| ------------------------------------------------- | ------ | ----------------------------------------------- |
| x-api-key<mark style="color:red;">\*</mark>       | String | Public Key available on the Developer Dashboard |
| x-api-signature<mark style="color:red;">\*</mark> | String | Generated RSA signature                         |
| x-api-token<mark style="color:red;">\*</mark>     | String | Timestamp used in the API Signature             |
| Content-Type<mark style="color:red;">\*</mark>    | String | 'application/json'                              |

#### Request Body

| Name                                        | Type   | Description |
| ------------------------------------------- | ------ | ----------- |
| stat<mark style="color:red;">\*</mark>      | String |             |
| increment<mark style="color:red;">\*</mark> | Number |             |
| userId                                      | String | Elixir ID   |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
"code": 1, 
"success": true, 
"data": {}
}
```
{% endtab %}
{% endtabs %}

###

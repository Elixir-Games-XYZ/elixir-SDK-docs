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

{% swagger method="post" path="/sdk/v2/game-stats" baseUrl="https://kend.elixir.app" summary="Submit Game Stat" %}
{% swagger-description %}
Submit game stat to progress an Elixir Quests. This endpoint is protected using the Elixir RSA Signature.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="String" required="true" %}
'application/json'
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-token" required="true" type="String" %}
Timestamp used in the API Signature
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userId" type="String" %}
Elixir ID
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="x-api-signature" type="String" %}
Generated RSA signature
{% endswagger-parameter %}

{% swagger-parameter in="body" name="increment" type="Number" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key available on the Developer Dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="stat" type="String" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
"code": 1, 
"success": true, 
"data": {}
}
```
{% endswagger-response %}
{% endswagger %}

###

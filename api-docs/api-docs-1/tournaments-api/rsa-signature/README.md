# 🔐 RSA Signature

## Overview

The [RSA signature](https://app.gitbook.com/s/XQoAdG0jQCAL0PFMB1Yu/game/skins) process is based on a pair of keys, mathematically linked, consisting of a private key and a public key.

The emitter uses the private key to generate a signature for the message. Then sends the message, the signature and his public key. With this information, the receiver can validate that the message was signed by the emitter identified by his public key and that the content in the message hasn't been modified.

In our implementation of the RSA signature, we follow a tweaked version, where the emitter needs to generate a signature for the body that he wants to send along with a timestamp, separated between a "." this timestamp makes the signature valid just for a limited period.

```bash
Data that I want to send = "Hello! Im George" 
Timestamp = 1672188588

Message = "Hello! Im George".1672188588

→ Sign Message ""Hello! Im George".1672188588" using my private key → Signature 

Send Signature, Message and Timestamp
```

## Extra Tools

### Verify Signature

To test the signature implementation, we facilitate this endpoint that you can call via code, or via Postman with the signature that you generated to see if its well implemented before introducing it in the application.

{% swagger method="post" path="/sdk/v2/signature/verify" baseUrl="https://kend.elixir.app" summary="Verify Signature" %}
{% swagger-description %}
Validates the generated signature so the signing process can be tested.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-signature" required="true" type="String" %}
Generated RSA signature
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-token" required="true" type="String" %}
Timestamp used in the API Signature
{% endswagger-parameter %}

{% swagger-parameter in="body" name="{}" type="Object" required="true" %}
An object containing the message that wants to be signed
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "code": 1, 
  "success": true, 
  "data": <Req.Body> // Data will include body sent in the request
}
```
{% endswagger-response %}
{% endswagger %}

## Example implementations

{% content-ref url="node.js-example.md" %}
[node.js-example.md](node.js-example.md)
{% endcontent-ref %}

{% content-ref url="c-example.md" %}
[c-example.md](c-example.md)
{% endcontent-ref %}


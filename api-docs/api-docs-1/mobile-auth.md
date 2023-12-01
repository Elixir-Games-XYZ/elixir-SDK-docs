---
description: Authentification request in order to get user credentials
---

# 📱 Mobile Auth

### OTP Login

The OTP login is based on a single login without a password. This kind of login is based on two steps:

1. A request to provide the sign-in code to the user via email
2. A second endpoint to verify the code.

### Refresh Token

The login endpoint will provide several fields for the user session. The most important one is the `accessToken` as `JWT` that will represent the user identity on each request.\
\
This `accessToken` has an expiration time to protect the user's identity when he is out of the platform. If the user interacts with the platform, the session needs to be refreshed to get a new `accessToken`\
\
The API uses a `refreshToken` to prevent users from entering the OTP Login several times: The client needs to save the `refreshToken` obtained from the Login and use it to refresh the user access token (`JWT)` \
\
This way, the client can save the last valid `refreshToken` for the future and obtain the user credentials. Avoiding the login step.

{% swagger method="post" path="/sdk/auth/v2/signin/otp-login" baseUrl="https://kend.elixir.app" summary="OTP Login Request" %}
{% swagger-description %}
In this request, the user must submit his email address, the server will then validate the address and, if every check is passed, send an email with the code to it.\
\
The client must save the transaction id in order to verify the code in the next step.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" type="String" %}
User email provided in the input
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Production" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "transactionId": "0306d0b1-bb5c-4a9b-aa55-8b56fe659168"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Failed response" %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/sdk/auth/v2/signin/otp-verify" baseUrl="https://kend.elixir.app" summary="OTP Login Verify" %}
{% swagger-description %}
This endpoint completes the process of the OTP Login.\
\
&#x20;Here the user must provide the code so the API can validate it for the current transaction id.&#x20;
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="transactionId" required="true" type="String" %}
OTP Login transaction id from the request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="code" required="true" type="String" %}
Code from user input
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Login credentials" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "token": "eyJhbGciOiJIU...",
        "tokenExpiry": 1678126661453,
        "tokenLifeMS": 30000000000,
        "refreshToken": "210...5bc",
        "user": {
            "_id": "6d3...5d",
            "status": "ACTIVE",
            "banReason": null
        },
        "newAccount": false // True if its a register
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Failed response" %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1001,
        "message": "Invalid API Key"
    }
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/sdk/auth/v2/session/refresh" baseUrl="https://kend.elixir.app" summary="Refresh Session" %}
{% swagger-description %}
The client will use the refreshToken obtained at the login verification and will use it on this request to extend the user access token.\
\
When the client does not have a valid access token, this request will provide the corresponding credentials for the given refreshToken.
{% endswagger-description %}

{% swagger-parameter in="body" name="refreshToken" type="String" required="true" %}
Refresh token
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successful response" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "token": "eyJhbGciOiJIUzUxMi...",
        "tokenExpiry": 1678138840184,
        "tokenLifeMS": 30000000000,
        "refreshToken": "31e...c95",
        "user": {
            "_id": "aea...36",
            "status": "ACTIVE",
            "banReason": ""
        }
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
        "code": "INVALID_REFRESH_TOKEN"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/sdk/auth/v2/session/signout" baseUrl="https://kend.elixir.app" summary="Sign Out" %}
{% swagger-description %}
This endpoint allows the user to remove the current session from the client.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="String" required="true" %}
"Bearer \<JWT>"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Success message" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
        "message": "Session closed successfully for this device"
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
        "code": 1000,
        "message": "Invalid Credentials!"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/sdk/auth/v2/signin/qr-verify" baseUrl="https://kend.elixir.app" summary="QR Verify" %}
{% swagger-description %}
Obtain the user credentials by scanning QR code available on Elixir > My Account > Security
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="qrValue" type="String" required="true" %}
Value obtained from scanning the QR code
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript

{
    "code": 1,
    "success": true,
    "data": {
        "token": "eyJhbGciOiJIU...",
        "tokenExpiry": 1703309445119,
        "tokenLifeMS": 31557600000,
        "refreshToken": "5fb...38e"
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
        "code": 1000,
        "message": "Invalid Credentials!"
    }
}
```
{% endswagger-response %}
{% endswagger %}

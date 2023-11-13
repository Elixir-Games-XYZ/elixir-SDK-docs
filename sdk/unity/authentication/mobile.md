# Mobile

The SDK offers two authentication methods for Elixir users on mobile platforms:

### OTP Login

Users enter their email to receive a verification code. Once validated, they are logged into the SDK.

### QR Scan

For seamless user experience, a QR code in the Elixir Launcher can be scanned using a phone camera for authentication.

{% hint style="info" %}
In Elixir SDK's mobile oAuth implementation users stay logged in with Elixir until they choose to log out, eliminating the need for repeated logins with each game session.
{% endhint %}

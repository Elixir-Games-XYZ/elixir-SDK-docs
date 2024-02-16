# Link Elixir account to a game API account

If you already have an account management API for your game and you would like to link the Elixir Launcher account to the game account and use the game account as main, you can do this simply via a Token Exchange flow.

### What is Token Exchange?

Token exchange is an extension to the OAuth 2.0 protocol that allows one token to be obtained by providing another valid token.

You can read more about it here:&#x20;

{% embed url="https://oauth.net/2/token-exchange/" %}

### The process at a glance&#x20;

Simply put, Elixir Launcher will provide the game with a JWT token for the associated account and the game will send it to the game's account service and receive a game main account JWT token in return.

{% hint style="info" %}
The JWT token provided by Elixir Launcher often includes an email which can be used to automatically link both accounts without further interaction from the user. Only in the event of the email not matching the one used in the game API would you need to require additional authentication with the game account service to know which account to link to.
{% endhint %}

### How do I implement it?

Below is a sequence diagram of the process of linking an Elixir account to a main game API account.

<figure><img src="../../.gitbook/assets/Untitled (1).png" alt=""><figcaption></figcaption></figure>

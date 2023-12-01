# Set up your Store

## Create a Game Store

1. At the Developer dashboard, navigate to the Store
2. Click in the (+) button to add a new store
3. Select the Game you want to start selling products

<figure><img src="../../../.gitbook/assets/Screenshot 2023-12-01 at 00.32.15.png" alt=""><figcaption></figcaption></figure>

4. Add the Game Backend URL, then click Submit

{% hint style="info" %}
_The Server URL represents the game backend endpoint where the post-payment webhook from Elixir Store will be sent._
{% endhint %}

<figure><img src="../../../.gitbook/assets/Add IAP to a new game.png" alt="" width="290"><figcaption></figcaption></figure>

{% hint style="warning" %}
After creating a store for a game, a unique pair of[ API keys](handle-post-payments.md) will be generated in the background, that can be accessed in the [Game API keys ](../../management/api-keys.md)section. There you can edit the server webhook endpoint and access your public key.
{% endhint %}


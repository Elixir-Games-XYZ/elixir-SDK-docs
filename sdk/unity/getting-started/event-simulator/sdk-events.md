# SDK Events

The currently available events are:

#### MTOpenStateChange

Signals to the game that the overlay was either opened or closed. This is useful if you want to pause the game while the overlay is open.&#x20;

#### MTCheckoutResult

{% hint style="danger" %}
Please note there can only be one checkout event happening at the time: Calling a new event will cancel the previous one. So the game should keep track of the latest SKU (product) involved in the checkout.
{% endhint %}

Notifies the game when a checkout has either been completed successfully or failed. This would normally be sent by the overlay after the game has initiated a [Checkout()](sdk-events.md#checkout) request.


# SDK Events

The currently available events are:

#### OnOpenStateChange

Signals to the game that the overlay was either opened or closed. This is useful if you want to pause the game while the overlay is open.&#x20;

#### OnCheckoutResult

{% hint style="danger" %}
Please note there can only be one checkout event happening at the time: Calling a new event will cancel the previous one. So the game should keep track of the latest SKU (product) involved in the checkout.
{% endhint %}

Notifies the game when a checkout has either been completed successfully or failed. This would normally be sent by the overlay after the game has initiated a [Checkout()](sdk-events.md#checkout) request.

#### OnGetWalletResult

Notifies the game of a result to the [`GetWallet`](../overlay-actions.md#getwallet) action. This event delegate has the following signature:

```csharp
public delegate void OnGetWalletResultDelegate(
    string status, string ethAddress, string solAddress, string eosAddress
);
```

The following status values can be returned:

<table><thead><tr><th width="313">Status</th><th>Description</th></tr></thead><tbody><tr><td>SUCCESS</td><td>Successful execution</td></tr><tr><td>USER_REQUEST_DENIED</td><td>SDK has been initialized with an invalid user email.</td></tr><tr><td>SOMETHING_WENT_WRONG</td><td>An system error occurred. Please get in touch with us if you continue seeing this error.</td></tr></tbody></table>

#### OnSignTypedDataResult

Notifies the game of a result to the [`SignTypedData`](../overlay-actions.md#signtypeddata) action. This event's delegate has the following signature:

```csharp
public delegate void OnSignTypedDataResultDelegate(
    string status, string signature, string r, string s, string v
);
```

The following status values can be returned:

<table><thead><tr><th width="313">Status</th><th>Description</th></tr></thead><tbody><tr><td>SUCCESS</td><td>Successful execution</td></tr><tr><td>USER_REQUEST_DENIED</td><td>SDK has been initialized with an invalid user email.</td></tr><tr><td>SOMETHING_WENT_WRONG</td><td>An system error occurred. Please get in touch with us if you continue seeing this error.</td></tr></tbody></table>

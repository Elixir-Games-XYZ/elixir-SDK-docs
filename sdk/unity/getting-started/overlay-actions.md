# Overlay Actions

Once initialized, the following functionality is available:

#### Checkout

You can trigger checkout of an NFT payable with credit card or a crypto wallet by calling `Overlay.Event.Checkout`:&#x20;

```csharp
Overlay.Event.Checkout("MY_ITEM_SKU")
```

Once initialized, the result of the checkout will be returned as an incoming message via the `OnChekoutResult` delegate.

{% hint style="warning" %}
Only one checkout process can be started at a given time. Calling `Checkout` a second time before getting the result will interrupt a previous checkout process.
{% endhint %}

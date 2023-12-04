# Overlay Actions

Once initialized, the following functionality is available:

#### Checkout

You can trigger checkout of an NFT payable with credit card or a crypto wallet by calling `OverlayMessage.Checkout`:&#x20;

```csharp
OverlayMessage.Checkout("MY_ITEM_SKU")
```

Once initialized, the result of the checkout will be returned as an incoming message of type `OverlayMessage.MCheckoutResult`.

{% hint style="warning" %}
Only one checkout process can be started at a given time. Calling `Checkout` a second time before getting the result will interrupt a previous checkout process.
{% endhint %}

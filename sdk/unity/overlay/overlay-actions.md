# Overlay Actions

Once initialized, the following functionality is available:

### In-Game Purchasing

#### Checkout

Trigger checkout of an NFT payable with credit card or a crypto wallet by calling `Overlay.Event.Checkout`:&#x20;

```csharp
Overlay.Event.Checkout("MY_ITEM_SKU")
```

Once initialized, the result of the checkout will be returned as an incoming message via the [`OnChekoutResult` ](event-simulator/sdk-events.md#oncheckoutresult)delegate.

{% hint style="warning" %}
Only one checkout process can be started at a given time. Calling `Checkout` a second time before getting the result will interrupt a previous checkout process.
{% endhint %}

### Invisible Wallet

#### GetWallet

The `getWallet` function in the SDK returns the `public wallet` of the user. The user might be asked to **go through a verification process** before the wallet is returned.

The result of the operation will be returned as an incoming event via the [`OnGetWalletResult`](event-simulator/sdk-events.md#ongetwalletresult) delegate.

#### SignTypedData

Once you have built an ethereum typed data, you can ask the user to sign it by using `signTypedData` function in MetaKeep SDK. The function expects a non-empty `reason` which is shown to the user at the time of typed data signing. This API is compliant with the latest EIP-712 spec and is a drop in replacement for Metamask's signTypedData\_v4 API.&#x20;

The first parameter (`message`) should be a _stringified JSON_ of the EIP-712 compliant payload.&#x20;

```csharp
Overlay.Event.SignTypedData("{ ... }", "Do Some Action")
```

Once initialized, the result of the checkout will be returned as an incoming event via the [`OnSignTypedDataResult`](event-simulator/sdk-events.md#onsigntypeddataresult) delegate.

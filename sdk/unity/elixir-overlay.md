---
description: Integrating Elixir Overlay with your Unity game
---

# Elixir Overlay

### Overview

<img src="../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

The Elixir Overlay is a feature that allows developers to integrate features like NFT purchasing and friends chat seamlessly into their game.

While the overlay is provided by Elixir Launcher in-game automatically without any additional setup requirements, to integrate all the features of the overlay in-game, some setup is required.

### Initialization & Disposal

Communication with the overlay is provided by the `Elixir.OverlayMessage` namespace. The overlay messaging functionality requires both initialization and teardown, and therefore you must make sure that your script implements the `IDisposable` interface.

Here is a minimal example:

{% code overflow="wrap" fullWidth="false" %}
```csharp
public class TestOverlayController : MonoBehaviour, IDisposable
{
	// ... we will assume that a method Log is implemented that prints
	// text on-screen.

	// To initialize, call the Init function, giving it a 
	// callback function that processes incoming messages
	public void Init()
	{
		OverlayMessage.Init(ProcessMessage);
	}
	
	// It is crucial to implement the Dispose method in which 
	// we stop listening to incoming messages from the overlay
	public void Dispose()
	{
		OverlayMessage.StopListening();
	}
	
	// This is our callback that processes incoming messages
	private void ProcessMessage(IMessage message)
	{
		switch (message)
		{
			// the overlay has opened or closed
			case OverlayMessage.MOpenStateChange openStateChange:
				Log($"MOpenStateChange: {openStateChange.IsOpen}");
				break;
			// checkout was completed
			case OverlayMessage.MCheckoutResult checkoutResult:
				Log($"MCheckoutResult: {checkoutResult.Success}");
				break;
			case default:
			case null:
				break;
		}
	}
}
```
{% endcode %}

### Overlay Actions

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

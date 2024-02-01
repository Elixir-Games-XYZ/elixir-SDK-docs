# Overview

{% embed url="https://youtu.be/i1cBJNe8Gn0" %}
Elixir Overlay - Getting Started
{% endembed %}

### Overview

<img src="../../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

The Elixir Overlay is a feature that allows developers to integrate features like NFT purchasing and friends chat seamlessly into their game.

While the overlay is provided by Elixir Launcher in-game automatically without any additional setup requirements, to integrate all the features of the overlay in-game, some setup is required.

### Initialization & Disposal

The overlay event buffer will be automatically initialized by the SDK upon a call to `PrepareElixir(apiKey)`.

The event buffer will remain initialized until application shutdown.

### Integration

Here is a minimal example:

<pre class="language-csharp" data-overflow="wrap" data-full-width="false"><code class="lang-csharp"><strong>using Elixir;
</strong>using Event = Elixir.Overlay.Event;
<strong>
</strong><strong>public class TestOverlayController : MonoBehaviour
</strong>{
	// ... we will assume that a method Log is implemented that prints
	// text on-screen.

	// To initialize simply initialize the SDK by calling PrepareElixir
	public void Init()
	{
		ElixirController.Instance.PrepareElixir("your api public key here");
		
		// after the SDK is initialized, you can assign to the delegates
		Event.OnCheckoutResult += HandleCheckoutResult;
		Event.OnOpenStateChange += HandleOpenStateChange;
	}
	
	private void HandleOpenStateChange(bool isOpen)
	{
		Log($"MOpenStateChange: {isOpen}");
	}

	private void HandleCheckoutResult(bool success, string sku)
	{
		Log($"MCheckoutResult: {success}");
	}

}
</code></pre>

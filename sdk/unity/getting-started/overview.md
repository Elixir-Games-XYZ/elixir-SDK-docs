# Overview

{% embed url="https://youtu.be/i1cBJNe8Gn0" %}
Elixir Overlay - Getting Started
{% endembed %}

### Overview

<img src="../../../.gitbook/assets/file.excalidraw.svg" alt="" class="gitbook-drawing">

The Elixir Overlay is a feature that allows developers to integrate features like NFT purchasing and friends chat seamlessly into their game.

While the overlay is provided by Elixir Launcher in-game automatically without any additional setup requirements, to integrate all the features of the overlay in-game, some setup is required.

### Initialization & Disposal

Communication with the overlay is provided by the `Elixir.OverlayMessage` namespace. The overlay messaging functionality requires both initialization and teardown, and therefore you must make sure that your script calls `Init()` and then `StopListening()` at the beginning and end of the game process respectively.

{% hint style="danger" %}
**IMPORTANT:** It is crucial to ensure that only one message processing callback is active at a given time. This is why for actual game implementation it is recommended to make the controller interacting with the overlay a singleton.
{% endhint %}

Here is a minimal example:

<pre class="language-csharp" data-overflow="wrap" data-full-width="false"><code class="lang-csharp"><strong>using Elixir.Overlay;
</strong><strong>
</strong><strong>public class TestOverlayController : MonoBehaviour
</strong>{
	// ... we will assume that a method Log is implemented that prints
	// text on-screen.

	// To initialize, call the Init function, giving it a 
	// callback function that processes incoming messages
	// this should be done as early as possible, only once
	public void Init()
	{
		OverlayMessage.Init(ProcessMessage);
	}
	
	// It is crucial to call the StopListening method in which 
	// we stop listening to incoming messages from the overlay
	// this should be done when we quit the game
	public void OnApplicationQuit()
	{
		OverlayMessage.StopListening();
	}
	
	// The Update() method should be called by the controller to 
	// ensure that events get processed on the main thread
	public void Update()
	{
		OverlayMessage.Update();
	}
	
	// This is our callback that processes incoming messages
	private void ProcessMessage(IMessage message)
	{
		switch (message)
		{
			// the overlay has opened or closed
			case MOpenStateChange openStateChange:
				Log($"MOpenStateChange: {openStateChange.IsOpen}");
				break;
			// checkout was completed
			case MCheckoutResult checkoutResult:
				Log($"MCheckoutResult: {checkoutResult.Success}");
				break;
		}
	}
}
</code></pre>

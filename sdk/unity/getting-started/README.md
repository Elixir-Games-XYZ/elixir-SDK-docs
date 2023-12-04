# Getting Started

{% hint style="info" %}
If you're new to the Elixir SDK, check out the detailed [Integration Example](https://github.com/Elixir-Games-XYZ/elixir-unity-sdk/blob/master/Demo/Scripts/InitSceneController.cs)
{% endhint %}

### 1. Download and install <a href="#user-content-1-download-and-install" id="user-content-1-download-and-install"></a>

* Download the latest version of the SDK available [here](https://github.com/Elixir-Games-XYZ/elixir-unity-sdk/releases).
* Import the package inside your workspace: _Assets_ > _Import Package_ > _Custom Package_

### 2. Obtain your public key

{% hint style="info" %}
[Click here to read more about Elixir API keys](../../../dashboard/management/api-keys.md)
{% endhint %}

Your public key can be obtained in the [Developer Dashboard](https://dashboard.elixir.app/).

The public key is used to initialize the Elixir SDK. Try it by replacing the following line in the integration example:

```
Elixir.ElixirController.Instance.PrepareElixir("put you public key here")
```

### 3. Use Elixir SDK in your game

You can see a working reference by running our integration example. After inputting the public key you should be able to run the initial scene and check that you obtained your Elixir publisher user.

* Understand [how the Overlay works](overview.md) inside your game
* Discover all the available [actions](overlay-actions.md) you can do with it
* Use our [Event Simulator](event-simulator/) to develop locally for a smooth integration

\

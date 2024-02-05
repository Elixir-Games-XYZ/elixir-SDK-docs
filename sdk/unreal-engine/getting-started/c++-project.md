---
description: >-
  This guide assumes you are implementing the Elixir SDK in a C++ project and
  have already cloned the Elixir SDK plugin into your "Plugins" folder.
---

# C++ Project

### Step 1: Prepare Elixir

The first step to integrating Elixir is to assign your SDK public key by running:

```cpp
UElixirSubsystem::GetInstance()->PrepareElixir(ElixirApiKey);
```

It is highly recommended to manage API keys through some sort of persisted settings system, such as the built in Unreal Engine `UDeveloperSettings` class, as you will find yourself having to frequently switch between development API keys for testing and production API keys for building a release.

{% embed url="https://www.tomlooman.com/unreal-engine-developer-settings/" %}
Learn more about adding custom settings to Unreal Engine
{% endembed %}

### Step 2: Initialize Elixir

The second step of Elixir integration is calling the `InitElixir` function. The function receives a `UElixirSubsystem::FCallback`.

```cpp
UElixirSubsystem::FCallback CompleteCallback;
CompleteCallback.BindDynamic(this, &UMyClass::OnElixirInitComplete);
UElixirSubsystem::GetInstance()->InitElixir(CompleteCallback);
```

The completion callback can execute any logic that should happen after initializing the SDK:

```cpp
void UMyClass::OnElixirInitComplete(const bool bSuccess)
{
    // this code will run after the SDK has either been successfully initialized
    // or an error has been encountered
}
```

{% hint style="info" %}
It is advisable to initialize the SDK as early as possible in your game workflow
{% endhint %}

The initialization process will take care of the following:

* Log in the user automatically via provided context from Elixir Launcher  (in production) or a freshly generated token (in development).
* Initialize connection to the Elixir Overlay event buffer
* Set up a timer to refresh the authentication token automatically in the background

You are now ready to use the Elixir SDK!

# Desktop

## Overview

The SDK ensures that the game runs within the Elixir Launcher Environment. Upon successful verification, it retrieves user session credentials, enabling login through the Elixir Launcher account.&#x20;

Failure in this verification prevents game execution, blocking access outside the Elixir Launcher and for banned users.&#x20;

{% hint style="warning" %}
The latest SDK version allows owners to bypass this check, permitting execution outside the Elixir Launcher Environment.
{% endhint %}

The Elixir SDK streamlines authentication processes, simplifying the workflow for developers. Leveraging the sandbox environment alongside the development API key, the SDK emulates the launcher authentication system.&#x20;

This integration allows game developers to effortlessly generate production builds, circumventing the need for development login. Instead, the credentials of the user launching the game from the Elixir launcher are seamlessly utilized. For more information have a look at the [Desktop Auth](../../../api-docs/api-docs-1/auth.md) docs.

---
description: >-
  This guide assumes you are implementing the Elixir SDK in a C++ or Blueprint
  project and have already cloned the Elixir SDK plugin into your "Plugins"
  folder.
---

# Blueprints Project

### Prepare & Init Elixir

To integrate the Elixir SDK into your blueprint project you must execute the "Prepare Elixir" node, which will connect your public API key to the SDK and the "Init Elixir" node.

You would normally want to do this in either your game state or your level blueprint, as they get initialized early and only get destroyed once the level is unloaded.

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>An example integration of Elixir SDK in a Level Blueprint</p></figcaption></figure>

The initialization process will take care of the following:

* Log in the user automatically via provided context from Elixir Launcher  (in production) or a freshly generated token (in development).
* Initialize connection to the Elixir Overlay event buffer
* Set up a timer to refresh the authentication token automatically in the background

### On Complete Event

The "Init Elixir" node will provide a delegate for a completion event. You can bind a custom event to that delegate using the "Create Event" node, and execute the logic of your choice upon either a successful or failed initialization.

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption><p>A simple example integration where we print the result of the initialization on screen</p></figcaption></figure>

You are now ready to use the Elixir SDK!

### Using Elixir Functions

You can easily find all the relevant Elixir functionality by looking for the "Get Elixir Subsystem" node.

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Once found, extend a connection from its' pin and type "Elixir" to see a list of all available nodes to interact with the SDK.

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

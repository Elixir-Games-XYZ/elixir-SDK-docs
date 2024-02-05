---
description: Interact with the Elixir API with your game credentials
---

# API Keys

## Overview

Each publisher can generate their Game API Keys, which are unique for each game, to interact with the Elixir API service.

Please be aware that the Elixir Keys are generated in pairs, including a **public key** and a **private key**. The public key will be constantly available at the _Developer Dashboard_, but the Private key will not be stored in Elixir for security reasons, so **please save it once generated,** as we cannot show the private key back again. We don't keep it! :smile:&#x20;

You will be using your **public key** for:

1. Retrieve information from Elixir about the player using your game, to get their username, avatar, wallet addresses or owned NFTs, for example.
2. In general, the public key is considered **safe to be included in your game client.**

The **private key** on the other hand, is needed to:

1. Sign requests that **update** information on Elixir, like posting tournament scores.&#x20;
2. We recommend against including your private key in any form in your distributable game clients, as it should be used primarily from your game backend.

If you lose or want to change for security reasons your keys, you will need to delete an existing key pair and generate a new one. This of course will imply you'll need to upload a new version / build of your game. This allows you to disable a game build, as all requests made using the removed key pair will be rejected by Elixir.



## Environments

Every publisher will be allowed to generate key pairs for two different environments:

#### Development&#x20;

These API Keys allow developers to access the Elixir API in development mode, and are intended to test the integration with Elixir locally. You'll use development API keys to:&#x20;

* Generate user credentials for development.
* Use protected endpoints for development, like hidden tournaments and submitting fake scores before publishing a tournament.

#### Production&#x20;

These API Keys grant access to the Elixir API in production mode. Switching to the Production API Key must be done when building and releasing the final build, since **requests using development keys will be rejected in production**.

{% hint style="warning" %}
Leaking a build with a Development API Key in the production environment will lead to request being rejected by Elixir and errors, leading to a bad user experience.
{% endhint %}

### Generate your keys

Navigate to the API Keys page in the developer dashboard and generate your developer keys.

{% hint style="danger" %}
Make sure to **save your private key** when generating it, as you won't be able to retrieve it again. Do not share your private key with anyone and don't include in any version control system like Git, as it will be exposed in the Git history.
{% endhint %}

<div align="center">

<figure><img src="../../.gitbook/assets/ezgif.com-gif-maker (1).gif" alt=""><figcaption><p>Creating a new API Key, make sure to save your private key on a safe place</p></figcaption></figure>

</div>




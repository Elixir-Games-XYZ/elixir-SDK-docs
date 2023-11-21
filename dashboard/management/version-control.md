---
description: Uploading your Game Build
---

# 💻 Version control

{% embed url="https://youtu.be/skj1ViMkKc0" %}
Update your game
{% endembed %}

### Understanding Branches

#### Master Branch

The Master Branch is used for public release. Once a new version of the game has been approved and a new release is on the way. Users must create a new build on Master and upload there the Game Build in a new Depot.

{% hint style="info" %}
We recommend to upload the Game Build to the TEST branch first in order to check that everything is running correctly before making it public.
{% endhint %}

#### Test Branch

This branch is used for closed beta access using [Beta Codes](beta-codes.md). Publishers can upload every new version of the game to test it internally or with the community before making it public.

This branch is also used for the pre-alpha versions when a game is not released yet.

#### Develop Branch&#x20;

Upload your build for internal testing. Check out the SDK integration and make the last adjustments before releasing the game with your audience.&#x20;

Only whitelisted developer accounts will have access to this build.



### Upgrading Version

Every new **Build** represents a new version of the Game. So every time that a publisher wants to release a new version of the game, it is needed to create a new build, and then activate it. \
\
When users launch Elixir, it will detect a new version is available and will prompt users to download the update before playing.

![When the old build is active, users will be able to keep playing.](<../../.gitbook/assets/Screenshot 2022-08-15 at 19.43.14.png>)

![When a new build is activated. The players are forced to update](<../../.gitbook/assets/Screenshot 2022-08-15 at 19.49.26.png>)

### Your First Build

Builds in Elixir Platform are used for version control. Every new Build represent a new version of the Game. Creating a build is a simple task:

* Choose your own version naming
* Have control of which build you have active to perform new releases and rollbacks

![](<../../.gitbook/assets/Screenshot 2022-08-15 at 19.22.54.png>)

Do not forget to activate the Build once everything is ready. Also, you can always de-activate it when you want to close the access to the game. Or perform a roll-back by activating older builds just by using the toggles:

![](<../../.gitbook/assets/Screenshot 2022-08-15 at 19.24.01.png>)

### Your First Depot

Now that you have created a Game Build. Let upload the file so you can start playing it. For this you will need to configure the Depot: A configuration file that will include information about the Game File and how to execute it.

* **Installation Path**: Do not modify this path. We are planning on removing it from here for the next version.
* **Launch Command**: It should follow a structure like `"<InstallationPath>/<route to the executable file>".` See [Recommendations](version-control.md#recommendations-and-usual-errors)

![](<../../.gitbook/assets/Screenshot 2022-08-15 at 19.26.15.png>)

![](<../../.gitbook/assets/Screenshot 2022-08-15 at 19.34.41.png>)

### Recommendations

We recommend to upload a zip file made out of selecting all the files in the Game Build instead than doing it from a folder as follows:

![](<../../.gitbook/assets/Screenshot 2022-08-15 at 20.03.30.png>)

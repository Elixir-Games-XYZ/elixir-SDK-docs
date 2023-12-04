# 🏆 Tournaments

## :information\_source: Overview

The Tournaments Tool in Elixir intends to provide a utility for games to engage with their community by allowing you to create tournaments, register player scores and retrieve a real time leaderboard.&#x20;

You will be able to retrieve existing or previous tournaments, along with the leaderboards, from within your game, and update your game UI if you chose to do so. No need to create a new build for each new tournament with a hardcoded tournament ID!

Elixir will keep tournament scores for you. In order to save the scores, each game needs to define which information to save for each player. These are the **score types**. For example, one game may want to track the number of "kills" while other one needs to track "goals". Score types allows you to define which numeric values you want to store in Elixir. You can use multiple score types for your game.&#x20;

Score types are defined in the Dashboard, under [Tournament Setting](set-up.md)s, as they defined the proper request / response messages when using the [Tournament API](../../api-docs/api-docs-1/tournaments-api/).

With tournament settings defined for your game, you'll be able to create a private (for testing / integration / QA) or public tournament. [Tournaments are created from Elixir Launcher.](create-tournament.md)

Once you define the available score types, you will use the Tournament API with your private key to send user scores to Elixir for a specific tournament.&#x20;



#### Use Case Example

To better understand this tool, in the following sections we'll be using an imaginary example of a FPS Zombie Survival game hosting a weekend tournament and wanting to reward the top 3 players. For this tournament, the game considers how many zombies each participant killed ("kills") and how many times they died ("deaths"), resulting in a final score that will determine their ranking position ("KD"), calculated via the number of kills/number of deaths.\
\
We will be display all three score types (kills, deaths, and KD rate) in the leaderboard, but only the KD value will be used to sort the leaderboard entries: the player with the highest SUM of KD will be the winner.



{% content-ref url="set-up.md" %}
[set-up.md](set-up.md)
{% endcontent-ref %}

{% content-ref url="create-tournament.md" %}
[create-tournament.md](create-tournament.md)
{% endcontent-ref %}

{% content-ref url="../../api-docs/api-docs-1/tournaments-api/" %}
[tournaments-api](../../api-docs/api-docs-1/tournaments-api/)
{% endcontent-ref %}

### Go to production

* Make a public tournament from Elixir Launcher.
* Use the appropriate **Production API Key** in your game server / backend (private key) and optionally in the client (public key) if you want to display the available tournaments inside your game or even the actual leaderboards.
* Upload the latest build and activate it on Version Control for the tournament.
* Have fun, and record scores from your backend for the leaderboard to be automatically updated in Elixir Launcher. The leaderboard will be visible from the Tournament page and the Game page, while the tournament is live.

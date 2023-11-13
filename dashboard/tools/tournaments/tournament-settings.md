---
description: Create the tournament settings in the Developer Dashboard
---

# 🔧 Tournament Settings

Start setting up the tournament configuration in the **developer dashboard**. You'll be able to find the "**Tournaments**" page in the Tools area.&#x20;

{% hint style="info" %}
These settings are very much coupled to your game logic and will determine the kind of requests your dev team will be sending[ through the API](../../../api-docs/api-docs-1/tournaments-api/).
{% endhint %}

<figure><img src="../../../.gitbook/assets/Screenshot 2023-01-09 at 21.02.42.png" alt=""><figcaption><p>Tournament Settings for the Use Case described</p></figcaption></figure>

#### Visibility

Here you get to choose if you want the tournament preset config to be available **for other content creators** or not. You, as a game publisher, will be able to create private tournaments using these settings. Once you have tested your integration, you can make your tournament settings public so other users may create tournaments.&#x20;

You will understand this better once you have gone through all the steps, but for now, all you need to understand is that it gives you control over the tournament events that can be hosted for your game.

#### Score Types

Define the data you'll want to save and optionally display in the tournament leaderboard. You will only be able to save scores of these specific types.

The **name** defines the API identifier for the score type.&#x20;

The **label** field is the text users will see in the public leaderboard.&#x20;

Use the **display** toggle to show this score in the leaderboard, and the final arrows to determine the display order in the leaderboard header. Fields higher in the list will appear to the left of the leaderboard, while fields down this list will appear to the right of the leaderboard.

#### Leaderboard Settings

Finally, select which score type will define the leaderboard sorting method, its type (Average or High Score, which the sum of all scores for a given user) and its order (**Desc**ending or **Asc**ending).\
\
Following our example, we want the tournament leader to be the user with the highest aggregated KD scores, so we use "Highscore" for type and "Desc" for the sort order. As this is the order-defining score type, we also set it as the last score type using the Order arrows in the score type definition list.



_Hint: You can set more than one Score Type to be displayed in the leaderboard. But the sorting field can only be one of them._

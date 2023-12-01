---
description: Game implementation of the tournaments tool.
---

# 🏆 Tournaments API

After completing the [required steps](../../../dashboard/tournaments/); For the implementation on the game side, we tried to make it in the simple but most secure way. Please, make sure to use the Development API key during the development and testing of your integration to work with a private tournament and avoid having test data in production. This key will only work for private tournaments.

We have defined two core endpoints: **get tournaments** and **submit scores**.

### Client Side: Get Tournaments

The first part of the implementation takes place on the game client/backend side. This first endpoint will provide the active tournaments for your game, given an API Key.

The **most critical** element will be the **`_id`** field, as it will define which tournament you want to submit the player's score to in the second part of the implementation.

{% hint style="warning" %}
Please notice that you'll only be able to access private tournaments and submit scores using a Development API Key.
{% endhint %}

We recommend adding the active tournament with a visible component in the game so that the player can select and play to it (or instead set it as default).

{% swagger method="get" path="/sdk/v2/tournaments/" baseUrl="https://kend.elixir.app" summary="Get Tournaments" %}
{% swagger-description %}
Retrieves all the tournaments for a given API Key.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key available on the Developer Dashboard
{% endswagger-parameter %}

{% swagger-parameter in="query" name="filter" type="ALL or ACTIVE" %}
Filter between ALL events or ACTIVE events. Default: "ACTIVE"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
<pre class="language-javascript"><code class="lang-javascript">{
"code": 1, 
"success": true, 
"data": [{
    "_id": // Unique identifier of the event (ID),
    "name": // Name of the event (STRING),
    "gameId": // ID,
    "description": // text,
    "createdAt": // Date of creation of the tournament (2022-12-13T12:45:17.281Z) "modifiedAt": Date of latest modification(ISO),
    "startsAt": // Starting date of the event(ISO),
    "endsAt": // Ending Date of the event(ISO),
    "repeatEvery": null,
    "location": // URL where the tournament is happening (String), 
    "eventUrl": // URL to redirect to the event (String),
    "userId": // Creator of the event (ID),
    "imageUrl": // URL with the image of the event (String),
    "prizePool": // Amount of USD in the prize pool (Number),
<strong>    "type": // Indicator if it is a "tournament" or just an "event",
</strong>    "visibility": // Indicator if the tournament is visible for the public (public/private), "rules": URL to the rules of the tournament (String),
    "prizeDescription": // Short description of the price (String),
    "settingsId": // Setting selected for the tournament (ID),
    "leaderboard": // Object containing the current leaderboard
} ]
}
</code></pre>
{% endswagger-response %}
{% endswagger %}

### Server Side: Submit Score

This second part of the implementation is the most critical one. Here you'll submit each player score, which will affect its ranking and be displayed in the leaderboard.

Given the critical nature of this functionality, we need to insist on the importance of calling this method from the **Game Server or Backend.**

{% hint style="warning" %}
You won't be able to submit a score to a **public** event with a Development API Key
{% endhint %}

We have chosen to be extra cautious and secure it with an [RSA Signature](rsa-signature/) using your private API key. We use this signature method to be sure that the score is sent from a verified server and reduces vulnerabilities and exploits of malicious agents. This provides reliability to the leaderboards displayed in Elixir.

To implement this accurately, the game developer must **never** **expose** his **private key**. And this should be done server-side, not client-side!

{% hint style="info" %}
You can submit multiple scores for each player. The scores will be grouped by the defined `userId` or `externalUserId` you provide with each score, and the total aggregate result will be displayed in the leaderboard.&#x20;
{% endhint %}

{% swagger method="post" path="/sdk/v2/tournaments/:tournamentId/submit" baseUrl="https://kend.elixir.app" summary="Submit Score" %}
{% swagger-description %}
Saves a user scores for a specific tournament. Either `userId` or `externalUserId` must be provided. `userId` represents the Elixir user Id, and will be linked to the Elixir account of the player to display their preferred username and avatar in the leaderboard, so we encourage you to use the User Info endpoint to retrieve the elixir Id of each player for the best looking tournament page.\
\
The format of the scores must follow the scoreTypes defined on [your tournament settings](../../../dashboard/tournaments/tournament-settings.md):\
\
{ "scoreType": \<scoreType>, "value": Number}
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-token" type="String" required="true" %}
Timestamp used in the API Signature
{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-api-signature" required="true" type="String" %}
Generated RSA signature
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userId" type="String" %}
Elixir User Id.&#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="externalUserId" type="String" required="false" %}
Your unique identifier for that user. (displayed if not linked to Elixir)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="scores" type="Array" required="true" %}
An Array of individual scores, with each element being an object of the shape \
`{ "scoreType": "<name>", "value": <number>}`
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="false" type="String" %}
'application/json'
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "code": 1, 
  "success": true, 
  "data": {
     "_id": "7e410239-5113-4e8c-bad2-fd018fb5cc64", 
     "tournamentId": "ad092f92-ce73-49df-a59f-1b423ad57463", 
     "externalUserId": "sniper-4431",
     "userId": "123",
     "scores": {
         "kills": 6, 
         "deaths": 2, 
         "kd": 3
    },
  "createdAt": "2022-12-15T00:48:32.084Z" 
  }
}
```
{% endswagger-response %}
{% endswagger %}

## Additional Tournament Info

If you want to extract the best out of the Elixir Tournaments feature, including these two endpoints will make you stand out:

#### Tournament Leaderboard

You can access the tournament leaderboard via API to display it inside your game. Apart from the general ranking, you will have access to the player rank. In case you want to display it on your client or if you want to know the winners and assign rewards for a finished tournament.

{% swagger method="get" path="/sdk/v2/tournaments/:tournamentId/leaderboard" baseUrl="https://kend.elixir.app" summary="Get Leaderboard" %}
{% swagger-description %}
Obtain the total ranking for the tournament based on the sorting method you configured in the Dashboard.  If you provide the player JWT, their rank will be included outside of the paginated entries.
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="startDate" type="Date" %}
Starting date that you want to consider for the leaderboard.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="endDate" type="Date" %}
Ending date that you want to consider for the leaderboard. (f.e. "2022-12-31")
{% endswagger-parameter %}

{% swagger-parameter in="body" name="limit" type="Int" %}
The number of entries you want to display. Intended for pagination (Default: 10)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="skip" type="Int" %}
The number of entries you want to skip. Intended for pagination (Default: 0)
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="String" required="false" %}
Bearer JWT
{% endswagger-parameter %}

{% swagger-parameter in="path" name="tournamentId" required="true" type="String" %}
ID of the tournament
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": {
            "entries": [{
                "_id": "rega",
                "rank": 1,
                "avatarUrl": null,
                "scores": [
                    {
                        "scoreType": "kills",
                        "value": 5
                    }
                ]
            },
            {
                "_id": "09142dc7-283d-400a-b073-9a20955cb92d",
                "rank": 2,
                "avatarUrl": null,
                "name": "Groundbreaker",
                "username": "groundbreaker-1433",
                "scores": [
                    {
                        "scoreType": "kills",
                        "value": 10
                    }
                ]
            }
        ],
        "totalEntries": 2,
        "tournamentId": "ee39d5e1-b578-4409-8383-ceef384e7e8d",
        "userRank": {
            "_id": "09142dc7-283d-400a-b073-9a20955cb92d",
            "rank": 2,
            "avatarUrl": null,
            "name": "Groundbreaker",
            "username": "groundbreaker-1433",
            "scores": [
                {
                    "scoreType": "kills",
                    "value": 10
                }
            ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

#### Tournament Scores

As a verifiable source, this endpoint will provide all scores given a tournament and a specific period. This way, game developers can contrast their data against the data in Elixir to avoid malicious activity and fake scores.

{% swagger method="get" path="/sdk/v2/tournaments/:tournamentId/scores" baseUrl="https://kend.elixir.app" summary="Get Scores" %}
{% swagger-description %}
Return the total tournament scores by user
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" required="true" type="String" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="body" name="startDate" type="Date" %}
Starting date that you want to consider for the calculation of the scores
{% endswagger-parameter %}

{% swagger-parameter in="body" name="endDate" type="Date" %}
Ending date that you want to consider for the calculation of the scores. (f.e. "2022-12-31")
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": [
        {
            "_id": "ff60d00d-9c35-4c76-93e4-4848473d8268",
            "tournamentId": "ee39d5e1-b578-4409-8383-ceef384e7e8d",
            "externalUserId": "sniper",
            "userId": null,
            "scores": {
                "kills": 5
            },
            "createdAt": "2023-01-11T14:52:31.394Z"
        },
        {
            "_id": "6ab6833d-6f96-47f9-8fd6-86212b3bfe4a",
            "tournamentId": "ee39d5e1-b578-4409-8383-ceef384e7e8d",
            "externalUserId": "Groundbreaker",
            "userId": "09142dc7-283d-400a-b073-9a20955cb92d",
            "scores": {
                "kills": 10
            },
            "createdAt": "2023-01-11T14:54:02.832Z"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

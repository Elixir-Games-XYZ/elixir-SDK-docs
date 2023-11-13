---
description: Obtain the user nfts and allow to play with them!
---

# 👾 NFTs

## Blockchain Support

<table><thead><tr><th width="536"></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td><strong>Solana</strong></td><td><strong>✅</strong></td><td></td></tr><tr><td><strong>Ethereum</strong></td><td>✅</td><td></td></tr><tr><td><strong>Polygon</strong></td><td>✅</td><td></td></tr><tr><td><strong>Immutable X</strong></td><td>✅</td><td></td></tr><tr><td><strong>Avalanche</strong></td><td>✅</td><td></td></tr><tr><td><strong>Arbitrum</strong></td><td>✅</td><td></td></tr><tr><td><strong>Sui</strong></td><td>🔜</td><td></td></tr><tr><td><strong>Near</strong></td><td>🔜</td><td></td></tr><tr><td><strong>Wax</strong></td><td>🔜</td><td></td></tr></tbody></table>

## NFT Gating

After [importing all NFT collections](../../dashboard/management/import-NFTs/) that the game involves using the Elixir Dashboard, you will be able to use this endpoint, as NFT gating, to obtain all the NFTs that the user owns for these collections.

{% swagger method="get" path="/sdk/v2/nfts/user" baseUrl="https://kend.elixir.app" summary="User NFTs" %}
{% swagger-description %}
Retrieve an array with the collections and the tokens owned by the given user
{% endswagger-description %}

{% swagger-parameter in="header" name="x-api-key" type="String" required="true" %}
Public Key obtained in the developer dashboard
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="String" required="true" %}
Bearer \<JWT>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 1,
    "success": true,
    "data": [
        {
            "collectionName": "Chronos Travelers",
            "collection": "chronos-travelers",
            "image": "https://i.seadn.io/gcs/files/681b8b0af65f6ed6e49927b8c3d0d427.png?w=500&auto=format",
            "nfts": [
                {
                    "tokenId": "14",
                    "name": "Traveler",
                    "image": "https://chronospublic.s3.eu-west-2.amazonaws.com/travelers/redgenesis.gif",
                    "attributes": [
                        {
                            "trait_type": "Quantum Power",
                            "value": "321",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Rarity",
                            "value": "Mythic"
                        },
                        {
                            "trait_type": "Strength",
                            "value": "0"
                        },
                        {
                            "trait_type": "Defense",
                            "value": "1"
                        },
                        {
                            "trait_type": "Dexterity",
                            "value": "5"
                        },
                        {
                            "trait_type": "Intelligence",
                            "value": "1"
                        },
                        {
                            "trait_type": "Constitution",
                            "value": "1"
                        },
                        {
                            "trait_type": "Endurance",
                            "value": "1"
                        },
                        {
                            "trait_type": "Soul",
                            "value": "1"
                        },
                        {
                            "trait_type": "Strength Scaling",
                            "value": "88",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Defense Scaling",
                            "value": "95",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Dexterity Scaling",
                            "value": "73",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Intelligence Scaling",
                            "value": "69",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Constitution Scaling",
                            "value": "53",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Endurance Scaling",
                            "value": "55",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Soul Scaling",
                            "value": "53",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Scaling Score",
                            "value": "69",
                            "display_type": "boost_percentage"
                        },
                        {
                            "trait_type": "Starting Level",
                            "value": "10",
                            "display_type": "number"
                        },
                        {
                            "trait_type": "Skill Tree Type",
                            "value": "14",
                            "display_type": "number"
                        }
                    ]
                }
            ]
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    "code": -1,
    "success": false,
    "error": {
        "status": 400,
        "code": 1001,
        "message": "Invalid initialization vector"
    }
}
```
{% endswagger-response %}
{% endswagger %}

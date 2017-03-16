---
title: Bets API Specification v1.0

language_tabs:
  - shell

toc_footers:
  - <a href='/contactus'>Contact Us</a>

includes:
  - references
  - changes

search: true
---

# Introduction

Bets API is a RESTful service for data on all sports. It is a *PAID* service with low price (started with $10 per month).

Please note that in order to access Bets API you must [contact us](/contactus).

# Authentication

You will get a *token* from our support. you can either pass it in header *X-API-TOKEN* or pass as token= in GET query.

> To authorize, use this code:

```shell
# With shell, pass the correct header with each request
curl "api_endpoint_here"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

> Make sure to replace `YOUR-TOKEN` with your token.

`X-API-TOKEN: YOUR-TOKEN`

<aside class="notice">
You must replace <code>YOUR-TOKEN</code> with your personal token.
</aside>

## API Endpoints

API endpoint started with [https://api.betsapi.com/v1](https://api.betsapi.com/v1), http is also supported but https is recommended.

# Events

## InPlay/Upcoming/Ended Events

```shell
curl "https://api.betsapi.com/events/inplay?sport_id=1"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

> The above command returns JSON structured like this:

```json
{
    "success": 1,
    "pager": {
        "page": 1,
        "per_page": 50,
        "total": 12
    },
    "results": [
        {
            "id": "68384",
            "time": "1478076778",
            "time_status": "1",
            "league": {
                "id": "2103",
                "name": "FIBA Europe Cup"
            },
            "home": {
                "id": "7704",
                "name": "Enisey Krasnoyarsk"
            },
            "away": {
                "id": "56003",
                "name": "Sigal Prishtina"
            },
            "timer": {
                "tm": "2",
                "ts": "31",
                "q": "3"
            },
            "scores": {
                "1": {
                    "home": "22",
                    "away": "32"
                },
                "2": {
                    "home": "18",
                    "away": "18"
                },
                "3": {
                    "home": "40",
                    "away": "50"
                },
                "4": {
                    "home": "19",
                    "away": "13"
                },
                "5": {
                    "home": "",
                    "away": ""
                },
                "6": {
                    "home": "",
                    "away": ""
                },
                "7": {
                    "home": "59",
                    "away": "63"
                }
            }
        },
        {
        ...
        }
    ]
}
```

Get events for inplay/upcoming/ended

### HTTP Request

`GET https://api.betsapi.com/events/inplay`

`GET https://api.betsapi.com/events/upcoming`

`GET https://api.betsapi.com/events/ended`

### Query Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
league_id | No | useful when you want only one league
day | No | format YYYYMMDD, eg: 20161201
page | No | [Pager reference](#pager)

## Events Search

```shell
curl "https://api.betsapi.com/v1/events/search?token=YOUR_TOKEN&sport_id=1&home=Man%20City&away=Barcelona&time=1478029500"
```

> The above command returns JSON structured like this:

```json
{
    "success": 1,
    "results": [
        {
            "id": "54750",
            "time": "1478029500",
            "time_status": "3",
            "league": {
                "id": "1040",
                "name": "UEFA Champions League"
            },
            "home": {
                "id": "708",
                "name": "Man City"
            },
            "away": {
                "id": "1211",
                "name": "Barcelona"
            },
            "scores": {
                "2": {
                    "home": "3",
                    "away": "1"
                }
            }
        }
    ]
}
```

Search for event with home/away name plus date

### HTTP Request

`GET https://api.betsapi.com/v1/events/search`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport_id)
home | Yes | home team name
away | Yes | away team name
time | Yes | UTC time epoch


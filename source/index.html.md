---
title: Bets API Specification v1.0 - BetsAPI.com

language_tabs:
  - shell

toc_footers:
  - <a href='/'>BetsAPI.com</a>
  - <a href='/contactus'>Contact Us</a>

includes:
  - faq
  - references
  - changes
  - code_sample

search: true
---

# Introduction

Bets API is a RESTful service for data on all sports. It is a **PAID** service with low price (started with $10 per month).

Please note that in order to access Bets API you must [contact us](/contactus).

## Authentication

> To authorize, use this code:

```shell
# With shell, pass the correct header with each request
curl "api_endpoint_here"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

```shell
# With shell, pass the correct header with each request
curl "api_endpoint_here?token=YOUR-TOKEN"
```

> Make sure to replace `YOUR-TOKEN` with your token.

`X-API-TOKEN: YOUR-TOKEN`

You will get a **token** from our support. you can either pass it in header **X-API-TOKEN** or pass as token= in GET query.

<aside class="notice">
You must replace <code>YOUR-TOKEN</code> with your personal token.
</aside>

## API Endpoints

API endpoint started with [https://api.betsapi.com/v1](https://api.betsapi.com/v1), http is also supported but https is recommended.

## Rate Limatation

```shell
X-RateLimit-Limit:3600
X-RateLimit-Remaining:3599
X-RateLimit-Reset:1495857600
```

3600 requests per hour.

You can pay extra 50$ to setup standalone server for unlimited request.

You can check the values in headers:

Header Name | Description
--------- | -------
X-RateLimit-Limit | The maximum number of requests that the consumer is permitted to make per hour.
X-RateLimit-Remaining | The number of requests remaining in the current rate limit window.
X-RateLimit-Reset | The time at which the current rate limit window resets in UTC epoch seconds.

## Response

All responses are in JSON and has a **success** key to indicate it is successful or not.

You'll get **results** if everything moves well, and an [error](#errors) will be thrown if failed.</p>

# Pricing

Check [Pricing](/mm/pricing) for details, or [contact us](/contactus).

# Events

## InPlay Events

```shell
curl "https://api.betsapi.com/v1/events/inplay?sport_id=1"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

### HTTP Request

`GET https://api.betsapi.com/v1/events/inplay`

### Query Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
league_id | No | useful when you want only one league
page | No | [Pager reference](#pager)

### HTTP Response

[inplay.json](samples/inplay.json)

## Upcoming Events

```shell
curl "https://api.betsapi.com/v1/events/upcoming?sport_id=1"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

### HTTP Request

`GET https://api.betsapi.com/v1/events/upcoming`

### Query Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
league_id | No | useful when you want only one league
team_id | No | useful when you want only one team
day | No | format YYYYMMDD, eg: 20161201
page | No | [Pager reference](#pager)

### HTTP Response

[upcoming.json](samples/upcoming.json)

## Ended Events

```shell
curl "https://api.betsapi.com/v1/events/ended?sport_id=1"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

### HTTP Request

`GET https://api.betsapi.com/v1/events/ended`

### Query Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
league_id | No | useful when you want only one league
team_id | No | useful when you want only one team
day | No | format YYYYMMDD, eg: 20161201
page | No | [Pager reference](#pager)

### HTTP Response

[ended.json](samples/ended.json)

## Events Search

```shell
curl "https://api.betsapi.com/v1/events/search?token=YOUR_TOKEN\
&sport_id=1&home=Man%20City&away=Barcelona&time=1478029500"
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
time | Yes | UTC time epoch (Limited to 90 days)

### HTTP Response

[search.json](samples/search.json)

## Event View

```shell
curl "https://api.betsapi.com/v1/event/view?token=YOUR_TOKEN\
&event_id=92149"
```

### HTTP Request

`GET https://api.betsapi.com/v1/event/view`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
event_id | Yes | Event ID you get from events/*

<aside class="notice">you can send multiple event_ids in one request with event_id=1,2,3,4 up to max 10 ids.</aside>

### HTTP Response

[event_view.json](samples/event_view.json)

## Event History

```shell
curl "https://api.betsapi.com/v1/event/history?token=YOUR_TOKEN\
&event_id=219465"
```

History events of Home/Away Team before this event.

### HTTP Request

`GET https://api.betsapi.com/v1/event/history`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
event_id | Yes | Event ID you get from events/*

### HTTP Response

[event_history.json](samples/event_history.json)

## Event Odds Summary

```shell
curl "https://api.betsapi.com/v1/event/odds/summary?token=YOUR_TOKEN\
&event_id=232751"
```

### HTTP Request

`GET https://api.betsapi.com/v1/event/odds/summary`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
event_id | Yes | Event ID you get from events/*

### HTTP Response

[event_odds_summary.json](samples/event_odds_summary.json)

### Reference

Key| Description
--------- | -----------
1_1, 18_1 | 1X2
1_2, 18_2 | Asian Handicap
1_3, 18_3 | O/U
1_4 | Asian Corners
1_5 | Asian Handicap (Half)
1_6 | O/U (Half)
1_7 | Asian Corners (Half)
18_8 | Quarter - Handicap
18_9 | Quarter - Total (2-Way)

## Event Odds

```shell
curl "https://api.betsapi.com/v1/event/odds?token=YOUR_TOKEN\
&event_id=92149"
```

### HTTP Request

`GET https://api.betsapi.com/v1/event/odds`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
event_id | Yes | Event ID you get from events/*
source | No | Possible value: bet365, 10bet, ladbrokes, williamhill, betclic, pinnaclesports, planetwin365, ysb88, 188bet, unibet, bwin, betfair, betfred, cloudbet, betsson, betdaq, paddypower, sbobet, titanbet, betathome, dafabet. defaults to bet365.
since_time | No | Integer. add_time will be >= $since_time in results. Faster to get only updates.

### HTTP Response

[event_odds.json](samples/event_odds.json)

## League

```shell
curl "https://api.betsapi.com/v1/league?token=YOUR_TOKEN\
&sport_id=1"
```

### HTTP Request

`GET https://api.betsapi.com/v1/league`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
cc | No | Eg: 'co' for Colombia [Reference](#countries)
page | No | [Pager reference](#pager)

### HTTP Response

[league.json](samples/league.json)

## League Table

<aside class="notice">
Note a few of (less than 5%) teams do not have 'id'.
</aside>

```shell
curl "https://api.betsapi.com/v1/league/table?token=YOUR_TOKEN\
&league_id=94"
```

### HTTP Request

`GET https://api.betsapi.com/v1/league/table`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
league_id | Yes | flag 'has_leaguetable' from [League API](#league)

### HTTP Response

[league_table.json](samples/league_table.json)

## Team

```shell
curl "https://api.betsapi.com/v1/team?token=YOUR_TOKEN\
&sport_id=1"
```

### HTTP Request

`GET https://api.betsapi.com/v1/team`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
page | No | [Pager reference](#pager)

### HTTP Response

[team.json](samples/team.json)

# Bet365 API

<aside class="notice">
It requires bet365 permission, see Pricing for more details
</aside>

## Bet365 InPlay

```shell
curl "https://api.betsapi.com/v1/bet365/inplay?token=YOUR_TOKEN"
```

### HTTP Request

`GET https://api.betsapi.com/v1/bet365/inplay`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
raw | No | raw Bet365 body without parsing

### HTTP Response

[bet365_inplay.json](samples/bet365_inplay.json)

[Fields Explanation](bet365_fields.html)

## Bet365 Inplay Event

```shell
curl "https://api.betsapi.com/v1/bet365/event?token=YOUR_TOKEN\
&FI=60504279"
```

### HTTP Request

`GET https://api.betsapi.com/v1/bet365/event`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
FI | Yes | FI from Bet365 Inplay
raw | No | raw Bet365 body without parsing

### HTTP Response

[bet365_event.soccer.json](samples/bet365_event.soccer.json)
[bet365_event.basketball.json](samples/bet365_event.basketball.json)
[bet365_event.cricket.json](samples/bet365_event.cricket.json)

[Fields Explanation](bet365_fields.html)

## Bet365 Upcoming Events

```shell
curl "https://api.betsapi.com/v1/bet365/upcoming?sport_id=1"
  -H "X-API-TOKEN: YOUR-TOKEN"
```

<aside class="notice">
league.id/home.id/away.id returned from bet365/upcoming might be different than event/upcoming.
</aside>

### HTTP Request

`GET https://api.betsapi.com/v1/bet365/upcoming`

### Query Parameters

Parameter | Required? | Description
--------- | ------- | -----------
sport_id | Yes | [Reference](#sport-id)
league_id | No | useful when you want only one league
day | No | format YYYYMMDD, eg: 20161201
page | No | [Pager reference](#pager)

### HTTP Response

[bet365_upcoming.json](samples/bet365_upcoming.json)

## Bet365 PreMatch Odds

```shell
curl "https://api.betsapi.com/v1/bet365/start_sp?token=YOUR_TOKEN\
&event_id=60504279"
```

### HTTP Request

`GET https://api.betsapi.com/v1/bet365/start_sp`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
FI | Yes | Event ID you get from bet365/upcoming
raw | No | raw Bet365 body without parsing

### HTTP Response

[bet365_event.json](samples/bet365_prematch_odds.json)

## Bet365 Result

```shell
curl "https://api.betsapi.com/v1/bet365/result?token=YOUR_TOKEN\
&event_id=63543522"
```

It is useful when you have FI from Bet365 XML Feed and want to know the results.

### HTTP Request

`GET https://api.betsapi.com/v1/bet365/result`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
event_id | Yes | Event ID (FI) from Bet365 Inplay

### HTTP Response

[bet365_result.json](samples/bet365_result.json)

# BWin API

<aside class="notice">
It requires bwin permission, see Pricing for more details
</aside>

## BWin InPlay

```shell
curl "https://api.betsapi.com/v1/bwin/inplay?token=YOUR_TOKEN"
```

### HTTP Request

`GET https://api.betsapi.com/v1/bwin/inplay`

### HTTP Response

[bwin_inplay.json](samples/bwin_inplay.json)

## BWin Prematch Odds

```shell
curl "https://api.betsapi.com/v1/bwin/prematch?token=YOUR_TOKEN"
```

### HTTP Request

`GET https://api.betsapi.com/v1/bwin/prematch`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
day | No | format YYYYMMDD, eg: 20161201
sport_id | No | BWin sport_id

### HTTP Response

[bwin_prematch.json](samples/bwin_prematch.json)

## BWin Event

```shell
curl "https://api.betsapi.com/v1/bwin/event?token=YOUR_TOKEN\
&event_id=60504279"
```

### HTTP Request

`GET https://api.betsapi.com/v1/bwin/event`

### URL Parameters

Parameter | Required? | Description
--------- | ------- | -----------
event_id | Yes | Event ID you get from /bwin/inplay or prematch

### HTTP Response

[bwin_event.json](samples/bwin_event.json)

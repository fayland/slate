# FAQ

### How can I get all historical data?

First try with [League](#league) API, and go through [pager](#pager) to get all data.

Afterwards, pass each **league_id** in [Events](#ended-events) API with pager.

### How can I get all leagues in Brazil?

use [League](#league) API with cc=br. For example: http://api.betsapi.com/v1/league?token=YOUR-TOKEN&sport_id=1&cc=br

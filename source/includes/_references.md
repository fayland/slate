# References

## Sport ID

sport_id | Name
---------- | -------
1 | Soccer
18 | Basketball
13 | Tennis
91 | Volleyball
78 | Handball
16 | Baseball
17 | Ice Hockey
12 | American Football
14 | Snooker
3 | Cricket

## Errors

Error Code | Description
---------- | -------
INTERNAL_SERVER_ERROR | 500 Internal Server Error, contact Support if it happens
NOT_FOUND | 404 Not Found
METHOD_NOT_ALLOWED | Method is not allowed, only GET is supported.
UNDER_MAINTENANCE | API is under maintenance, we'll annouce it
AUTHORIZE_FAILED | Token is not provided or incorrect.
TOKEN_EXPIRED | Token is expired.
PERMISSION_DENIED | You're not allowed, contact Support if it is wrong.
PARAM_REQUIRED | Required param is missing, check error_detail for details
PARAM_INVALID | param is invalid, check error_detail for details

## Pager

Whenever you see **pager** in the API response, it means you can go next page by passing page=2 etc. there are 3 elements inside which means:

Error Code | Description
---------- | -------
page | Current page
per_page | how many results per page, default to 50 as always
total | how many results in total. use it to indicate that it has next page or not.

## time_status

Error Value | Description
---------- | -------
0 | Not Started
1 | InPlay
2 | TO BE FIXED
3 | Ended
4 | Postponed
5 | Cancelled

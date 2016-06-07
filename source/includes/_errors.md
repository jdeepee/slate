# Errors

The Loop API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The endpoint you tried to access is hidden for administrators only
404 | Not Found -- The endpoint you tried to access does not exsist
405 | Method Not Allowed -- You tried to access an endpoint with a invalid method
406 | Not Acceptable -- You requested a format that isn't json
429 | Too Many Requests -- You're requesting too many kittens! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.

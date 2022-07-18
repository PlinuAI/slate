# Errors
> Error output

```
HTTP/1.0 {Code} {Meaning}
Content-Type: application/json
Content-Length: {length of content}
Server: Werkzeug/{version} Python/{version}
Date: {day}, {# day} {month} {year} hh:mm:ss GMT

{
  "{error type}": "{explanation of the error}"
}
```
All errors in the Plinu API return an error code and a JSON with error type and an explanation of the error.

The Plinu API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid, you missed an element of the data.
401 | Unauthorized -- Your {user} {password} information is incorrect or your {token} is invalid or your user is inactive.
403 | Forbidden -- Your user does not have the appropiate permissions for this action.
404 | Not Found -- Variables, model, p2d or endpoint not found
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
500 | Internal Server Error -- We had a problem with our server. Try again later.
504 | Gateway Timeout -- The webpage grin.co did not respond within the max time. Try again later.

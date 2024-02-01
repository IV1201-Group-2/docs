# REST API

All microservices use a REST API (HTTP GET or POST). All functions should return JSON objects.

## HTTP response codes

* **200 OK** - API call was successful. The contents of the returned JSON object depends on the API call.
* **201 Created** - API call was successful and a new resource was created.
* **400 Bad Request** - API call failed validation.
* **401 Unauthorized** - Client is not logged in and tried to access a protected route without permission.
* **403 Forbidden** - Client is logged in and tried to access an API they don't have access to (for example, applicant tries to call recruiter API).
* **404 Not Found** - API with that name doesn't exist.
* **409 Conflict** - API call failed because of a conflict.
* **500 Internal Server Error** - This should be returned if the server panics or throws an exception.

## Error response

If the microservice encounters an error, it should return an object with the following structure:

```json
{
    "error": "...",
    "details": {...}
}
```

The `error` field should be one of the following error codes:

* (add error codes here)
* `UNKNOWN` - Unknown error

The error type should be translated to an error description on the frontend so that the user knows what went wrong.

The `details` field is optional and the contents depends on the error type.

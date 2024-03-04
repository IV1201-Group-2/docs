# REST API

All microservices use a REST API (HTTP GET or POST). All functions should return JSON objects.

## Available APIs

* **Register** - [apis/register.md](apis/register.md)
* **Login** - [apis/login.md](apis/login.md)
* **Password Reset** - [apis/password-reset.md](apis/password-reset.md)
* **Application Submission** - [apis/application-submission.md](apis/application-submission.md)
* **Application Status** - [apis/application-status.md](apis/application-status.md)
* **Competences** - [apis/competences.md](apis/competences.md)
* **Personal Info** - [apis/personal-info.md](apis/personal-info.md)

## HTTP response codes

* **200 OK** - API call was successful. The contents of the returned JSON object depends on the API call.
* **201 Created** - API call was successful and a new resource was created.
* **400 Bad Request** - API call failed validation.
* **401 Unauthorized** - Client is not logged in and tried to access a protected route or resource without permission.
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

The `error` field should describe the type of error that occured. The error code can be specific to an API call or one of these generic error codes:

* **`MISSING_PARAMETERS` (400 Bad Request)** - User did not provide all required query parameters
* **`TOKEN_EXPIRED` (401 Unauthorized)** - User's JWT token has expired
* **`UNKNOWN` (500 Internal Server Error)** - Unknown error

The error type should be translated to an error description on the frontend so that the user knows what went wrong.

The `details` field is optional and the contents depends on the error type.

# Competences Endpoint

`GET /api/application-form/competences`

## Additional requirements

* The user must be logged in when calling this API
* The user's JWT token must be included in the `Authorization` header

## Successful response

The API returns a list of competences with the following structure:

```json
[
    {
        "competence_id": 0,
        "name": "Python"
    },
    ...
]
```

## Error responses

#### `COMPETENCES_NOT_FOUND` (404 Not Found)

No competences were found in the database

#### `COULD_NOT_FETCH_COMPETENCES` (500 Internal Server Error)

There was an issue with the database operation when trying to fetch the competences

#### `UNAUTHORIZED` (401 Unauthorized)

User is not logged in (JWT token was not provided or is invalid)

#### `INVALID_TOKEN` (401 Unauthorized)

The provided JWT token is invalid (e.g., it is expired, not yet valid, or does not contain the required claims)

#### `TOKEN_NOT_PROVIDED` (401 Unauthorized)

No JWT token was provided in the `Authorization` header

#### `TOKEN_REVOKED` (401 Unauthorized)

The provided JWT token has been revoked

#### `INTERNAL_SERVER_ERROR` (500 Internal Server Error)

An unexpected error occurred
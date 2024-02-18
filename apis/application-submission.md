# Application Submission Endpoint

`POST /api/application-form/submit/`

## Additional requirements

* The user must be logged in when calling this API
* The user's JWT token must be included in the `Authorization` header
* The request body must contain a JSON object with the following structure:

```json
{
    "competences": [
        {
            "competence_id": 0,
            "years_of_experience": 5.67
        },
        ...
    ],
    "availabilities": [
        {
            "from_date": "2023-01-01",
            "to_date": "2023-12-31"
        },
        ...
    ]
}
```

## Successful response

The API returns a JSON object with the following structure:

```json
{
    "status": "application_status",
    "competences": [
        {
            "competence_id": 0,
            "years_of_experience": 5.67
        },
        ...
    ],
    "availabilities": [
        {
            "from_date": "2023-01-01",
            "to_date": "2023-12-31"
        },
        ...
    ]
}
```

## Error responses

#### `INVALID_JSON_PAYLOAD` (400 Bad Request)

The request body is not a valid JSON object

#### `INVALID_PAYLOAD_STRUCTURE` (400 Bad Request)

The structure of the JSON object in the request body is invalid

#### `MISSING_COMPETENCE_ID` (400 Bad Request)

A competence in the request body does not have a `competence_id` key

#### `MISSING_YEARS_OF_EXPERIENCE` (400 Bad Request)

A competence in the request body does not have a `years_of_experience` key

#### `INVALID_COMPETENCE_ID` (400 Bad Request)

A competence in the request body has an invalid `competence_id` value

#### `INVALID_YEARS_OF_EXPERIENCE` (400 Bad Request)

A competence in the request body has an invalid `years_of_experience` value

#### `MISSING_AVAILABILITIES` (400 Bad Request)

The request body does not have an `availabilities` key

#### `INVALID_AVAILABILITY` (400 Bad Request)

An availability in the request body is not a valid JSON object

#### `MISSING_FROM_DATE` (400 Bad Request)

An availability in the request body does not have a `from_date` key

#### `MISSING_TO_DATE` (400 Bad Request)

An availability in the request body does not have a `to_date` key

#### `INVALID_DATE_FORMAT` (400 Bad Request)

An availability in the request body has an invalid date format

#### `INVALID_DATE_RANGE` (400 Bad Request)

An availability in the request body has an invalid date range

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
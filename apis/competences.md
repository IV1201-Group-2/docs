
# Competences API

This API endpoint is used to retrieve a list of selectable competences.

`GET /api/application-form/competences/`

## Requirements

- The request must include a valid JWT token for authentication.

## Successful response

The API returns a JSON array of competences with the following structure:

```json
{
  "1": "Programming",
  "2": "Data Analysis"
}
```

## Error responses

#### `COMPETENCES_NOT_FOUND` (404 Not Found)

No competences found in the database.

#### `COULD_NOT_FETCH_COMPETENCES` (500 Internal Server Error)

Could not fetch competences from the database due to an internal error.

#### `INVALID_JWT_TOKEN` (401 Unauthorized)

This error occurs when the provided JWT token is not valid.

#### `TOKEN_EXPIRED` (401 Unauthorized)

This error is returned when the JWT token has expired and is no longer valid.

#### `UNAUTHORIZED` (401 Forbidden)

This error is returned when a request is made without a required JWT token or the token is not provided correctly.
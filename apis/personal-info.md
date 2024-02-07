
# Personal Information API

This API endpoint is used to retrieve personal information for the current user.

`GET /api/application-form/applicant/personal-info/`

## Requirements

- The request must include a valid JWT token for authentication.

## Successful response

The API returns a JSON object with the personal information of the current user:

```json
{
  "id": 123,
  "name": "John",
  "surname": "Doe",
  "pnr": "123456789",
  "email": "john.doe@example.com",
  "username": "johndoe",
  "role": 1
}
```

## Error responses

#### `USER_NOT_FOUND` (404 Not Found)

User not found with the provided id.

#### `COULD_NOT_FETCH_USER` (500 Internal Server Error)

Could not fetch user from the database due to an internal error.

#### `INVALID_JWT_TOKEN` (401 Unauthorized)

This error occurs when the provided JWT token is not valid.

#### `TOKEN_EXPIRED` (401 Unauthorized)

This error is returned when the JWT token has expired and is no longer valid.

#### `UNAUTHORIZED` (401 Forbidden)

This error is returned when a request is made without a required JWT token or the token is not provided correctly.
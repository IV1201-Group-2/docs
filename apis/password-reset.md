# Password Reset API

This API is used by applicants that need to recreate their password in the database. The login API will send a reset token through a secure channel (such as email) that identifies the user for a limited time.

`POST /api/reset?password={password}`

* `password` - New password of the account

## Additional requirements

* The user's temporary reset token must be included in the `Authorization` header.
* The token must have its `usage` claim set to `reset`.
* The user cannot be logged in when calling this API.

## Successful response

The API will automatically authenticate the user after resetting the password. The API returns a JSON object with the same structure as the login API.

## Error responses

#### `MISSING_PARAMETERS` (400 Bad Request)

User did not provide a new password.

#### `TOKEN_EXPIRED` (401 Unauthorized)

Reset token has expired.

#### `ALREADY_LOGGED_IN` (400 Bad Request)

A login token was provided instead of a reset token.

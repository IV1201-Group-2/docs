# Login API

This API is used by applicants and recruiters to obtain access to protected routes.

`POST /login?identity={identity}&password={password}&role={role}`

* `identity` - Username OR email address of the account
* `password` - Password of the account
* `role` - The role that the user wants to obtain access to
  * `1` - Recruiter
  * `2` - Applicant

## Additional requirements

* Role IDs are defined by the database
* The user cannot be logged in when calling this API

## Successful response

The API returns an object with the following structure:

```json
{
    "token": "..."
}
```

The token is a JWT token encoded with HS256. The payload should decode to a JSON object with the following structure:

```json
{
    "id": 0,
    "username": "mockuser_applicant",
    "email": "mockuser-applicant@example.com",
    "role": 2,

    "iat": 1706887684,
    "exp": 1706891284
}
```

`iat` and `exp` are standard JWT claims that specify when the token was created and when it expires.

## Error responses

#### `MISSING_PARAMETERS` (400 Bad Request)

User did not provide identity, password or desired role.

#### `MISSING_PASSWORD` (404 Not Found)

User does not have a password in the database.
They should be informed of what they need to do to set a new password.

#### `WRONG_IDENTITY` (401 Unauthorized)

No account was found with that specific username or email address

#### `WRONG_PASSWORD` (401 Unauthorized)

Account was found but the wrong password was provided

#### `ALREADY_LOGGED_IN` (400 Bad Request)

User is already logged in (JWT token was provided)

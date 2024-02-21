# Register API

This API is used for applicants to register an account in order to create appilcation profiles in the system.

`POST /api/register`

## The Request Body

- `name` - The first name of the user
- `surname` - The last name of the user
- `pnr` - The social security number of the user
- `email` - The email of the user
- `password` - The password of the user
- `username` - The username of the account

## Additional requirements

- Person IDs are automatically generated and incremented by the database
- Role IDs are automaticcaly set to Applicant during registration with all the roles in the database being:
  - `1` - Recruiter
  - `2` - Applicant

## Successful response - HTTP/1.1 200 OK

The API responds with an HTTP status 200 OK.

## Error responses

#### `MISSING_PARAMETERS` (400 Bad Request)

User did not provide either or all of name, surname, social security number, email, password or username.

#### `INVALID_EMAIL` (400 Bad Request)

User did not provide an email with the correct format containing local-part@domain-part

#### `USERNAME_TAKEN` (400 Bad Request)

User is attempting to register with a usernam that already exists in the database

#### `EMAIL_TAKEN` (400 Bad Request)

User is attempting to register with an email that already exists in the database

#### `PNR_TAKEN` (400 Bad Request)

User is attempting to register with a social security number that already exists in the database

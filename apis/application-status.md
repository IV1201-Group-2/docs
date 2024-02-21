# Application Status API

This API is used for handling application status for applications in the system.

`POST /api/applicant`

## The Request Body

- `person_id` - The id of a person who has an application
- `status` - The status of the application

## Successful response - HTTP/1.1 200 OK

The API responds with an HTTP status 200 OK.

## Error responses

#### `INVALID_DATA` (400 Bad Request)

User did not provide either or all of name, surname, social security number, email, password or username.

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

Either an invalid person_id or an invalid status was received. A person_id is considered invalid if it can not be found in the person table. A status is considered invalid if it is anything other then Accept/Reject/Pending.


# Applicant Competences API

This API endpoint is designed for storing applicant competences.

`POST /api/application-form/applicant/competences/`

## Requirements

- The request must include a valid JWT token for authentication.

### Request Body

- The request body must be a JSON payload containing a list of competences. Each competence should be an object with the following keys:
    - `competence_id` - The unique identifier of the competence.
    - `experience` - The years of experience the applicant has with this competence.

Example request body:

```json
[
  {
    "competence_id": 1,
    "experience": 5
  },
  {
    "competence_id": 2,
    "experience": 3
  }
]
```

### Successful Response

- **Status Code:** `200 OK`
- **Content:** Returns a JSON object containing arrays of `successes` and `failures`. 
- Each entry in `successes` includes the stored competence's details, and each entry in `failures` includes the competence ID and the error encountered.

Example successful response:

```json
{
  "successes": [
    {
      "person_id": 123,
      "competence_id": 1,
      "years_of_experience": 5
    }
  ],
  "failures": []
}
```

### Error Responses

#### `INVALID_JSON_PAYLOAD` (400 Bad Request)

- **Content:** `{"error": "INVALID_JSON_PAYLOAD"}`
- Occurs if the request body is not a valid JSON list.

#### Validation Errors

- If the provided competences contain invalid data (e.g., incorrect `competence_id` or `experience` values), the response will include these as failures within the `failures` array, each with a descriptive error message.

#### `INVALID_JWT_TOKEN` (401 Unauthorized)

This error occurs when the provided JWT token is not valid.

#### `TOKEN_EXPIRED` (401 Unauthorized)

This error is returned when the JWT token has expired and is no longer valid.

#### `UNAUTHORIZED` (401 Forbidden)

This error is returned when a request is made without a required JWT token or the token is not provided correctly.
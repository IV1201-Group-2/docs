# REST API

All microservices use a REST API. All functions should return JSON objects.

## HTTP response codes

TODO

## Error codes

If the microservice encounters an error, it should return an object with the following structure:
```json
{
	"error": "...",
	"message": "..."
}
```

The `error` field should be one of the following error codes:
(add error codes here)

The `message` field should describe the error in English to the user.
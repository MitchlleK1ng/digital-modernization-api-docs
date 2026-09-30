# API Errors

## Overview

The API uses standard HTTP status codes and a consistent JSON response structure to communicate errors.

Clients should use the HTTP status code to identify the general category of an error and the error code to determine the specific cause.

The examples in this document are illustrative and belong to the Digital Modernization Program.

---

## Error Response Format

API errors use the following structure:

```json
{
  "error": {
    "code": "error_code",
    "message": "Description of the error."
  }
}
```

### Error Fields

| Field           | Type   | Description                                |
| --------------- | ------ | ------------------------------------------ |
| `error`         | object | Contains information about the error.      |
| `error.code`    | string | Machine-readable identifier for the error. |
| `error.message` | string | Human-readable description of the error.   |

Clients should use `error.code` for application logic rather than relying on the text of the `message` field.

---

## HTTP Status Codes

The API uses the following HTTP status codes.

| Status Code | Name                  | Description                                                                        |
| ----------- | --------------------- | ---------------------------------------------------------------------------------- |
| `400`       | Bad Request           | The request contains invalid or incomplete data.                                   |
| `401`       | Unauthorized          | Authentication is missing or invalid.                                              |
| `403`       | Forbidden             | The client is authenticated but does not have permission to perform the operation. |
| `404`       | Not Found             | The requested resource does not exist.                                             |
| `409`       | Conflict              | The request conflicts with the current state of the resource.                      |
| `429`       | Too Many Requests     | The client has exceeded the permitted request rate.                                |
| `500`       | Internal Server Error | An unexpected server-side error occurred.                                          |

---

## 400 Bad Request

The server returns `400 Bad Request` when the request cannot be processed because the submitted data is invalid or incomplete.

### Example

```http
HTTP/1.1 400 Bad Request
```

```json
{
  "error": {
    "code": "invalid_request",
    "message": "The email field is required."
  }
}
```

### Common Causes

* Required field is missing.
* Field contains an invalid value.
* Request body contains invalid JSON.
* Query parameter has an unsupported value.

### Client Action

Review the request data, correct the invalid fields, and submit the request again.

---

## 401 Unauthorized

The server returns `401 Unauthorized` when authentication is missing or invalid.

### Example

```http
HTTP/1.1 401 Unauthorized
```

```json
{
  "error": {
    "code": "unauthorized",
    "message": "Authentication is required."
  }
}
```

### Common Causes

* Authorization header is missing.
* Access token is invalid.
* Access token has expired.

### Client Action

Verify that a valid access token is included in the request.

For more information, see [Authentication](authentication.md).

---

## 403 Forbidden

The server returns `403 Forbidden` when the client is authenticated but does not have the permission required for the requested operation.

### Example

```http
HTTP/1.1 403 Forbidden
```

```json
{
  "error": {
    "code": "forbidden",
    "message": "The client does not have permission to perform this operation."
  }
}
```

### Common Causes

* Client does not have the required permission.
* Client is authenticated with insufficient access.
* Operation is restricted to authorized clients.

### Client Action

Verify that the authenticated client has the required permission.

For example, updating a customer requires the `customers:update` permission.

---

## 404 Not Found

The server returns `404 Not Found` when the requested resource does not exist.

### Example

```http
HTTP/1.1 404 Not Found
```

```json
{
  "error": {
    "code": "customer_not_found",
    "message": "The requested customer could not be found."
  }
}
```

### Common Causes

* Customer ID does not exist.
* Resource has been removed or is no longer available.
* URL contains an incorrect resource identifier.

### Client Action

Verify the resource identifier and confirm that the resource exists.

---

## 409 Conflict

The server returns `409 Conflict` when a request conflicts with the current state of a resource.

### Example

```http
HTTP/1.1 409 Conflict
```

```json
{
  "error": {
    "code": "customer_exists",
    "message": "A customer with the specified email already exists."
  }
}
```

### Common Causes

* Attempting to create a duplicate customer.
* Request conflicts with an existing resource.

### Client Action

Review the existing resource before retrying the request.

---

## 429 Too Many Requests

The server returns `429 Too Many Requests` when a client exceeds the permitted request rate.

### Example

```http
HTTP/1.1 429 Too Many Requests
```

```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "Too many requests. Please try again later."
  }
}
```

### Client Action

Wait before sending additional requests.

Clients should implement retry logic with an appropriate delay when retrying requests after receiving a `429` response.

---

## 500 Internal Server Error

The server returns `500 Internal Server Error` when an unexpected problem occurs while processing a request.

### Example

```http
HTTP/1.1 500 Internal Server Error
```

```json
{
  "error": {
    "code": "internal_error",
    "message": "An unexpected error occurred."
  }
}
```

### Client Action

Do not repeatedly retry the request immediately.

If the problem persists, contact the appropriate system support team and provide relevant request information without exposing authentication credentials or sensitive data.

---

## Error Code Reference

The following table summarizes the error codes defined for the API.

| Error Code            | HTTP Status | Description                                   |
| --------------------- | ----------: | --------------------------------------------- |
| `invalid_request`     |       `400` | Request data is invalid or incomplete.        |
| `unauthorized`        |       `401` | Authentication is missing or invalid.         |
| `forbidden`           |       `403` | Client does not have the required permission. |
| `customer_not_found`  |       `404` | Requested customer does not exist.            |
| `customer_exists`     |       `409` | Customer already exists.                      |
| `rate_limit_exceeded` |       `429` | Client has exceeded the request rate limit.   |
| `internal_error`      |       `500` | Unexpected server-side error.                 |

---

## Troubleshooting Guidance

When an API request fails, use the following process:

1. Check the HTTP status code.
2. Review the `error.code` value.
3. Read the `error.message` for additional context.
4. Verify the request URL and parameters.
5. Verify authentication and required permissions.
6. Correct the request if necessary.
7. Retry the request only when appropriate.

Do not include access tokens, passwords, or other sensitive information when reporting an API error.

---

## Related Documentation

* [API Overview](api-overview.md)
* [Authentication](authentication.md)
* [Customers API](customers.md)
* [Versioning](versioning.md)


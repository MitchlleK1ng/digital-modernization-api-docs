# API Authentication

## Purpose

This document describes the authentication and authorization requirements for the Customer Management API.

The API uses bearer tokens to authenticate clients accessing protected resources.

## Authentication Overview

Clients must provide a valid access token when making requests to protected API endpoints.

The access token is sent in the `Authorization` HTTP header using the following format:

```http
Authorization: Bearer <access-token>
```

Example:

```http
GET /v1/customers/cus_10001 HTTP/1.1
Host: api.customers.com
Authorization: Bearer <access-token>
```

Requests that do not contain valid authentication credentials will not be permitted to access protected resources.

## Access Tokens

An access token represents an authenticated client's authorization to access specific API resources.

For this API, access tokens are issued through the organization's approved authentication service.

Clients must:

* Store access tokens securely.
* Avoid exposing tokens in source code.
* Avoid including tokens in URLs.
* Avoid writing tokens to application logs.
* Transmit tokens only over HTTPS.
* Request only the permissions required by the application.

## Authorization

Authentication verifies the identity of a client.

Authorization determines whether the authenticated client has permission to perform a requested operation.

For example, a client may be authorized to retrieve customer information but may not have permission to create or deactivate customer records.

## Permissions

The API uses permissions to control access to customer operations.

Example permissions include:

| Permission             | Description                              |
| ---------------------- | ---------------------------------------- |
| `customers:read`       | Retrieve and search customer information |
| `customers:create`     | Create customer records                  |
| `customers:update`     | Update customer records                  |
| `customers:deactivate` | Deactivate customer records              |

Clients should be assigned only the permissions required for their intended use.

## Authentication Header

Every protected API request must include the `Authorization` header.

Example:

```http
Authorization: Bearer eyJhbGciOi...
```

The token shown above is illustrative and is not a real credential.

## HTTPS Requirement

All API requests must use HTTPS.

Example:

```text
https://api.customers.com/v1/customers
```

Unencrypted HTTP connections must not be used for API communication.

HTTPS protects authentication credentials and other information transmitted between the client and API.

## Authentication Errors

The API uses standard HTTP status codes to communicate authentication and authorization failures.

### 401 Unauthorized

The API returns `401 Unauthorized` when authentication is missing or invalid.

Example:

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json
```

Example response:

```json
{
  "error": {
    "code": "unauthorized",
    "message": "Authentication is required."
  }
}
```

Common causes include:

* Missing `Authorization` header
* Expired access token
* Invalid access token
* Malformed authentication credentials

### 403 Forbidden

The API returns `403 Forbidden` when the client is authenticated but does not have permission to perform the requested operation.

Example:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json
```

Example response:

```json
{
  "error": {
    "code": "forbidden",
    "message": "The client does not have permission to perform this operation."
  }
}
```

## Example Authenticated Request

The following example retrieves a customer record:

```bash
curl -X GET "https://api.customers.com/v1/customers/cus_10001" \
  -H "Authorization: Bearer <access-token>"
```

Example successful response:

```json
{
  "customerId": "cus_10001",
  "name": "Jordan Smith",
  "email": "jordan.smith@outlook.com",
  "status": "active"
}
```

## Token Security

Clients are responsible for protecting their access tokens.

Do not:

* Commit tokens to Git repositories.
* Include tokens in screenshots.
* Share tokens through unsecured communication channels.
* Store tokens in publicly accessible configuration files.
* Include tokens in URLs.

If a credential is accidentally exposed, it should be revoked or rotated according to the organization's security procedures.

## Authentication and API Documentation

Individual endpoint documentation identifies the permissions required for each operation.

For example:

| Endpoint                  | Method | Required Permission    |
| ------------------------- | ------ | ---------------------- |
| `/customers`              | GET    | `customers:read`       |
| `/customers/{customerId}` | GET    | `customers:read`       |
| `/customers`              | POST   | `customers:create`     |
| `/customers/{customerId}` | PUT    | `customers:update`     |
| `/customers/{customerId}` | DELETE | `customers:deactivate` |

## Security Considerations

Authentication and authorization controls should be reviewed as part of the organization's security and compliance processes.




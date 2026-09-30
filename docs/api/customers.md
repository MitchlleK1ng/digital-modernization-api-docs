# Customers API

## Overview

The Customers API provides endpoints for creating, retrieving, updating, searching, and deactivating customer records.

All endpoints require authentication and use JSON for request and response data.

**Base URL:**

```text
https://api.customers.com/v1


---

## Customer Resource

A customer record contains information used to identify and manage a customer.

| Field        | Type   | Description                                |
| ------------ | ------ | ------------------------------------------ |
| `customerId` | string | Unique identifier for the customer.        |
| `name`       | string | Customer's full name.                      |
| `email`      | string | Customer's email address.                  |
| `phone`      | string | Customer's telephone number.               |
| `status`     | string | Current customer status.                   |
| `address`    | object | Customer's address information.            |
| `createdAt`  | string | Date and time the record was created.      |
| `updatedAt`  | string | Date and time the record was last updated. |

Example customer object:

```json
{
  "customerId": "cus_10001",
  "name": "Alex Morgan",
  "email": "alex.morgan@outlook.com",
  "phone": "+1-555-0100",
  "status": "active",
  "address": {
    "street": "100 Main Street",
    "city": "Austin",
    "state": "TX",
    "postalCode": "78701",
    "country": "US"
  },
  "createdAt": "2026-09-01T14:30:00Z",
  "updatedAt": "2026-09-01T14:30:00Z"
}
```

---

## Retrieve a Customer

Retrieves a single customer by customer ID.

### Request

```http
GET /customers/{customerId}
```

### Authentication

Requires the `customers:read` permission.

### Path Parameters

| Parameter    | Type   | Required | Description                        |
| ------------ | ------ | -------- | ---------------------------------- |
| `customerId` | string | Yes      | Unique identifier of the customer. |

### Example Request

```bash
curl -X GET "https://api.customers.com/v1/customers/cus_10001" \
  -H "Authorization: Bearer <access-token>"
```

### Example Response

```json
{
  "customerId": "cus_10001",
  "name": "Alex Morgan",
  "email": "alex.morgan@outlook.com",
  "phone": "+1-555-0100",
  "status": "active",
  "address": {
    "street": "100 Main Street",
    "city": "Austin",
    "state": "TX",
    "postalCode": "78701",
    "country": "US"
  },
  "createdAt": "2026-09-01T14:30:00Z",
  "updatedAt": "2026-09-01T14:30:00Z"
}
```

### Status Codes

| Status                      | Description                                   |
| --------------------------- | --------------------------------------------- |
| `200 OK`                    | Customer retrieved successfully.              |
| `401 Unauthorized`          | Authentication is missing or invalid.         |
| `403 Forbidden`             | Client does not have the required permission. |
| `404 Not Found`             | Customer does not exist.                      |
| `500 Internal Server Error` | Unexpected server error.                      |

---

## Create a Customer

Creates a new customer record.

### Request

```http
POST /customers
```

### Authentication

Requires the `customers:create` permission.

### Request Body

| Field     | Type   | Required | Description                     |
| --------- | ------ | -------- | ------------------------------- |
| `name`    | string | Yes      | Customer's full name.           |
| `email`   | string | Yes      | Customer's email address.       |
| `phone`   | string | No       | Customer's telephone number.    |
| `address` | object | No       | Customer's address information. |

### Example Request

```bash
curl -X POST "https://api.customers.com/v1/customers" \
  -H "Authorization: Bearer <access-token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Alex Morgan",
    "email": "alex.morgan@outlook.com",
    "phone": "+1-555-0100",
    "address": {
      "street": "100 Main Street",
      "city": "Austin",
      "state": "TX",
      "postalCode": "78701",
      "country": "US"
    }
  }'
```

### Example Response

```json
{
  "customerId": "cus_10002",
  "name": "Alex Morgan",
  "email": "alex.morgan@outlook.com",
  "phone": "+1-555-0100",
  "status": "active",
  "address": {
    "street": "100 Main Street",
    "city": "Austin",
    "state": "TX",
    "postalCode": "78701",
    "country": "US"
  },
  "createdAt": "2026-09-30T14:30:00Z",
  "updatedAt": "2026-09-30T14:30:00Z"
}
```

### Status Codes

| Status                      | Description                                   |
| --------------------------- | --------------------------------------------- |
| `201 Created`               | Customer created successfully.                |
| `400 Bad Request`           | Request contains invalid or missing data.     |
| `401 Unauthorized`          | Authentication is missing or invalid.         |
| `403 Forbidden`             | Client does not have the required permission. |
| `409 Conflict`              | Customer already exists.                      |
| `500 Internal Server Error` | Unexpected server error.                      |

---

## Update a Customer

Updates an existing customer record.

### Request

```http
PUT /customers/{customerId}
```

### Authentication

Requires the `customers:update` permission.

### Path Parameters

| Parameter    | Type   | Required | Description                        |
| ------------ | ------ | -------- | ---------------------------------- |
| `customerId` | string | Yes      | Unique identifier of the customer. |

### Request Body

```json
{
  "name": "Alex Morgan",
  "email": "alex.morgan@outlook.com",
  "phone": "+1-555-0199"
}
```

### Example Request

```bash
curl -X PUT "https://api.customers.com/v1/customers/cus_10001" \
  -H "Authorization: Bearer <access-token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Alex Morgan",
    "email": "alex.morgan@example.com",
    "phone": "+1-555-0199"
  }'
```

### Example Response

```json
{
  "customerId": "cus_10001",
  "name": "Alex Morgan",
  "email": "alex.morgan@outlook.com",
  "phone": "+1-555-0199",
  "status": "active",
  "updatedAt": "2026-09-30T15:00:00Z"
}
```

### Status Codes

| Status                      | Description                                   |
| --------------------------- | --------------------------------------------- |
| `200 OK`                    | Customer updated successfully.                |
| `400 Bad Request`           | Request contains invalid data.                |
| `401 Unauthorized`          | Authentication is missing or invalid.         |
| `403 Forbidden`             | Client does not have the required permission. |
| `404 Not Found`             | Customer does not exist.                      |
| `500 Internal Server Error` | Unexpected server error.                      |

---

## Search Customers

Returns a list of customers matching the supplied search criteria.

### Request

```http
GET /customers
```

### Authentication

Requires the `customers:read` permission.

### Query Parameters

| Parameter | Type    | Required | Description                         |
| --------- | ------- | -------- | ----------------------------------- |
| `name`    | string  | No       | Filters customers by name.          |
| `email`   | string  | No       | Filters customers by email address. |
| `status`  | string  | No       | Filters customers by status.        |
| `page`    | integer | No       | Page number.                        |
| `limit`   | integer | No       | Maximum number of records returned. |

### Example Request

```bash
curl -X GET "https://api.customers.com/v1/customers?status=active&page=1&limit=20" \
  -H "Authorization: Bearer <access-token>"
```

### Example Response

```json
{
  "data": [
    {
      "customerId": "cus_10001",
      "name": "Alex Morgan",
      "email": "alex.morgan@outlook.com",
      "status": "active"
    },
    {
      "customerId": "cus_10002",
      "name": "Jordan Lee",
      "email": "jordan.lee@outlook.com",
      "status": "active"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 2
  }
}
```

### Status Codes

| Status                      | Description                                   |
| --------------------------- | --------------------------------------------- |
| `200 OK`                    | Search completed successfully.                |
| `400 Bad Request`           | One or more query parameters are invalid.     |
| `401 Unauthorized`          | Authentication is missing or invalid.         |
| `403 Forbidden`             | Client does not have the required permission. |
| `500 Internal Server Error` | Unexpected server error.                      |

---

## Deactivate a Customer

Deactivates a customer record.

Deactivation does not permanently delete the customer record. The customer's status is changed to `inactive`.

### Request

```http
DELETE /customers/{customerId}
```

### Authentication

Requires the `customers:deactivate` permission.

### Path Parameters

| Parameter    | Type   | Required | Description                        |
| ------------ | ------ | -------- | ---------------------------------- |
| `customerId` | string | Yes      | Unique identifier of the customer. |

### Example Request

```bash
curl -X DELETE "https://api.outlook.com/v1/customers/cus_10001" \
  -H "Authorization: Bearer <access-token>"
```

### Example Response

A successful deactivation returns no response body.

```http
204 No Content
```

### Status Codes

| Status                      | Description                                   |
| --------------------------- | --------------------------------------------- |
| `204 No Content`            | Customer deactivated successfully.            |
| `401 Unauthorized`          | Authentication is missing or invalid.         |
| `403 Forbidden`             | Client does not have the required permission. |
| `404 Not Found`             | Customer does not exist.                      |
| `500 Internal Server Error` | Unexpected server error.                      |

---

## Error Response

The API uses a consistent error structure.

Example:

```json
{
  "error": {
    "code": "customer_not_found",
    "message": "The requested customer could not be found."
  }
}
```

Common error codes include:

| Error Code           | Description                                   |
| -------------------- | --------------------------------------------- |
| `invalid_request`    | Request data is invalid or incomplete.        |
| `unauthorized`       | Authentication is missing or invalid.         |
| `forbidden`          | Client does not have the required permission. |
| `customer_not_found` | Requested customer does not exist.            |
| `customer_exists`    | Customer already exists.                      |
| `internal_error`     | Unexpected server error.                      |

For additional error-handling information, see [Errors](errors.md).

---

## Requirements Traceability

The Customers API implements the functional requirements defined in the project requirements document.

| Requirement                | API Operation                    |
| -------------------------- | -------------------------------- |
| FR-001 Retrieve Customer   | `GET /customers/{customerId}`    |
| FR-002 Create Customer     | `POST /customers`                |
| FR-003 Update Customer     | `PUT /customers/{customerId}`    |
| FR-004 Search Customers    | `GET /customers`                 |
| FR-005 Deactivate Customer | `DELETE /customers/{customerId}` |
| FR-006 API Versioning      | `/v1` base path                  |

---

## Related Documentation

* [API Overview](api-overview.md)
* [Authentication](authentication.md)
* [Errors](errors.md)
* [Versioning](versioning.md)
* [Project Requirements](../requirements.md)

---

# API Versioning

## Overview

The Digital Modernization API uses URL-based versioning to manage changes to the API while maintaining compatibility for existing clients.

The API version is included in the URL path.

```text
https://api.customers.com/v1

---

## Version Format

API versions use the following format:

```text
/v{major-version}
```

The initial API release uses version `v1`.

Example:

```http
GET /v1/customers/cus_10001
```

---

## Why the API Uses Versioning

API versioning helps the organization introduce changes without unexpectedly disrupting applications that depend on an existing API version.

Versioning provides a clear boundary between major API changes and allows clients time to evaluate and adopt newer versions.

---

## Current Version

The current API version is:

```text
v1
```

The base URL is:

```text
https://api.customers.com/v1
```

Example request:

```bash
curl -X GET "https://api.customers.com/v1/customers/cus_10001" \
  -H "Authorization: Bearer <access-token>"
```

---

## Versioning Rules

The following rules apply to the API.

### Major Changes

A new major API version should be introduced when a change could break existing client integrations.

Examples include:

* Removing an existing endpoint.
* Removing a required response field.
* Changing the meaning of an existing field.
* Changing the data type of an existing field.
* Changing authentication requirements in a way that affects existing clients.

A breaking change may result in a new version such as:

```text
/v2
```

---

### Non-Breaking Changes

Changes that do not break existing integrations may be introduced within the current major version.

Examples include:

* Adding a new optional request field.
* Adding a new response field.
* Adding a new endpoint.
* Adding additional documentation.
* Improving error messages without changing existing error codes.

Non-breaking changes do not require a new major version.

---

## Version Migration

When a new major version becomes available, clients should migrate from the previous version according to the organization's migration guidance.

For example:

```text
Current:
https://api.customers.com/v1/customers

Future:
https://api.customers.com/v2/customers
```

Migration documentation should identify:

* Changes between versions.
* Deprecated endpoints or fields.
* Required client updates.
* Authentication changes.
* Request and response differences.
* Migration deadlines.
* Validation requirements.

---

## Deprecation

When an API version is scheduled for retirement, clients should receive advance notice.

A deprecation notice should include:

1. The API version being deprecated.
2. The planned retirement date.
3. The replacement API version.
4. Changes that clients must make.
5. Migration documentation.
6. Contact information for support.

Example:

```text
API version v1 is scheduled for deprecation.

Replacement version: v2
Migration deadline: 2027-12-31
```

The dates shown above are illustrative only.

---

## Client Responsibilities

API clients are responsible for monitoring API documentation and updating integrations when required.

Clients should:

* Explicitly specify the API version they use.
* Review release and deprecation notices.
* Test integrations before migrating to a new version.
* Update API documentation references.
* Validate authentication and authorization requirements.
* Verify request and response behavior after migration.

Clients should not assume that a new major version is backward compatible with the previous version.

---

## Documentation Requirements

Each API version should have corresponding documentation.

Version-specific documentation should clearly identify:

* API version.
* Supported endpoints.
* Authentication requirements.
* Request formats.
* Response formats.
* Error behavior.
* Deprecated functionality.
* Migration requirements.

This approach allows developers and technical support teams to identify which API behavior applies to a specific client integration.

---

## Version Comparison Example

The following example illustrates how documentation could compare two major API versions.

| Feature           | v1              | v2                    |
| ----------------- | --------------- | --------------------- |
| Customer endpoint | `/v1/customers` | `/v2/customers`       |
| Authentication    | Bearer token    | Bearer token          |
| Customer ID       | `customerId`    | `customerId`          |
| Response format   | JSON            | JSON                  |
| Breaking changes  | N/A             | Documented separately |
| Migration guide   | N/A             | Required              |

The `v2` details above are illustrative and do not represent an actual implementation.

---

## Versioning and Requirements

API versioning supports requirement **FR-006: API Versioning** defined in the project requirements.

The requirement specifies that the API must provide a mechanism for managing changes while minimizing disruption to existing integrations.

For more information, see [Project Requirements](../requirements.md).

---

## Related Documentation

* [API Overview](api-overview.md)
* [Authentication](authentication.md)
* [Customers API](customers.md)
* [Errors](errors.md)
* [Project Requirements](../requirements.md)

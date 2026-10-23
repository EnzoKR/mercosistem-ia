---
platform: software-house
format: api-documentation
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: API Documentation

## Core Principles

API documentation is the contract between your service and every developer who integrates with it. Incomplete or inaccurate docs erode trust and generate avoidable support tickets.

- **Docs are part of the product.** Treat documentation as a shippable feature with the same quality bar as code.
- **Show, don't just tell.** Every endpoint needs a working example request and response.
- **Keep docs in sync with code.** Stale documentation is worse than no documentation — it actively misleads.
- **Docs-as-code:** Version API docs alongside the API code; review documentation changes in the same PR.

## OpenAPI / Swagger Standard

Use OpenAPI 3.1 (preferred) or OpenAPI 3.0 as the specification format. All endpoints should be described in a machine-readable `openapi.yaml` or `openapi.json` file.

### Required Fields Per Endpoint

```yaml
/users/{id}:
  get:
    summary: Get a user by ID
    description: |
      Returns a single user object. Requires authentication.
      Returns 404 if the user does not exist.
    operationId: getUserById
    tags:
      - Users
    parameters:
      - name: id
        in: path
        required: true
        description: The unique identifier of the user
        schema:
          type: string
          format: uuid
          example: "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
    responses:
      "200":
        description: User found
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/User"
            example:
              id: "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
              email: "jane@example.com"
              name: "Jane Doe"
              createdAt: "2024-01-15T10:30:00Z"
      "401":
        $ref: "#/components/responses/Unauthorized"
      "404":
        $ref: "#/components/responses/NotFound"
```

## Documentation Structure

```
[OVERVIEW]
- What the API does and who it is for
- Base URL(s) per environment
- Versioning strategy (URL path, header, or query param)

[AUTHENTICATION]
- Auth method (API key, OAuth 2.0, JWT)
- How to obtain credentials
- How to send credentials (header, query param)
- Token expiration and refresh procedure

[RATE LIMITING]
- Limits per plan or tier
- Rate limit response headers
- Retry strategy (exponential backoff with jitter)

[ERRORS]
- Standard error response format
- Complete list of error codes and their meaning
- Troubleshooting common errors

[ENDPOINTS]
For each endpoint:
- Method and path
- Summary and description
- Request parameters (path, query, header, body)
- Request body schema with all fields documented
- Response codes and schemas
- Working code example (curl, minimum one SDK)

[CHANGELOG / API VERSIONING]
- Breaking vs. non-breaking changes
- Deprecation policy and timeline
- Migration guides for version upgrades

[SDKS AND CLIENT LIBRARIES]
- Official SDK links
- Community SDK links
- Quickstart guides
```

## Guidelines

- Every field in every schema must have: type, description, whether required, and an example value.
- Document the null/empty behavior explicitly: "Returns null if not set" vs. "Field omitted from response if not set."
- Error responses must be documented with the same rigor as success responses.
- Authentication: include a working, copy-paste-ready curl command in the auth section.
- Pagination: document the pagination strategy (cursor, offset, page) with examples of first page, next page, and last page.
- Webhooks: document payload schema, signature verification, retry logic, and idempotency.
- Keep examples realistic — use plausible fake data, not `foo`, `bar`, `test123`.
- Provide a Postman collection or Insomnia workspace as a downloadable artifact.

## Error Response Standard

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The 'email' field is required and must be a valid email address.",
    "details": [
      {
        "field": "email",
        "issue": "required",
        "value": null
      }
    ],
    "requestId": "req_7f3a9b2c1d",
    "docsUrl": "https://docs.example.com/errors/VALIDATION_ERROR"
  }
}
```

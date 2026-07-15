---
schema-version: 1.1.0
document-version: 0
---

# Endpoint contracts

<!-- Grouped by resource.
     Record only DEVIATIONS from conventions.md - never repeat shared rules.
     Field constraints ARE the contract:
     state them on the fields, with the validation-failure problem type.
     Replace every <...> and example block; repeat the endpoint block per endpoint.
     Delete guidance comments when done. -->

## <Resource>

### <METHOD> <path>

<one-line purpose> (implements: <requirements operation name>)

- **Auth**: <required scopes; object-ownership check if any>
- **Request**
  - Path/query parameters:

    | Parameter | Type | Constraints | Required |
    |-----------|------|-------------|----------|
    | <name> | <type> | <format/range/enum> | <yes/no> |

  - Body:

    | Field | Type | Constraints | Required |
    |-------|------|-------------|----------|
    | <name> | <type> | <format/range/enum> | <yes/no> |

- **Responses**

  | Status | Body | When |
  |--------|------|------|
  | <2xx> | <schema summary or table ref> | <success condition> |
  | <4xx/5xx> | <problem type (conventions error catalog)> | <condition> |

- **Guarantees** *(deviations/refinements only)*: <idempotency / If-Match required / cache class / consistency-atomicity notes - e.g. "write and event publish are not atomic; see sequences: <flow>">

- **Example**

  ```http
  <one request/response pair; do not duplicate schema details>
  ```

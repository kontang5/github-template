# Feature Specification

Version: [e.g., 0.0.1]  
Last Updated: [YYYY-MM-DD]

## Tech Stack

- [Framework/Library - e.g., Spring Boot 3.5.6]
- [Database - e.g., PostgreSQL 18]
- [Other tech]

## Table of Contents

1. [Feature Name 1](#feature-name-1)
2. [Feature Name 2](#feature-name-2)

---

## [Feature Name]

### Data Model

| Field            | Type        | Description                            |
|------------------|-------------|----------------------------------------|
| `id`             | `BIGINT`    | Primary key (auto-generated)           |
| `[fieldName]`    | `[TYPE]`    | [Description]                          |
| `[fieldName]`    | `[TYPE]`    | [Description]                          |
| `isActive`       | `BOOLEAN`   | Whether the record is currently active |
| `createdBy`      | `BIGINT`    | User ID who created this record        |
| `createdAt`      | `TIMESTAMP` | Record creation timestamp              |
| `lastModifiedBy` | `BIGINT`    | User ID who last modified this record  |
| `lastModifiedAt` | `TIMESTAMP` | Last modification timestamp            |

### Business Rules

| # | Rule                  | Description                                         |
|---|-----------------------|-----------------------------------------------------|
| 1 | **[Rule Name]**       | [Detailed description of the business rule]         |
| 2 | **[Rule Name]**       | [Detailed description of the business rule]         |
| 3 | **Unique Constraint** | [Describe what must be unique]                      |
| 4 | **Auditability**      | All operations must store created/modified metadata |
| 5 | **Integrity**         | [Describe referential integrity rules]              |
| 6 | **Authorization**     | [Describe who can access/modify this feature]       |

### Business Logic

- **Create [Entity]**
    - [Who can perform this action]
    - [What happens during creation]
    - [Validation rules]
    - [Constraints to check]

- **Read [Entity]**
    - [Who can view what]
    - [Filtering rules]
    - [Default sorting]

- **Update [Entity]**
    - [Who can perform this action]
    - [What can be updated]
    - [What cannot be updated]
    - [Validation rules]

- **Delete [Entity]**
    - [Who can perform this action]
    - [Hard or soft delete?]
    - [Constraints to check before deletion]

- **[Custom Operation]**
    - [Who can perform this action]
    - [What it does]
    - [Special rules]

### API Endpoints

**Base URL:** `/api/v1/[resource]`

| Method | Endpoint           | Description               | Auth   | Request Body           |
|--------|--------------------|---------------------------|--------|------------------------|
| POST   | `/[resource]`      | Create a new [entity]     | [ROLE] | `{ "field": "value" }` |
| GET    | `/[resource]`      | Get all [entities]        | [ROLE] | -                      |
| GET    | `/[resource]/{id}` | Get [entity] by ID        | [ROLE] | -                      |
| PUT    | `/[resource]/{id}` | Update [entity]           | [ROLE] | `{ "field": "value" }` |
| PATCH  | `/[resource]/{id}` | Partially update [entity] | [ROLE] | `{ "field": "value" }` |
| DELETE | `/[resource]/{id}` | Delete [entity]           | [ROLE] | -                      |

> [!NOTE]
> [Add any important notes about pagination, filtering, or special behavior]

#### Query Parameters (if applicable)

| Parameter  | Type     | Required | Description              | Default | Example          |
|------------|----------|----------|--------------------------|---------|------------------|
| `page`     | `int`    | No       | Page number (0-indexed)  | 0       | `?page=0`        |
| `size`     | `int`    | No       | Number of items per page | 20      | `?size=50`       |
| `sort`     | `string` | No       | Sort field and direction | -       | `?sort=name,asc` |
| `[filter]` | `[type]` | No       | [Filter description]     | -       | `?status=active` |

#### Response Codes

| Code | Description                                |
|------|--------------------------------------------|
| 200  | Success (GET, PUT, PATCH)                  |
| 201  | Created (POST)                             |
| 204  | No Content (DELETE)                        |
| 400  | Bad Request (validation failed)            |
| 401  | Unauthorized                               |
| 403  | Forbidden (insufficient permissions)       |
| 404  | Not Found                                  |
| 409  | Conflict (duplicate, constraint violation) |
| 500  | Internal Server Error                      |

### Validation

| Field     | Rule     | Value                   | Error Message                                 |
|-----------|----------|-------------------------|-----------------------------------------------|
| `[field]` | Required | Cannot be null or blank | "[field] is required."                        |
| `[field]` | Length   | [min]-[max] characters  | "[field] must be between X and Y characters." |
| `[field]` | Format   | [Pattern description]   | "[field] must match [format description]."    |
| `[field]` | Range    | [min]-[max]             | "[field] must be between X and Y."            |
| `[field]` | Enum     | [Valid values]          | "[field] must be one of: [valid values]."     |

**Additional Validation Rules:**

- [Describe complex validation logic]
- [Cross-field validation]
- [Business rule validation]

### Exceptions

```
exception/
├── GlobalExceptionHandler
└── [Feature]Exception
    ├── [Specific]Exception
    ├── [Specific]Exception
    └── [Specific]Exception
```

| Exception             | HTTP Status | Error Code         | When It Occurs                 | Example Client Message         |
|-----------------------|-------------|--------------------|--------------------------------|--------------------------------|
| `[Specific]Exception` | [Code]      | `[ERROR_CODE]`     | [When this happens]            | "[User-friendly message]"      |
| `[Specific]Exception` | [Code]      | `[ERROR_CODE]`     | [When this happens]            | "[User-friendly message]"      |
| `[Feature]Exception`  | 400         | `{AUTO_GENERATED}` | Other [feature]-related errors | Varies by specific error       |
| `GenericException`    | 500         | `INTERNAL_ERROR`   | Fallback exception             | "An unexpected error occurred" |

> [!NOTE]  
> [Add notes about error handling strategy]

### Initial Data (if applicable)

| id | [field] | [field] | [field] | isActive |
|----|---------|---------|---------|----------|
| 1  | [value] | [value] | [value] | true     |
| 2  | [value] | [value] | [value] | true     |

### Database Indexes (if needed)

| Index Name              | Columns                | Type  | Purpose                    |
|-------------------------|------------------------|-------|----------------------------|
| `idx_[table]_[field]`   | `[field]`              | BTREE | [Why this index is needed] |
| `idx_[table]_composite` | `[field1]`, `[field2]` | BTREE | [Why this index is needed] |

### Performance Considerations

- [Consideration 1 - e.g., "Expected QPS: 100 reads, 10 writes"]
- [Consideration 2 - e.g., "Caching strategy for frequently accessed data"]
- [Consideration 3 - e.g., "Query optimization for list endpoints"]

### Security Considerations

- [Consideration 1 - e.g., "Authorization enforcement at service layer"]
- [Consideration 2 - e.g., "Input sanitization for XSS prevention"]
- [Consideration 3 - e.g., "Rate limiting for API endpoints"]

### Dependencies

**Internal:**

- [Depends on Feature X for Y]
- [Uses Service Z for functionality]

**External:**

- [Third-party API/Library]
- [External service integration]

### Testing Strategy

**Unit Tests:**

- [ ] [Test scenario 1]
- [ ] [Test scenario 2]
- [ ] Validation rules
- [ ] Exception handling

**Integration Tests:**

- [ ] [API endpoint test 1]
- [ ] [API endpoint test 2]
- [ ] Database operations
- [ ] Authentication/Authorization

**Edge Cases:**

- [ ] [Edge case 1]
- [ ] [Edge case 2]
- [ ] Concurrent operations
- [ ] Large data sets

## TODO

### v[X.X.X] (Current Release)

- [ ] [Task 1 - e.g., "Implement entity with JPA auditing"]
- [ ] [Task 2 - e.g., "Create repository with custom queries"]
- [ ] [Task 3 - e.g., "Implement service layer"]
- [ ] [Task 4 - e.g., "Add validation"]
- [ ] [Task 5 - e.g., "Write unit tests"]
- [ ] [Task 6 - e.g., "Add integration tests"]
- [ ] [Task 7 - e.g., "Create database migration scripts"]
- [ ] [Task 8 - e.g., "Seed initial data"]

### v[X+1.X.X] (Next Release)

- [ ] [Future enhancement 1]
- [ ] [Future enhancement 2]

### Future Considerations

- [ ] [Long-term improvement 1]
- [ ] [Long-term improvement 2]

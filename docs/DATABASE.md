# Database Schema

Version: [e.g., 0.0.1]  
Last Updated: [YYYY-MM-DD]

## Overview

JPA-centric database schema with version control using Flyway.

- **Database:** [e.g., PostgreSQL 18]
- **Database Name:** [e.g., your_db_name]
- **Schema:** [e.g., public (default)]
- **Migration Tool:** Flyway
- **ORM:** JPA/Hibernate

## Database Roles

| Role                | Purpose             | Usage                          |
|---------------------|---------------------|--------------------------------|
| `[prefix]_admin`    | Schema management   | Flyway migrations, DDL changes |
| `[prefix]_app`      | Application runtime | CRUD operations                |
| `[prefix]_readonly` | Read-only queries   | Analytics, reports, monitoring |

> [!NOTE]
> Follow principle of least privilege - application should not have DDL permissions

## Tables Overview

| Table          | Purpose             | Key Relationships    |
|----------------|---------------------|----------------------|
| `[table_name]` | [Brief description] | → [related_table]    |
| `[table_name]` | [Brief description] | ← [related_table]    |
| `[table_name]` | [Brief description] | → [table1], [table2] |

> [!NOTE]
> Detailed schema defined in JPA entities and Flyway migrations

## Naming Conventions

### Tables

- **Format:** plural, lowercase (e.g., `users`, `products`)
- **Junction tables:** `[table1]_[table2]` (e.g., `users_roles`)

### Columns

- **JPA Entity:** camelCase (e.g., `createdAt`)
- **Database:** snake_case (e.g., `created_at`)
- **Foreign keys:** `[table]_id` (e.g., `user_id`)

### Constraints

- **Primary key:** `pk_[table]`
- **Foreign key:** `fk_[table1]_[table2]`
- **Unique:** `uk_[table]_[column]`
- **Check:** `ck_[table]_[condition]`
- **Index:** `idx_[table]_[column(s)]`

## Standard Columns

All tables include these audit columns:

| Column             | Type        | Description                    |
|--------------------|-------------|--------------------------------|
| `id`               | `BIGINT`    | Primary key (auto-generated)   |
| `created_by`       | `BIGINT`    | User ID who created the record |
| `created_at`       | `TIMESTAMP` | Record creation timestamp      |
| `last_modified_by` | `BIGINT`    | User ID who last modified      |
| `last_modified_at` | `TIMESTAMP` | Last modification timestamp    |

### Soft Delete Pattern (when applicable)

| Column      | Type      | Description                     |
|-------------|-----------|---------------------------------|
| `is_active` | `BOOLEAN` | `false` indicates soft deletion |

> [!NOTE]
> Use soft delete for data that requires audit trail or may need recovery

## Indexes Strategy

### Default Indexes

- Primary keys: Automatically indexed
- Foreign keys: Indexed by default for join performance
- Unique constraints: Automatically create unique indexes

### Custom Indexes

- Added as needed based on query patterns
- Document in migration files
- Monitor slow query logs to identify needs

## Database Migrations

**Tool:** Flyway for database schema versioning and migration management.

### Migration File Naming

**Format:** `V[VERSION]__[DESCRIPTION].sql`

**Examples:**

- `V1__Create_users_table.sql`
- `V2__Add_email_to_users.sql`

**Rules:**

- Version numbers must be sequential
- Use double underscore `__` between version and description
- Description uses underscore for spaces
- Use descriptive names (verb + object)

### Migration Best Practices

- ✅ One logical change per migration
- ✅ Test migrations on local DB first
- ✅ Include both UP and DOWN logic when possible
- ✅ Never modify existing migrations once deployed
- ✅ Use repeatable migrations for views/procedures
- ❌ Don't drop columns immediately (deprecate first)
- ❌ Don't rename columns directly (create new + migrate data)

### Migration History

| Version | Description                | Date       | Author |
|---------|----------------------------|------------|--------|
| V1      | [e.g., Create roles table] | YYYY-MM-DD | [Name] |
| V2      | [e.g., Create users table] | YYYY-MM-DD | [Name] |

> [!TIP]
> Use `flyway info` to see migration status  
> Use `flyway validate` before deployment

## Performance Monitoring

### Key Metrics to Track

- [ ] Query execution time (slow query log)
- [ ] Connection pool usage
- [ ] Table sizes and growth rate
- [ ] Index usage statistics
- [ ] Cache hit ratio

### Tools

- `pg_stat_statements`: Track query performance
- `EXPLAIN ANALYZE`: Analyze query plans
- `pg_stat_user_tables`: Monitor table statistics

## Security

### Access Control

- Application connects with `[prefix]_app` role
- Migrations run with `[prefix]_admin` role
- Read-only access via `[prefix]_readonly` role

### Data Protection

- [ ] SSL/TLS encryption in transit
- [ ] Encryption at rest (if required)
- [ ] Regular security patches
- [ ] Password rotation policy

### Sensitive Data

- [ ] PII (Personally Identifiable Information) identified
- [ ] Encryption strategy for sensitive columns
- [ ] Data retention policy defined
- [ ] Compliance requirements (GDPR, etc.)

## Development Workflow

### Local Development

1. **Start PostgreSQL:**
   ```bash
   docker run -d \
     --name postgres-dev \
     -e POSTGRES_DB=[db_name] \
     -e POSTGRES_USER=[user] \
     -e POSTGRES_PASSWORD=[password] \
     -p 5432:5432 \
     postgres:18
   ```

2. **Run Flyway migrations:**
   ```bash
   ./gradlew flywayMigrate
   ```

3. **Verify schema:**
   ```bash
   ./mvnw flyway:info
   ```

### Adding New Tables

1. Create JPA Entity
2. Write Flyway migration script
3. Test migration on local DB
4. Update this document (Tables Overview)
5. Commit both entity and migration together
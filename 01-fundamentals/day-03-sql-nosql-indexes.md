# Day 3 — SQL vs NoSQL, Schemas, and Indexes

## Goal
Understand how to choose a data store, how relational tables are connected, and why indexes matter.

## Why use a database?
A database provides persistent storage and query capabilities. For example, a student system might store student IDs, names, emails, departments, and CGPAs.

## SQL / relational databases
Relational databases organize data into tables with rows and columns. Tables can be connected using keys, and SQL is used to define, query, and modify data.

Examples include PostgreSQL and MySQL.

A simple schema:

```sql
CREATE TABLE Students (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE,
    department_id INT,
    cgpa DECIMAL(3, 2)
);
```

## NoSQL / non-relational databases
NoSQL is a broad category that includes document, key-value, wide-column, and graph databases. Data models and guarantees vary by product; NoSQL does not simply mean “no schema.”

Example document in a document database:

```json
{
  "id": 101,
  "name": "Ravi",
  "department": "CSE",
  "cgpa": 8.5
}
```

## SQL vs NoSQL: choosing thoughtfully

| Requirement | A reasonable starting point | Why |
|---|---|---|
| Orders, payments, inventory with related records | Relational SQL database | Relationships, constraints, and transactions are useful |
| Documents with varied fields | Document database may fit | Flexible document model |
| Low-latency cache or temporary lookup data | In-memory key-value store such as Redis | Fast access for suitable workloads |
| Large write-heavy workload with specific partitioning needs | Evaluate databases designed for that workload | Access patterns and scaling requirements matter |

There is no universal winner. Consider relationships, query patterns, consistency, transaction needs, data volume, availability, operational complexity, and cost. Real systems often use multiple storage technologies for different purposes.

## Schema, primary key, and foreign key
A schema describes the structure of data and constraints.

- **Primary key:** uniquely identifies a row.
- **Foreign key:** references a key in another table and helps enforce a relationship.
- **Unique constraint:** prevents duplicate values in the constrained column or column set.
- **Data type:** defines what values a column can hold.

Example relationship:

```sql
CREATE TABLE Departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);

CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT REFERENCES Departments(department_id)
);
```

The department is stored once and referenced by each student, rather than repeating all department details in every student record.

## What is a database index?
An index is an additional data structure that can help the database find rows without scanning the entire table. The actual benefit depends on the query, data distribution, and database query planner.

Example:

```sql
CREATE INDEX idx_students_email ON Students(email);

SELECT *
FROM Students
WHERE email = 'ravi@example.com';
```

### Index trade-offs
- Can speed up suitable filters, joins, and sorts.
- Uses additional storage.
- Adds work to inserts, updates, and deletes because the index must be maintained.
- Too many or poorly chosen indexes can hurt performance.
- Check query plans and measure performance rather than indexing every column.

## Example: an online store
A store might use:
- SQL for customers, orders, payments, and inventory.
- Redis for caching frequently requested product information.
- Object storage for product images.

This is one possible design, not a universal requirement.

## Key takeaways
- Choose storage based on access patterns and guarantees, not hype.
- SQL databases are relational; NoSQL covers several different data models.
- Primary and foreign keys model identity and relationships.
- Indexes can improve reads but have storage and write costs.

## Practice
1. Explain why a relational database is a sensible starting point for orders and payments.
2. Define primary key and foreign key in your own words.
3. What trade-offs come with adding an index?
4. Explain why an application might use SQL for orders and Redis for caching.

## Quick check
**Question:** Does an index always make every database operation faster?

**Answer:** No. It can improve suitable reads, but it consumes storage and can add overhead to writes.

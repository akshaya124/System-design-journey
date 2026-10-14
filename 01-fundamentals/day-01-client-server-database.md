# Day 1 — Client, Server, and Database

## Goal
Understand the basic components that make up many applications and how they communicate.

## What is system design?
System design is the process of deciding how an application’s components fit together to meet functional and non-functional requirements. It includes choices about components, data, communication, reliability, performance, and trade-offs.

## The three basic building blocks

### 1. Client
The client is the application or device that initiates a request, such as a web browser, mobile app, or desktop application. It displays information and collects user input.

### 2. Server
The server receives requests, applies business rules, coordinates work, and sends responses. For example, it can validate a user’s input and decide whether an order can be placed.

### 3. Database and storage
A database stores structured or semi-structured application data persistently. Files and object storage are often used for images, videos, and other large files.

## Example: uploading a photo

1. The user selects a photo in the client.
2. The client sends an upload request to the backend.
3. The backend authenticates the user and validates the request.
4. The image is stored in file/object storage.
5. Metadata such as the owner, storage key, and upload time is saved in a database.
6. The server returns a response to the client.

This is a simplified flow. Real applications may also use queues, content delivery networks (CDNs), scanning services, and background workers.

## Architecture sketch

```text
+----------------+       HTTP request       +----------------+
| Client         | -----------------------> | Backend server |
| Browser / App  | <----------------------- | Business logic |
+----------------+       HTTP response      +-------+--------+
                                                    |
                                             reads / writes
                                                    |
                                            +-------v--------+
                                            | Database and   |
                                            | file storage   |
                                            +----------------+
```

## LLD vs HLD

- **Low-Level Design (LLD):** the internal structure of code—classes, interfaces, responsibilities, and their relationships.
- **High-Level Design (HLD):** the overall architecture—services, databases, communication, scaling, and reliability.

## Key takeaways
- The client initiates requests; the server processes them.
- Persistent data belongs in suitable storage, not only in temporary application variables.
- A backend usually mediates access to the database.
- The simplest architecture is a starting point; requirements determine when more components are needed.

## Practice
1. Draw the architecture of a student portal.
2. Identify what belongs in the client, backend, and database.
3. Explain in your own words the difference between LLD and HLD.

## Quick check
**Question:** Where should student records be stored so they remain available after the application restarts?

**Answer:** In persistent storage, commonly a database.

# Day 2 — HTTP, APIs, Requests, and Responses

## Goal
Understand how a client communicates with a backend and how HTTP methods describe operations.

## Client-server communication
A frontend might be built with HTML, CSS, and JavaScript/React. It sends HTTP requests to backend endpoints. The backend validates input, applies business logic, accesses data when needed, and sends an HTTP response.

```text
Browser / Mobile App
        |
        | HTTP request
        v
    Backend API
        |
        | query / update
        v
     Database
        |
        v
    Backend API
        |
        | HTTP response (status + body)
        v
Browser / Mobile App
```

## What is an API?
An Application Programming Interface (API) defines how software components can interact. A web API exposes operations through endpoints.

Example endpoints:
- `GET /products` — retrieve products
- `GET /products/10` — retrieve product 10
- `POST /products` — submit details to create a product
- `PUT /products/10` — replace product 10
- `PATCH /products/10` — update selected fields
- `DELETE /products/10` — delete product 10

These are illustrative endpoints; actual behavior depends on the API contract.

## Common HTTP methods

| Method | Typical purpose | Example |
|---|---|---|
| GET | Retrieve a resource | List products |
| POST | Submit data; often create a resource or trigger an operation | Create a product |
| PUT | Replace a resource representation | Replace product details |
| PATCH | Partially update a resource | Change a product price |
| DELETE | Remove a resource | Delete a product |

GET should be safe: it should not request a change to server state. PUT and DELETE are defined as idempotent in HTTP semantics; POST is not generally idempotent. Real APIs should document their behavior.

## Example: GET request

```http
GET /products HTTP/1.1
Host: example.com
Accept: application/json
```

Possible response body:

```json
[
  { "id": 1, "name": "Laptop", "price": 50000 },
  { "id": 2, "name": "Mouse", "price": 500 }
]
```

## Example: POST request

```http
POST /products HTTP/1.1
Host: example.com
Content-Type: application/json
```

Request body:

```json
{
  "name": "Keyboard",
  "price": 1500
}
```

If creation succeeds, the server commonly responds with `201 Created`, potentially including the created resource or its location.

## Useful HTTP status codes

| Code | Meaning |
|---|---|
| 200 | Request succeeded |
| 201 | Resource created |
| 204 | Request succeeded with no response body |
| 400 | Invalid request |
| 401 | Authentication is missing or invalid |
| 403 | Request understood, but access is forbidden |
| 404 | Resource not found |
| 500 | Unexpected server error |

## JSON
JSON is a common text format for exchanging structured data between clients and servers. It supports objects, arrays, strings, numbers, booleans, and null.

## Try a public test API
Open [JSONPlaceholder — sample post](https://jsonplaceholder.typicode.com/posts/1) in a browser, or send a GET request to it using Postman. It is a testing service, not your own backend.

## Key takeaways
- An API is a contract/interface; an endpoint is a particular address for an operation.
- HTTP methods communicate the intended operation.
- A response includes a status code and may include headers and a body.
- Authentication and authorization are different: authentication checks identity; authorization checks permissions.

## Practice
1. Write a GET example for listing students.
2. Write a POST example for registering a student.
3. Explain the difference between 401 and 403.
4. Draw the request and response paths between a browser, backend, and database.

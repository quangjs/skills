## 1. REST Architectural Principles

**RE**presentational **S**tate **T**ransfer is an architectural style, not a protocol.

* **Statelessness:** The server does not store any client context between requests. Each request from the client must contain all the information necessary to understand and complete the request (e.g., an Auth token).
* *Benefit:* Enhances **scalability** because any server can handle any request.


* **Resource-Based:** Everything is a resource (User, Order, Product), identified by **URIs** (Uniform Resource Identifiers). Use nouns, not verbs (e.g., `/users` instead of `/getAllUsers`).
* **Uniform Interface:** A standardized way of interacting with the server, regardless of the device or application. This includes using standard HTTP methods and media types (JSON/XML).

---

## 2. HTTP Methods & Semantics

You must distinguish between **Idempotency** and **Safety**.

| Method | Goal | Idempotent | Safe |
| --- | --- | --- | --- |
| **GET** | Retrieve a resource. | **Yes** | **Yes** |
| **POST** | Create a new resource. | **No** | **No** |
| **PUT** | Replace/Update a resource (Full). | **Yes** | **No** |
| **PATCH** | Update a resource (Partial). | **No** | **No** |
| **DELETE** | Remove a resource. | **Yes** | **No** |

> **Interview Tip:** If asked why **PUT** is idempotent and **POST** is not: "Calling PUT with the same payload multiple times results in the same state on the server. Calling POST multiple times results in multiple duplicate resources being created."

---

## 3. Standard HTTP Status Codes

* **2xx (Success)**
* `200 OK`: Request succeeded.
* `201 Created`: Resource created (usually after POST).
* `204 No Content`: Success, but nothing to return (common for DELETE).


* **4xx (Client Errors)**
* `400 Bad Request`: Invalid syntax/malformed request.
* `401 Unauthorized`: Authentication is required (Identity is missing).
* `403 Forbidden`: Authenticated but lacks permission (Identity is known, but no rights).
* `404 Not Found`: Resource does not exist.
* `409 Conflict`: Conflict with the current state (e.g., duplicate username).
* `422 Unprocessable Entity`: Semantic errors (e.g., validation failed).


* **5xx (Server Errors)**
* `500 Internal Server Error`: Generic "something went wrong" on the server.



---

## 4. Advanced API Design

### Versioning

* **URI Versioning:** `/v1/products` (Easy to route, transparent).
* **Header Versioning:** `Accept: application/vnd.api.v1+json` (Cleaner URLs, follows REST "Content Negotiation" principles).

### Pagination, Filtering, & Sorting

* **Offset Pagination:** `?limit=20&offset=100`. Easy but slow for deep pages in large DBs.
* **Cursor Pagination:** `?after=XYZ`. More performant for real-time data (e.g., social media feeds).
* **Filtering/Sorting:** Use query params: `/orders?status=shipped&sort=-price`.

---

## 5. Security: Auth & Rate Limiting

### Authentication vs. Authorization

* **Authentication (AuthN):** "Who are you?" (Checking credentials).
* **Authorization (AuthZ):** "What are you allowed to do?" (Checking permissions/roles).

### JWT & OAuth2

* **JWT (JSON Web Token):** A stateless token containing claims.
* *Structure:* Header, Payload, Signature.


* **Refresh Token:** A long-lived token used to obtain a new short-lived **Access Token** without requiring the user to re-login.
* **OAuth2:** An authorization framework that allows applications to obtain limited access to user accounts (e.g., "Login with Google").

### Rate Limiting & Throttling

* **Rate Limiting:** Restricts the number of requests a user can make in a timeframe (e.g., 100 requests/minute).
* **Throttling:** Slows down the response if a user exceeds the limit to prevent server crashes.

---

## 6. API Documentation (OpenAPI/Swagger)

* **OpenAPI:** The industry-standard **specification** for describing REST APIs.
* **Swagger:** The **tooling** (UI, Editor) used to implement the OpenAPI spec.
* *Why use it?* It provides "Interactive Documentation" where developers can test endpoints without writing code.

---

### Potential Interview Questions to Practice:

1. "Explain the difference between 401 and 403 errors."
2. "Why should we prefer PATCH over PUT for updating a single field?"
3. "How do you handle a scenario where a user makes 1,000 requests per second?"
4. "What are the pros and cons of JWT being stateless?"

**Would you like me to provide a "Mock Answer" for any of these specific questions?**
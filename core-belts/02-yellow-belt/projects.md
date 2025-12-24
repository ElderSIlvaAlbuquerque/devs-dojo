# 💛 Yellow Belt - Capstone Projects

Pick ONE project to graduate to the Orange Belt. These projects build on your White Belt API by adding layers of professionalism: validation, automated testing, and better data management.

## Project 1: Todo API with Validation & Testing
**Time**: 1-2 weeks
**Tech Stack**: Your language of choice (Go, Python, Ruby, Node.js, etc.) + PostgreSQL/MySQL
**Concepts**: API Validation, Integration Testing, Database Migrations, CI/CD

**Description**:
Take a simple CRUD API (like the one from the White Belt) and make it robust. The focus here is not on new features, but on reliability.

**Requirements**:
- [ ] **API Endpoints**: Full CRUD for "Todo" items (`GET`, `POST`, `PUT`, `DELETE`).
- [ ] **Input Validation**: `POST` and `PUT` endpoints must validate input. A `title` must be present and non-empty. Invalid requests must return a `400 Bad Request` with a clear error message.
- [ ] **Database Migrations**: Use a migration tool to create and manage your `todos` table schema. You must have at least two migrations: one to create the table, and a second one to add a `due_date` column.
- [ ] **Integration Tests**: Write integration tests for every endpoint. The test suite must connect to a real test database, and each test should clean up after itself. You must have tests for both "happy path" (correct input) and "sad path" (incorrect input).
- [ ] **CI/CD Pipeline**: Create a GitHub Actions (or similar) pipeline that automatically runs your full integration test suite on every push to a pull request. Merging must be blocked if tests fail.
- [ ] **Structured Logging**: Implement structured logging (e.g., JSON format) for all requests, including a unique `request_id` for tracing.

---

## Project 2: User Authentication System
**Time**: 2-3 weeks
**Tech Stack**: Your language of choice + PostgreSQL/MySQL + a JWT library
**Concepts**: API Security, Hashing, JWT, Database Migrations, Integration Testing

**Description**:
Build the core of most web applications: a system for users to sign up and log in. This project forces you to handle passwords securely and manage user sessions.

**Requirements**:
- [ ] **API Endpoints**:
    - `POST /signup`: Accepts `email` and `password`, creates a new user.
    - `POST /login`: Accepts `email` and `password`, returns a JWT if valid.
    - `GET /me`: A protected endpoint that requires a valid JWT. It returns the current user's information.
- [ ] **Password Security**: Passwords must be hashed using a strong, salted algorithm (e.g., bcrypt, Argon2). **Never store plain-text passwords.**
- [ ] **JWT Generation**: On successful login, generate a JSON Web Token (JWT) containing the user's ID. The token must have an expiration date.
- [ ] **Middleware/Authentication**: Implement a middleware that checks for a valid JWT on protected routes like `/me`. If the token is missing, expired, or invalid, it must return a `401 Unauthorized` or `403 Forbidden` error.
- [ ] **Database Migrations**: Use a migration tool to create the `users` table, including `email` and `hashed_password` columns. Ensure the `email` column has a unique constraint.
- [ ] **Integration Tests**: Write integration tests for the full flow: signup, login, and accessing a protected route with the token. Also test failure cases: wrong password, invalid token, etc.

---

## Submission
- [ ] Code is available on a public GitHub repository.
- [ ] The `README.md` file contains:
    - Clear, step-by-step setup instructions.
    - API documentation explaining each endpoint, the expected request body, and the possible responses (like an API contract).
- [ ] A live, deployed version is NOT required, but the CI/CD pipeline MUST pass.
- [ ] Pass all items on the Yellow Belt promotion checklist.

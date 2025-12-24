# 💛 Yellow Belt - Lessons

## What You'll Learn
- [ ] API design best practices (error handling, validation, contracts)
- [ ] Database migrations and schema design
- [ ] Integration testing (with database, external APIs)
- [ ] CI/CD basics (GitHub Actions, automated tests)
- [ ] Logging and debugging (structured logs, tracing IDs)

## Core Ideas
1. **API Contracts**: An API is a promise. Your contract (the spec, like OpenAPI) tells consumers what to expect. Good contracts include clear data formats, required fields, and predictable error responses.
    *   **Example**: A `POST /users` endpoint should return a `400 Bad Request` with a descriptive error message if the `email` field is missing, not a `500 Internal Server Error`.

2. **Database Migrations**: Your database schema will change. Migrations are version-controlled scripts that apply these changes incrementally and reversibly. This prevents data loss and ensures all environments (local, staging, production) are consistent.
    *   **Example**: A migration to add a `phone_number` column to the `users` table. A separate migration to make it `NOT NULL` after backfilling existing records.

3. **Integration Testing**: Unit tests check small components in isolation. Integration tests check that those components work *together*. This is where you test your API endpoint against a real (or test-container) database.
    *   **Example**: An integration test that calls `POST /users`, then queries the test database to verify the user was actually created.

4. **CI/CD Pipeline**: Continuous Integration/Continuous Deployment automates your testing and deployment process. On every `git push`, the pipeline should automatically run all tests. If they pass, it might deploy to a staging environment.
    *   **Example**: A GitHub Actions workflow that triggers on every pull request, runs `go test ./...`, and blocks merging if tests fail.

5. **Structured Logging**: Instead of printing "Error processing request", log a JSON object: `{"level": "error", "message": "Failed to process request", "trace_id": "xyz-123", "user_id": 42, "error": "database connection refused"}`. This makes logs searchable and filterable.

## Why This Matters
At the Yellow Belt level, you move from writing code that *works* to writing code that is *maintainable, reliable, and testable*. These concepts form the foundation of professional software engineering. Bad APIs, broken database changes, and untestable code cause outages and slow down teams.

## Common Mistakes
- **Putting business logic in migrations**: Migrations should only handle schema changes. Complex data backfills should happen in separate scripts or application code.
- **Ignoring error handling**: Assuming every request will be perfect. Always validate inputs and handle potential failures gracefully.
- **Testing implementation details**: Your integration tests should focus on the API's public contract (what goes in, what comes out), not how the code internally works.

## Further Reading
- [Google API Design Guide](https://cloud.google.com/apis/design/)
- [The Twelve-Factor App - III. Config](https://12factor.net/config)
- [Martin Fowler - "Integration Test"](https://martinfowler.com/bliki/IntegrationTest.html)

## 🥋 Promotion Requirements - Yellow Belt 💛

To advance to the Orange Belt, you must demonstrate a solid foundation in creating reliable and maintainable services. This means your code is not just functional, but also well-tested, predictable, and easy for others to understand.

### Knowledge & Understanding
- [ ] Can you explain the purpose of a database migration and why it's better than manually changing the database schema?
- [ ] Can you describe the difference between a unit test and an integration test? When would you use each?
- [ ] Can you explain what a "sad path" test is and why it's important?
- [ ] Can you explain what structured logging is and how it helps with debugging in a production environment?
- [ ] Can you describe what an API contract is and why it's important for teamwork?

### Project Implementation
- [ ] **Capstone Project Complete**: Your chosen capstone project is functionally complete and meets all specified requirements.
- [ ] **Input Validation**: The API correctly validates all user-provided input and returns clear `400 Bad Request` errors for invalid data.
- [ ] **Database Migrations**: The database schema is managed entirely by version-controlled migration files. There is a clear history of changes (e.g., initial creation, adding a column).
- [ ] **Comprehensive Integration Tests**: The project has a suite of integration tests covering every API endpoint. This includes:
    - [ ] At least one "happy path" test for each endpoint.
    - [ ] At least one "sad path" test for each endpoint that accepts input.
- [ ] **CI/CD Pipeline**: A Continuous Integration pipeline (e.g., GitHub Actions) is configured.
    - [ ] The pipeline automatically runs the full test suite on every `git push` to a pull request.
    - [ ] The pipeline status is clearly visible (passing or failing) on the pull request.
- [ ] **Structured Logging**: The application produces structured logs (e.g., JSON) for incoming requests, including a correlation ID to trace a request's lifecycle.
- [ ] **README Documentation**: The `README.md` is professional and clear.
    - [ ] It includes a section documenting the API contract (endpoints, request/response formats).
    - [ ] It provides clear, step-by-step instructions for setting up and running the project locally.

### Review
- [ ] **Peer Review**: Another person (a peer, mentor, or senior developer) has reviewed your code and confirmed it is readable and makes sense.
- [ ] **Self-Assessment**: You have reviewed your own code against the promotion requirements and believe it meets the standards.

**Final Check**: ✓ Once all items above are checked, you are ready for your promotion review.

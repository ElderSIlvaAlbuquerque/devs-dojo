## 💛 Daily Exercises - Yellow Belt

Duration: 15-25 min per exercise (pick 1-2 daily)

### Monday
- [ ] **API Design**: Design one API endpoint, including its path, verb, request body (with data types and validation rules), and possible response codes (e.g., 200, 201, 400, 404, 500). Write it down in a notebook or text file.
- [ ] **Logging**: Take a function you wrote for your White Belt project and add structured logging to it. Log key inputs and the final result.

### Tuesday
- [ ] **Integration Test**: Write one integration test for a CRUD endpoint from your White Belt project. It must interact with a real (test) database.
- [ ] **Database Migration**: Read the documentation for a migration tool in your language of choice (e.g., `go-migrate`, `Active Record Migrations`, `Alembic`).

### Wednesday
- [ ] **CI/CD**: Create a basic GitHub Actions workflow file (`.github/workflows/ci.yml`) that runs on every push and executes a simple command, like `echo "Hello, world!"`.
- [ ] **API Design**: Review a public API (like GitHub's or Stripe's). Find one endpoint and analyze its request/response structure. What do you like or dislike?

### Thursday
- [ ] **Integration Test**: Write a "sad path" integration test. Test what happens when you send invalid data to an endpoint. Does it return the correct 4xx error code and a useful error message?
- [ ] **Database Migration**: Write a migration to add a new, nullable column to a table from your White Belt project.

### Friday
- [ ] **Logging**: Add a unique request/trace ID to your API's context so you can follow a single request through multiple logs.
- [ ] **Review**: Read an article or blog post about API versioning strategies (e.g., path, header, query param).

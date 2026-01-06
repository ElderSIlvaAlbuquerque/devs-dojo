# Go - Orange Belt Lessons

## Lesson 1: Error Handling in Go

### What You'll Learn

- [ ] Go's error handling philosophy
- [ ] Creating and returning errors
- [ ] Error wrapping with fmt.Errorf
- [ ] errors.Is() and errors.As()
- [ ] Custom error types

### Core Ideas

#### 1. Errors are Values

```go
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

result, err := divide(10, 0)
if err != nil {
    log.Fatal(err)
}
```

#### 2. Error Wrapping

```go
func readConfig(filename string) (*Config, error) {
    data, err := os.ReadFile(filename)
    if err != nil {
        return nil, fmt.Errorf("read config: %w", err)
    }
    // Process data...
}
```

#### 3. Sentinel Errors

```go
var (
    ErrNotFound     = errors.New("not found")
    ErrUnauthorized = errors.New("unauthorized")
)

func getUser(id int) (*User, error) {
    // ...
    if !exists {
        return nil, ErrNotFound
    }
}

// Check error
if errors.Is(err, ErrNotFound) {
    // Handle not found
}
```

### Why This Matters

Explicit error handling makes code more reliable and easier to debug than exceptions.

---

## Lesson 2: Concurrency with Goroutines

### What You'll Learn

- [ ] Goroutines vs threads
- [ ] The go keyword
- [ ] sync.WaitGroup for coordination
- [ ] Common concurrency pitfalls
- [ ] Race conditions and sync.Mutex

### Core Ideas

#### 1. Launching Goroutines

```go
func main() {
    var wg sync.WaitGroup
    
    for i := 0; i < 3; i++ {
        wg.Add(1)
        go func(id int) {
            defer wg.Done()
            fmt.Printf("Worker %d\n", id)
        }(i)  // Pass i as parameter!
    }
    
    wg.Wait()
}
```

#### 2. Race Conditions

```go
// WRONG - race condition
var counter int
for i := 0; i < 1000; i++ {
    go func() {
        counter++  // Not safe!
    }()
}

// CORRECT - use mutex
var (
    counter int
    mu      sync.Mutex
)
for i := 0; i < 1000; i++ {
    go func() {
        mu.Lock()
        counter++
        mu.Unlock()
    }()
}
```

#### 3. Detecting Race Conditions

```bash
go run -race main.go
go test -race
```

### Why This Matters

Go's concurrency primitives enable writing efficient concurrent programs without managing threads.

---

## Lesson 3: Channels for Communication

### What You'll Learn

- [ ] Unbuffered vs buffered channels
- [ ] Sending and receiving
- [ ] Closing channels
- [ ] Range over channels
- [ ] Select statement

### Core Ideas

#### 1. Channel Basics

```go
// Unbuffered - synchronous
ch := make(chan int)

// Buffered - asynchronous up to capacity
ch := make(chan int, 10)

// Send
ch <- 42

// Receive
value := <-ch

// Close
close(ch)
```

#### 2. Select for Multiple Channels

```go
select {
case msg := <-ch1:
    fmt.Println("Received from ch1:", msg)
case msg := <-ch2:
    fmt.Println("Received from ch2:", msg)
case <-time.After(1 * time.Second):
    fmt.Println("Timeout")
default:
    fmt.Println("No activity")
}
```

#### 3. Pipeline Pattern

```go
func generator(nums ...int) <-chan int {
    out := make(chan int)
    go func() {
        for _, n := range nums {
            out <- n
        }
        close(out)
    }()
    return out
}

func square(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            out <- n * n
        }
        close(out)
    }()
    return out
}

// Usage
for n := range square(generator(1, 2, 3, 4)) {
    fmt.Println(n) // 1, 4, 9, 16
}
```

### Why This Matters

Channels provide a safe way to communicate between goroutines: "Don't communicate by sharing memory; share memory by communicating."

---

## Lesson 4: Context Package

### What You'll Learn

- [ ] Context for cancellation
- [ ] Context with timeout
- [ ] Context with deadline
- [ ] Context values (use sparingly)
- [ ] Context best practices

### Core Ideas

#### 1. Context Types

```go
// Background context (root)
ctx := context.Background()

// With cancellation
ctx, cancel := context.WithCancel(ctx)
defer cancel()

// With timeout
ctx, cancel := context.WithTimeout(ctx, 5*time.Second)
defer cancel()

// With deadline
deadline := time.Now().Add(10 * time.Second)
ctx, cancel := context.WithDeadline(ctx, deadline)
defer cancel()
```

#### 2. Using Context

```go
func doWork(ctx context.Context) error {
    for {
        select {
        case <-ctx.Done():
            return ctx.Err() // context.Canceled or context.DeadlineExceeded
        default:
            // Do work
            if err := processItem(); err != nil {
                return err
            }
        }
    }
}
```

#### 3. HTTP with Context

```go
func handler(w http.ResponseWriter, r *http.Request) {
    ctx := r.Context() // Request context
    
    // Pass to database query
    rows, err := db.QueryContext(ctx, "SELECT * FROM users")
    if err != nil {
        if ctx.Err() == context.Canceled {
            // Client disconnected
            return
        }
        // Handle other errors
    }
}
```

### Why This Matters

Context enables graceful cancellation and timeouts across API boundaries.

---

## Lesson 5: Testing in Go

### What You'll Learn

- [ ] Writing unit tests
- [ ] Table-driven tests
- [ ] Test helpers
- [ ] Benchmarks
- [ ] Test coverage

### Core Ideas

#### 1. Basic Test Structure

```go
// math.go
func Add(a, b int) int {
    return a + b
}

// math_test.go
func TestAdd(t *testing.T) {
    got := Add(2, 3)
    want := 5
    
    if got != want {
        t.Errorf("Add(2, 3) = %d; want %d", got, want)
    }
}
```

#### 2. Table-Driven Tests

```go
func TestAdd(t *testing.T) {
    tests := []struct {
        name   string
        a, b   int
        want   int
    }{
        {"positive", 2, 3, 5},
        {"negative", -1, -2, -3},
        {"zero", 0, 5, 5},
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            if got := Add(tt.a, tt.b); got != tt.want {
                t.Errorf("got %d, want %d", got, tt.want)
            }
        })
    }
}
```

#### 3. Benchmarks

```go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(2, 3)
    }
}

// Run: go test -bench=. -benchmem
```

### Why This Matters

Go's built-in testing framework encourages writing tests alongside code.

---

## Lesson 6: Working with JSON

### What You'll Learn

- [ ] JSON encoding (marshaling)
- [ ] JSON decoding (unmarshaling)
- [ ] Struct tags
- [ ] Custom marshal/unmarshal
- [ ] Streaming JSON

### Core Ideas

#### 1. Basic JSON Operations

```go
type User struct {
    ID        int    `json:"id"`
    Name      string `json:"name"`
    Email     string `json:"email,omitempty"`
    Password  string `json:"-"` // Never serialize
    CreatedAt time.Time `json:"created_at"`
}

// Marshal (Go -> JSON)
user := User{ID: 1, Name: "Alice"}
data, err := json.Marshal(user)

// Unmarshal (JSON -> Go)
var user User
err := json.Unmarshal(data, &user)
```

#### 2. Streaming JSON

```go
// Encode to writer
encoder := json.NewEncoder(w)
encoder.Encode(user)

// Decode from reader
decoder := json.NewDecoder(r.Body)
var user User
decoder.Decode(&user)
```

### Why This Matters

JSON is ubiquitous in web APIs and configuration files.

---

## Lesson 7: HTTP Servers and Clients

### What You'll Learn

- [ ] net/http package basics
- [ ] Handlers and ServeMux
- [ ] Middleware pattern
- [ ] HTTP client usage
- [ ] Request/Response handling

### Core Ideas

#### 1. Basic HTTP Server

```go
func helloHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, %s!", r.URL.Query().Get("name"))
}

func main() {
    http.HandleFunc("/hello", helloHandler)
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

#### 2. Middleware

```go
func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        log.Printf("%s %s", r.Method, r.URL.Path)
        next.ServeHTTP(w, r)
    })
}

mux := http.NewServeMux()
mux.HandleFunc("/", homeHandler)
http.ListenAndServe(":8080", loggingMiddleware(mux))
```

#### 3. HTTP Client

```go
client := &http.Client{
    Timeout: 10 * time.Second,
}

resp, err := client.Get("https://api.example.com/users")
if err != nil {
    log.Fatal(err)
}
defer resp.Body.Close()

var users []User
json.NewDecoder(resp.Body).Decode(&users)
```

### Why This Matters

Go's standard library provides a production-ready HTTP server and client.

---

## Lesson 8: Database Operations

### What You'll Learn

- [ ] database/sql package
- [ ] Connection pooling
- [ ] Prepared statements
- [ ] Transactions
- [ ] Handling NULL values

### Core Ideas

#### 1. Connecting to Database

```go
import (
    "database/sql"
    _ "github.com/lib/pq" // PostgreSQL driver
)

db, err := sql.Open("postgres", 
    "host=localhost user=postgres password=secret dbname=mydb")
if err != nil {
    log.Fatal(err)
}
defer db.Close()

// Test connection
if err := db.Ping(); err != nil {
    log.Fatal(err)
}
```

#### 2. Queries

```go
// Query multiple rows
rows, err := db.Query("SELECT id, name FROM users WHERE age > $1", 18)
if err != nil {
    log.Fatal(err)
}
defer rows.Close()

for rows.Next() {
    var id int
    var name string
    if err := rows.Scan(&id, &name); err != nil {
        log.Fatal(err)
    }
    fmt.Printf("%d: %s\n", id, name)
}

// Query single row
var name string
err = db.QueryRow("SELECT name FROM users WHERE id = $1", 1).Scan(&name)
```

#### 3. Transactions

```go
tx, err := db.Begin()
if err != nil {
    log.Fatal(err)
}

_, err = tx.Exec("INSERT INTO users (name) VALUES ($1)", "Alice")
if err != nil {
    tx.Rollback()
    log.Fatal(err)
}

if err = tx.Commit(); err != nil {
    log.Fatal(err)
}
```

### Why This Matters

database/sql provides a consistent interface for working with SQL databases.

---

These lessons prepare you for building production Go applications!

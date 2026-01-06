# Go Orange Belt - Daily Exercises

**Duration**: 20-30 minutes per exercise  
**Goal**: Build proficiency with Go's concurrency and standard library

---

## Week 1: Error Handling & Testing

### Monday

**Focus**: Idiomatic error handling

- [ ] **Exercise** (20 min): Error wrapping and unwrapping

  ```go
  package main
  
  import (
      "errors"
      "fmt"
  )
  
  var ErrNotFound = errors.New("not found")
  
  func fetchUser(id int) (string, error) {
      if id <= 0 {
          return "", fmt.Errorf("invalid id %d: %w", id, ErrNotFound)
      }
      return "User", nil
  }
  
  func main() {
      _, err := fetchUser(0)
      if err != nil {
          if errors.Is(err, ErrNotFound) {
              fmt.Println("User not found")
          }
          fmt.Printf("Error: %v\n", err)
      }
  }
  ```

### Tuesday

**Focus**: Table-driven tests

- [ ] **Exercise** (25 min): Write table-driven tests

  ```go
  func TestAdd(t *testing.T) {
      tests := []struct {
          name string
          a, b int
          want int
      }{
          {"positive numbers", 2, 3, 5},
          {"negative numbers", -1, -2, -3},
          {"mixed", -1, 5, 4},
          {"zeros", 0, 0, 0},
      }
      
      for _, tt := range tests {
          t.Run(tt.name, func(t *testing.T) {
              got := Add(tt.a, tt.b)
              if got != tt.want {
                  t.Errorf("Add(%d, %d) = %d; want %d", 
                      tt.a, tt.b, got, tt.want)
              }
          })
      }
  }
  ```

### Wednesday

**Focus**: Benchmarking

- [ ] **Exercise** (20 min): Write and run benchmarks

  ```go
  func BenchmarkFibonacci(b *testing.B) {
      for i := 0; i < b.N; i++ {
          Fibonacci(20)
      }
  }
  
  // Run: go test -bench=. -benchmem
  ```

### Thursday

**Focus**: Test coverage

- [ ] **Exercise** (25 min): Achieve >80% coverage
  - Write tests for all functions
  - Run `go test -cover`
  - Generate HTML coverage report: `go test -coverprofile=coverage.out && go tool cover -html=coverage.out`

### Friday

**Focus**: Mocking and interfaces

- [ ] **Exercise** (30 min): Test with mocks

  ```go
  type UserStore interface {
      GetUser(id int) (User, error)
  }
  
  type MockUserStore struct {
      users map[int]User
  }
  
  func (m *MockUserStore) GetUser(id int) (User, error) {
      user, ok := m.users[id]
      if !ok {
          return User{}, ErrNotFound
      }
      return user, nil
  }
  ```

---

## Week 2: Concurrency

### Monday

**Focus**: Goroutines basics

- [ ] **Exercise** (25 min): Launch multiple goroutines

  ```go
  func main() {
      var wg sync.WaitGroup
      
      for i := 0; i < 5; i++ {
          wg.Add(1)
          go func(id int) {
              defer wg.Done()
              fmt.Printf("Worker %d starting\n", id)
              time.Sleep(time.Second)
              fmt.Printf("Worker %d done\n", id)
          }(i)
      }
      
      wg.Wait()
      fmt.Println("All workers completed")
  }
  ```

### Tuesday

**Focus**: Channels

- [ ] **Exercise** (30 min): Channel communication

  ```go
  func main() {
      ch := make(chan int)
      
      // Producer
      go func() {
          for i := 0; i < 10; i++ {
              ch <- i
          }
          close(ch)
      }()
      
      // Consumer
      for num := range ch {
          fmt.Println(num)
      }
  }
  ```

### Wednesday

**Focus**: Select statement

- [ ] **Exercise** (30 min): Multiple channel operations

  ```go
  func main() {
      ch1 := make(chan string)
      ch2 := make(chan string)
      
      go func() {
          time.Sleep(1 * time.Second)
          ch1 <- "one"
      }()
      
      go func() {
          time.Sleep(2 * time.Second)
          ch2 <- "two"
      }()
      
      for i := 0; i < 2; i++ {
          select {
          case msg1 := <-ch1:
              fmt.Println("Received", msg1)
          case msg2 := <-ch2:
              fmt.Println("Received", msg2)
          case <-time.After(3 * time.Second):
              fmt.Println("Timeout")
          }
      }
  }
  ```

### Thursday

**Focus**: Worker pools

- [ ] **Exercise** (30 min): Implement worker pool

  ```go
  func worker(id int, jobs <-chan int, results chan<- int) {
      for j := range jobs {
          fmt.Printf("Worker %d processing job %d\n", id, j)
          time.Sleep(time.Second)
          results <- j * 2
      }
  }
  
  func main() {
      jobs := make(chan int, 100)
      results := make(chan int, 100)
      
      // Start 3 workers
      for w := 1; w <= 3; w++ {
          go worker(w, jobs, results)
      }
      
      // Send jobs
      for j := 1; j <= 9; j++ {
          jobs <- j
      }
      close(jobs)
      
      // Collect results
      for a := 1; a <= 9; a++ {
          <-results
      }
  }
  ```

### Friday

**Focus**: Context usage

- [ ] **Exercise** (30 min): Context for cancellation

  ```go
  func doWork(ctx context.Context) error {
      for {
          select {
          case <-ctx.Done():
              return ctx.Err()
          default:
              // Do work
              time.Sleep(100 * time.Millisecond)
              fmt.Println("Working...")
          }
      }
  }
  
  func main() {
      ctx, cancel := context.WithTimeout(
          context.Background(), 
          2*time.Second,
      )
      defer cancel()
      
      err := doWork(ctx)
      fmt.Printf("Finished: %v\n", err)
  }
  ```

---

## Week 3: HTTP & JSON

### Monday-Tuesday

**Focus**: HTTP server

- [ ] **Exercise** (45 min): Build REST API

  ```go
  func main() {
      http.HandleFunc("/users", handleUsers)
      http.HandleFunc("/users/", handleUser)
      
      log.Println("Server starting on :8080")
      log.Fatal(http.ListenAndServe(":8080", nil))
  }
  
  func handleUsers(w http.ResponseWriter, r *http.Request) {
      switch r.Method {
      case http.MethodGet:
          // List users
      case http.MethodPost:
          // Create user
      default:
          http.Error(w, "Method not allowed", 
              http.StatusMethodNotAllowed)
      }
  }
  ```

### Wednesday

**Focus**: JSON encoding/decoding

- [ ] **Exercise** (25 min): JSON operations

  ```go
  type User struct {
      ID    int    `json:"id"`
      Name  string `json:"name"`
      Email string `json:"email,omitempty"`
  }
  
  func handleCreateUser(w http.ResponseWriter, r *http.Request) {
      var user User
      if err := json.NewDecoder(r.Body).Decode(&user); err != nil {
          http.Error(w, err.Error(), http.StatusBadRequest)
          return
      }
      
      // Process user...
      
      w.Header().Set("Content-Type", "application/json")
      json.NewEncoder(w).Encode(user)
  }
  ```

### Thursday-Friday

**Focus**: Middleware

- [ ] **Exercise** (45 min): Implement middleware

  ```go
  func loggingMiddleware(next http.Handler) http.Handler {
      return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
          start := time.Now()
          log.Printf("%s %s", r.Method, r.URL.Path)
          next.ServeHTTP(w, r)
          log.Printf("Completed in %v", time.Since(start))
      })
  }
  
  func main() {
      mux := http.NewServeMux()
      mux.HandleFunc("/", homeHandler)
      
      handler := loggingMiddleware(mux)
      http.ListenAndServe(":8080", handler)
  }
  ```

---

Practice these exercises daily to build strong Go foundations!

# Go Green Belt - Daily Exercises

**Duration**: 30-45 minutes per exercise  
**Goal**: Master advanced Go patterns and performance optimization

---

## Week 1: Advanced Concurrency Patterns

### Monday

**Focus**: Fan-out, fan-in pattern

- [ ] **Exercise** (40 min): Implement fan-out/fan-in

  ```go
  func fanOut(in <-chan int, workers int) []<-chan int {
      channels := make([]<-chan int, workers)
      for i := 0; i < workers; i++ {
          channels[i] = worker(in)
      }
      return channels
  }
  
  func fanIn(channels ...<-chan int) <-chan int {
      var wg sync.WaitGroup
      out := make(chan int)
      
      output := func(c <-chan int) {
          defer wg.Done()
          for n := range c {
              out <- n
          }
      }
      
      wg.Add(len(channels))
      for _, c := range channels {
          go output(c)
      }
      
      go func() {
          wg.Wait()
          close(out)
      }()
      
      return out
  }
  ```

### Tuesday

**Focus**: Pipeline pattern

- [ ] **Exercise** (35 min): Build multi-stage pipeline
  - Stage 1: Generate numbers
  - Stage 2: Square numbers
  - Stage 3: Filter evens
  - Stage 4: Sum results

### Wednesday

**Focus**: Context propagation

- [ ] **Exercise** (30 min): Pass context through pipeline
  - Implement cancellable pipeline
  - Test cancellation at different stages
  - Ensure proper cleanup

### Thursday-Friday

**Focus**: Advanced synchronization

- [ ] **Exercise** (60 min): Implement rate limiter
  - Use time.Ticker
  - Implement token bucket algorithm
  - Add burst support
  - Test concurrency

---

## Week 2: Performance & Profiling

### Monday-Tuesday

**Focus**: CPU profiling

- [ ] **Exercise** (60 min): Profile and optimize code
  - Write benchmarks
  - Generate CPU profile: `go test -cpuprofile=cpu.prof -bench=.`
  - Analyze: `go tool pprof cpu.prof`
  - Optimize hot paths
  - Re-benchmark to verify improvement

### Wednesday

**Focus**: Memory profiling

- [ ] **Exercise** (40 min): Find memory leaks
  - Generate memory profile
  - Use `go tool pprof -alloc_space`
  - Identify allocations
  - Reduce allocations with sync.Pool

### Thursday-Friday

**Focus**: Benchmarking techniques

- [ ] **Exercise** (60 min): Advanced benchmarks
  - ResetTimer usage
  - StopTimer/StartTimer for setup
  - Run parallel benchmarks
  - Use benchstat for comparison

---

## Week 3: Generics & Reflection

### Monday-Tuesday

**Focus**: Generics

- [ ] **Exercise** (60 min): Generic data structures

  ```go
  type Stack[T any] struct {
      items []T
  }
  
  func (s *Stack[T]) Push(item T) {
      s.items = append(s.items, item)
  }
  
  func (s *Stack[T]) Pop() (T, bool) {
      if len(s.items) == 0 {
          var zero T
          return zero, false
      }
      item := s.items[len(s.items)-1]
      s.items = s.items[:len(s.items)-1]
      return item, true
  }
  
  // Usage
  intStack := Stack[int]{}
  intStack.Push(42)
  
  stringStack := Stack[string]{}
  stringStack.Push("hello")
  ```

### Wednesday-Thursday

**Focus**: Reflection

- [ ] **Exercise** (60 min): Build struct validator

  ```go
  type User struct {
      Name  string `validate:"required,min=3"`
      Email string `validate:"required,email"`
      Age   int    `validate:"min=18,max=100"`
  }
  
  func Validate(v interface{}) error {
      val := reflect.ValueOf(v)
      typ := val.Type()
      
      for i := 0; i < val.NumField(); i++ {
          field := val.Field(i)
          tag := typ.Field(i).Tag.Get("validate")
          // Parse tag and validate field
      }
      return nil
  }
  ```

### Friday

**Focus**: Code generation

- [ ] **Exercise** (40 min): Generate boilerplate
  - Write template for CRUD operations
  - Use text/template
  - Implement `//go:generate` directive
  - Generate code from struct definitions

---

Remember to profile before optimizing - measure, don't guess!

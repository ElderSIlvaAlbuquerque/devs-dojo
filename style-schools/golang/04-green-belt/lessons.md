# Go - Green Belt Lessons

## Lesson 1: Advanced Concurrency Patterns

### What You'll Learn

- [ ] Fan-out and fan-in patterns
- [ ] Pipeline pattern
- [ ] Cancellation propagation
- [ ] Semaphores and rate limiting
- [ ] errgroup for error handling

### Core Ideas

#### 1. Fan-Out, Fan-In

Distribute work to multiple goroutines, then merge results:

```go
// Fan-out: Multiple workers read from same channel
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        results <- process(j)
    }
}

// Fan-in: Merge multiple channels into one
func merge(cs ...<-chan int) <-chan int {
    out := make(chan int)
    var wg sync.WaitGroup
    
    for _, c := range cs {
        wg.Add(1)
        go func(ch <-chan int) {
            defer wg.Done()
            for v := range ch {
                out <- v
            }
        }(c)
    }
    
    go func() {
        wg.Wait()
        close(out)
    }()
    
    return out
}
```

#### 2. Context-Aware Pipelines

```go
func stage(ctx context.Context, in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        defer close(out)
        for {
            select {
            case v, ok := <-in:
                if !ok {
                    return
                }
                select {
                case out <- v * 2:
                case <-ctx.Done():
                    return
                }
            case <-ctx.Done():
                return
            }
        }
    }()
    return out
}
```

### Why This Matters

These patterns enable building scalable, cancellable concurrent systems.

---

## Lesson 2: Generics (Type Parameters)

### What You'll Learn

- [ ] Generic functions
- [ ] Generic types
- [ ] Type constraints
- [ ] When to use (and not use) generics

### Core Ideas

#### 1. Generic Functions

```go
func Min[T constraints.Ordered](a, b T) T {
    if a < b {
        return a
    }
    return b
}

// Usage
Min(1, 2)        // int
Min(1.5, 2.7)    // float64
Min("a", "b")    // string
```

#### 2. Generic Data Structures

```go
type LinkedList[T any] struct {
    value T
    next  *LinkedList[T]
}

func (l *LinkedList[T]) Add(value T) {
    if l.next == nil {
        l.next = &LinkedList[T]{value: value}
    } else {
        l.next.Add(value)
    }
}
```

#### 3. Type Constraints

```go
type Numeric interface {
    int | int64 | float64
}

func Sum[T Numeric](values []T) T {
    var sum T
    for _, v := range values {
        sum += v
    }
    return sum
}
```

### Why This Matters

Generics enable writing reusable, type-safe code without interface{} and reflection.

---

## Lesson 3: Reflection

### What You'll Learn

- [ ] reflect package basics
- [ ] Type and Value inspection
- [ ] Struct tags
- [ ] When to avoid reflection

### Core Ideas

#### 1. Type Inspection

```go
import "reflect"

func inspect(v interface{}) {
    t := reflect.TypeOf(v)
    fmt.Printf("Type: %v\n", t)
    fmt.Printf("Kind: %v\n", t.Kind())
    
    val := reflect.ValueOf(v)
    fmt.Printf("Value: %v\n", val)
}
```

#### 2. Struct Tags

```go
type User struct {
    Name  string `json:"name" db:"user_name"`
    Email string `json:"email" db:"email"`
}

func getTag(v interface{}, fieldName, tagName string) string {
    t := reflect.TypeOf(v)
    field, _ := t.FieldByName(fieldName)
    return field.Tag.Get(tagName)
}

// getTag(User{}, "Name", "db") // "user_name"
```

#### 3. Setting Values

```go
func set(v interface{}, fieldName string, value interface{}) {
    rv := reflect.ValueOf(v).Elem()
    field := rv.FieldByName(fieldName)
    field.Set(reflect.ValueOf(value))
}

user := &User{}
set(user, "Name", "Alice")
```

### Why This Matters

Reflection enables building flexible libraries (JSON, ORM, validation), but use sparingly due to performance cost.

---

## Lesson 4: Performance Optimization with pprof

### What You'll Learn

- [ ] CPU profiling
- [ ] Memory profiling
- [ ] Blocking profiling
- [ ] Reading profile output
- [ ] Optimization techniques

### Core Ideas

#### 1. CPU Profiling

```bash
# In tests
go test -cpuprofile=cpu.prof -bench=.

# In production
import _ "net/http/pprof"
http.ListenAndServe(":6060", nil)
# Visit http://localhost:6060/debug/pprof/

# Analyze
go tool pprof cpu.prof
(pprof) top10
(pprof) list functionName
(pprof) web  # Generate SVG
```

#### 2. Memory Profiling

```bash
go test -memprofile=mem.prof -bench=.
go tool pprof -alloc_space mem.prof

# Reduce allocations
# Before:
result := []string{}
for _, item := range items {
    result = append(result, process(item))
}

# After: Pre-allocate
result := make([]string, 0, len(items))
for _, item := range items {
    result = append(result, process(item))
}
```

#### 3. Optimization Techniques

**String Building**:
```go
// Slow
var s string
for _, str := range strings {
    s += str  // Creates new string each time
}

// Fast
var builder strings.Builder
for _, str := range strings {
    builder.WriteString(str)
}
s := builder.String()
```

**Pool Reuse**:
```go
var bufPool = sync.Pool{
    New: func() interface{} {
        return new(bytes.Buffer)
    },
}

buf := bufPool.Get().(*bytes.Buffer)
defer bufPool.Put(buf)
buf.Reset()
// Use buf
```

### Why This Matters

Profiling reveals actual bottlenecks, enabling data-driven optimization.

---

## Lesson 5: gRPC and Protocol Buffers

### What You'll Learn

- [ ] Protocol Buffers definition
- [ ] Generating Go code from .proto
- [ ] Implementing gRPC services
- [ ] Client and server streaming
- [ ] Error handling in gRPC

### Core Ideas

#### 1. Define Service

```protobuf
// user.proto
syntax = "proto3";

package user;

service UserService {
    rpc GetUser (GetUserRequest) returns (User);
    rpc ListUsers (ListUsersRequest) returns (stream User);
}

message User {
    int32 id = 1;
    string name = 2;
    string email = 3;
}

message GetUserRequest {
    int32 id = 1;
}
```

#### 2. Implement Server

```go
type server struct {
    pb.UnimplementedUserServiceServer
}

func (s *server) GetUser(ctx context.Context, req *pb.GetUserRequest) (*pb.User, error) {
    // Lookup user
    return &pb.User{
        Id:    req.Id,
        Name:  "Alice",
        Email: "alice@example.com",
    }, nil
}

func main() {
    lis, _ := net.Listen("tcp", ":50051")
    s := grpc.NewServer()
    pb.RegisterUserServiceServer(s, &server{})
    s.Serve(lis)
}
```

#### 3. Client Usage

```go
conn, _ := grpc.Dial("localhost:50051", grpc.WithInsecure())
defer conn.Close()

client := pb.NewUserServiceClient(conn)
user, err := client.GetUser(context.Background(), &pb.GetUserRequest{Id: 1})
```

### Why This Matters

gRPC provides efficient, type-safe service communication for microservices.

---

## Lesson 6: Code Generation

### What You'll Learn

- [ ] go generate command
- [ ] text/template package
- [ ] Abstract syntax tree (AST) parsing
- [ ] Common generation patterns

### Core Ideas

#### 1. go generate Directive

```go
//go:generate stringer -type=Status
type Status int

const (
    Pending Status = iota
    Running
    Completed
)
```

#### 2. Custom Generator

```go
// generate.go
package main

import (
    "os"
    "text/template"
)

const tmpl = `
package {{.Package}}

type {{.TypeName}} struct {
    {{range .Fields}}
    {{.Name}} {{.Type}}
    {{end}}
}
`

func main() {
    t := template.Must(template.New("struct").Parse(tmpl))
    data := map[string]interface{}{
        "Package": "models",
        "TypeName": "User",
        "Fields": []map[string]string{
            {"Name": "ID", "Type": "int"},
            {"Name": "Name", "Type": "string"},
        },
    }
    t.Execute(os.Stdout, data)
}
```

### Why This Matters

Code generation reduces boilerplate and ensures consistency.

---

## Lesson 7: Distributed Tracing

### What You'll Learn

- [ ] OpenTelemetry basics
- [ ] Span creation and propagation
- [ ] Context propagation
- [ ] Integration with services

### Core Ideas

#### 1. Basic Tracing

```go
import (
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/trace"
)

func handleRequest(ctx context.Context) {
    tracer := otel.Tracer("my-service")
    ctx, span := tracer.Start(ctx, "handleRequest")
    defer span.End()
    
    // Do work
    result := doWork(ctx)
    
    span.SetAttributes(attribute.Int("result.count", result))
}

func doWork(ctx context.Context) int {
    tracer := otel.Tracer("my-service")
    _, span := tracer.Start(ctx, "doWork")
    defer span.End()
    
    // Work happens here
    return 42
}
```

### Why This Matters

Distributed tracing is essential for debugging microservices.

---

## Lesson 8: Memory Management & GC

### What You'll Learn

- [ ] Go's garbage collector
- [ ] Memory allocation patterns
- [ ] Escape analysis
- [ ] GC tuning with GOGC

### Core Ideas

#### 1. Escape Analysis

```bash
# See what escapes to heap
go build -gcflags="-m" main.go

# Keep on stack (fast)
func sum(a, b int) int {
    return a + b
}

# Escapes to heap (slower)
func makeSlice() *[]int {
    s := make([]int, 100)
    return &s  // Escapes!
}
```

#### 2. Reducing Allocations

```go
// Bad: Multiple allocations
for i := 0; i < 1000; i++ {
    s := make([]int, 100)
    process(s)
}

// Good: Reuse slice
s := make([]int, 100)
for i := 0; i < 1000; i++ {
    process(s)
}
```

### Why This Matters

Understanding memory management helps write efficient, low-latency code.

---

These advanced lessons prepare you for building high-performance, production-grade Go systems!

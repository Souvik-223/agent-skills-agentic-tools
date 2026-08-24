---
name: golang-testing
description: Comprehensive testing strategies for test-driven development and ensuring high-quality Go code.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Go Testing

Comprehensive testing strategies for test-driven development (TDD) and ensuring high-quality Go code.

## When to Activate

- When writing new Go code
- When reviewing Go code
- When improving existing tests
- When increasing test coverage
- When debugging and fixing bugs

## Core Principles

### 1. Test-Driven Development (TDD) Workflow

Follow the cycle of writing a failing test, implementing it, and refactoring.

```go
// 1. Write the test (fails)
func TestCalculateTotal(t *testing.T) {
    total := CalculateTotal([]float64{10.0, 20.0, 30.0})
    want := 60.0
    if total != want {
        t.Errorf("got %f, want %f", total, want)
    }
}

// 2. Implement it (test passes)
func CalculateTotal(prices []float64) float64 {
    var total float64
    for _, price := range prices {
        total += price
    }
    return total
}

// 3. Refactor
// Improve the code without breaking the test
```

### 2. Table-Driven Tests

Systematically test multiple cases.

```go
func TestAdd(t *testing.T) {
    tests := []struct {
        name string
        a, b int
        want int
    }{
        {"positive numbers", 2, 3, 5},
        {"negative numbers", -2, -3, -5},
        {"mixed signs", -2, 3, 1},
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

### 3. Subtests

Organizing tests logically using subtests.

```go
func TestUser(t *testing.T) {
    t.Run("validation", func(t *testing.T) {
        t.Run("empty email", func(t *testing.T) {
            user := User{Email: ""}
            if err := user.Validate(); err == nil {
                t.Error("expected validation error")
            }
        })

        t.Run("valid email", func(t *testing.T) {
            user := User{Email: "test@example.com"}
            if err := user.Validate(); err != nil {
                t.Errorf("unexpected error: %v", err)
            }
        })
    })

    t.Run("serialization", func(t *testing.T) {
        // A separate group of tests
    })
}
```

## Test Organization

### File Organization

```text
mypackage/
├── user.go
├── user_test.go          # unit tests
├── integration_test.go   # integration tests
├── testdata/             # test fixtures
│   ├── valid_user.json
│   └── invalid_user.json
└── export_test.go        # unexported symbols exported for internal testing
```

### Test Packages

```go
// user_test.go - same package (white-box testing)
package user

func TestInternalFunction(t *testing.T) {
    // Can test internals
}

// user_external_test.go - external package (black-box testing)
package user_test

import "myapp/user"

func TestPublicAPI(t *testing.T) {
    // Tests only the public API
}
```

## Assertions and Helpers

### Basic Assertions

```go
func TestBasicAssertions(t *testing.T) {
    // Equality
    got := Calculate()
    want := 42
    if got != want {
        t.Errorf("got %d, want %d", got, want)
    }

    // Error check
    _, err := Process()
    if err != nil {
        t.Fatalf("unexpected error: %v", err)
    }

    // nil check
    result := GetResult()
    if result == nil {
        t.Fatal("expected non-nil result")
    }
}
```

### Custom Helper Functions

```go
// Mark as a helper (won't show in the stack trace)
func assertEqual(t *testing.T, got, want interface{}) {
    t.Helper()
    if got != want {
        t.Errorf("got %v, want %v", got, want)
    }
}

func assertNoError(t *testing.T, err error) {
    t.Helper()
    if err != nil {
        t.Fatalf("unexpected error: %v", err)
    }
}

// Usage example
func TestWithHelpers(t *testing.T) {
    result, err := Process()
    assertNoError(t, err)
    assertEqual(t, result.Status, "success")
}
```

### Deep Equality Checks

```go
import "reflect"

func assertDeepEqual(t *testing.T, got, want interface{}) {
    t.Helper()
    if !reflect.DeepEqual(got, want) {
        t.Errorf("got %+v, want %+v", got, want)
    }
}

func TestStructEquality(t *testing.T) {
    got := User{Name: "Alice", Age: 30}
    want := User{Name: "Alice", Age: 30}
    assertDeepEqual(t, got, want)
}
```

## Mocking and Stubs

### Interface-Based Mocks

```go
// Production code
type UserStore interface {
    GetUser(id string) (*User, error)
    SaveUser(user *User) error
}

type UserService struct {
    store UserStore
}

// Test code
type MockUserStore struct {
    users map[string]*User
    err   error
}

func (m *MockUserStore) GetUser(id string) (*User, error) {
    if m.err != nil {
        return nil, m.err
    }
    return m.users[id], nil
}

func (m *MockUserStore) SaveUser(user *User) error {
    if m.err != nil {
        return m.err
    }
    m.users[user.ID] = user
    return nil
}

// Test
func TestUserService(t *testing.T) {
    mock := &MockUserStore{
        users: make(map[string]*User),
    }
    service := &UserService{store: mock}

    // Test the service...
}
```

### Mocking Time

```go
// Production code - make time injectable
type TimeProvider interface {
    Now() time.Time
}

type RealTime struct{}

func (RealTime) Now() time.Time {
    return time.Now()
}

type Service struct {
    time TimeProvider
}

// Test code
type MockTime struct {
    current time.Time
}

func (m MockTime) Now() time.Time {
    return m.current
}

func TestTimeDependent(t *testing.T) {
    mockTime := MockTime{
        current: time.Date(2024, 1, 1, 0, 0, 0, 0, time.UTC),
    }
    service := &Service{time: mockTime}

    // Test with a fixed time...
}
```

### Mocking the HTTP Client

```go
type HTTPClient interface {
    Do(req *http.Request) (*http.Response, error)
}

type MockHTTPClient struct {
    response *http.Response
    err      error
}

func (m *MockHTTPClient) Do(req *http.Request) (*http.Response, error) {
    return m.response, m.err
}

func TestAPICall(t *testing.T) {
    mockClient := &MockHTTPClient{
        response: &http.Response{
            StatusCode: 200,
            Body:       io.NopCloser(strings.NewReader(`{"status":"ok"}`)),
        },
    }

    api := &APIClient{client: mockClient}
    // Test the API client...
}
```

## Testing HTTP Handlers

### Using httptest

```go
func TestHandler(t *testing.T) {
    handler := http.HandlerFunc(MyHandler)

    req := httptest.NewRequest("GET", "/users/123", nil)
    rec := httptest.NewRecorder()

    handler.ServeHTTP(rec, req)

    // Check the status code
    if rec.Code != http.StatusOK {
        t.Errorf("got status %d, want %d", rec.Code, http.StatusOK)
    }

    // Check the response body
    var response map[string]interface{}
    if err := json.NewDecoder(rec.Body).Decode(&response); err != nil {
        t.Fatalf("failed to decode response: %v", err)
    }

    if response["id"] != "123" {
        t.Errorf("got id %v, want 123", response["id"])
    }
}
```

### Testing Middleware

```go
func TestAuthMiddleware(t *testing.T) {
    // Dummy handler
    nextHandler := http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        w.WriteHeader(http.StatusOK)
    })

    // Wrap with middleware
    handler := AuthMiddleware(nextHandler)

    tests := []struct {
        name       string
        token      string
        wantStatus int
    }{
        {"valid token", "valid-token", http.StatusOK},
        {"invalid token", "invalid", http.StatusUnauthorized},
        {"no token", "", http.StatusUnauthorized},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            req := httptest.NewRequest("GET", "/", nil)
            if tt.token != "" {
                req.Header.Set("Authorization", "Bearer "+tt.token)
            }
            rec := httptest.NewRecorder()

            handler.ServeHTTP(rec, req)

            if rec.Code != tt.wantStatus {
                t.Errorf("got status %d, want %d", rec.Code, tt.wantStatus)
            }
        })
    }
}
```

### Test Server

```go
func TestAPIIntegration(t *testing.T) {
    // Create a test server
    server := httptest.NewServer(http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        json.NewEncoder(w).Encode(map[string]string{
            "message": "hello",
        })
    }))
    defer server.Close()

    // Make an actual HTTP request
    resp, err := http.Get(server.URL)
    if err != nil {
        t.Fatalf("request failed: %v", err)
    }
    defer resp.Body.Close()

    // Verify the response
    var result map[string]string
    json.NewDecoder(resp.Body).Decode(&result)

    if result["message"] != "hello" {
        t.Errorf("got %s, want hello", result["message"])
    }
}
```

## Database Testing

### Isolating Tests with Transactions

```go
func TestUserRepository(t *testing.T) {
    db := setupTestDB(t)
    defer db.Close()

    tests := []struct {
        name string
        fn   func(*testing.T, *sql.DB)
    }{
        {"create user", testCreateUser},
        {"find user", testFindUser},
        {"update user", testUpdateUser},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            tx, err := db.Begin()
            if err != nil {
                t.Fatal(err)
            }
            defer tx.Rollback() // Roll back after the test

            tt.fn(t, tx)
        })
    }
}
```

### Test Fixtures

```go
func setupTestDB(t *testing.T) *sql.DB {
    t.Helper()

    db, err := sql.Open("postgres", "postgres://localhost/test")
    if err != nil {
        t.Fatalf("failed to connect: %v", err)
    }

    // Run schema migrations
    if err := runMigrations(db); err != nil {
        t.Fatalf("migrations failed: %v", err)
    }

    return db
}

func seedTestData(t *testing.T, db *sql.DB) {
    t.Helper()

    fixtures := []string{
        `INSERT INTO users (id, email) VALUES ('1', 'test@example.com')`,
        `INSERT INTO posts (id, user_id, title) VALUES ('1', '1', 'Test Post')`,
    }

    for _, query := range fixtures {
        if _, err := db.Exec(query); err != nil {
            t.Fatalf("failed to seed data: %v", err)
        }
    }
}
```

## Benchmarks

### Basic Benchmarks

```go
func BenchmarkCalculation(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Calculate(100)
    }
}

// Report memory allocations
func BenchmarkWithAllocs(b *testing.B) {
    b.ReportAllocs()
    for i := 0; i < b.N; i++ {
        ProcessData([]byte("test data"))
    }
}
```

### Sub-benchmarks

```go
func BenchmarkEncoding(b *testing.B) {
    data := generateTestData()

    b.Run("json", func(b *testing.B) {
        b.ReportAllocs()
        for i := 0; i < b.N; i++ {
            json.Marshal(data)
        }
    })

    b.Run("gob", func(b *testing.B) {
        b.ReportAllocs()
        var buf bytes.Buffer
        enc := gob.NewEncoder(&buf)
        b.ResetTimer()
        for i := 0; i < b.N; i++ {
            enc.Encode(data)
            buf.Reset()
        }
    })
}
```

### Benchmark Comparison

```go
// Run: go test -bench=. -benchmem
func BenchmarkStringConcat(b *testing.B) {
    b.Run("operator", func(b *testing.B) {
        for i := 0; i < b.N; i++ {
            _ = "hello" + " " + "world"
        }
    })

    b.Run("fmt.Sprintf", func(b *testing.B) {
        for i := 0; i < b.N; i++ {
            _ = fmt.Sprintf("%s %s", "hello", "world")
        }
    })

    b.Run("strings.Builder", func(b *testing.B) {
        for i := 0; i < b.N; i++ {
            var sb strings.Builder
            sb.WriteString("hello")
            sb.WriteString(" ")
            sb.WriteString("world")
            _ = sb.String()
        }
    })
}
```

## Fuzz Testing

### Basic Fuzz Test (Go 1.18+)

```go
func FuzzParseInput(f *testing.F) {
    // Seed corpus
    f.Add("hello")
    f.Add("world")
    f.Add("123")

    f.Fuzz(func(t *testing.T, input string) {
        // Verify parsing doesn't panic
        result, err := ParseInput(input)

        // Even with an error, verify the result is non-nil or consistent
        if err == nil && result == nil {
            t.Error("got nil result with no error")
        }
    })
}
```

### More Complex Fuzzing

```go
func FuzzJSONParsing(f *testing.F) {
    f.Add([]byte(`{"name":"test","age":30}`))
    f.Add([]byte(`{"name":"","age":0}`))

    f.Fuzz(func(t *testing.T, data []byte) {
        var user User
        err := json.Unmarshal(data, &user)

        // If the JSON decodes successfully, it should be re-encodable
        if err == nil {
            _, err := json.Marshal(user)
            if err != nil {
                t.Errorf("marshal failed after successful unmarshal: %v", err)
            }
        }
    })
}
```

## Test Coverage

### Running and Viewing Coverage

```bash
# Run coverage and generate an HTML report
go test -coverprofile=coverage.out ./...
go tool cover -html=coverage.out -o coverage.html

# Show coverage per package
go test -cover ./...

# Detailed coverage
go test -coverprofile=coverage.out -covermode=atomic ./...
```

### Coverage Best Practices

```go
// Good: testable code
func ProcessData(data []byte) (Result, error) {
    if len(data) == 0 {
        return Result{}, ErrEmptyData
    }

    // Each branch is testable
    if isValid(data) {
        return parseValid(data)
    }
    return parseInvalid(data)
}

// The corresponding test covers every branch
func TestProcessData(t *testing.T) {
    tests := []struct {
        name    string
        data    []byte
        wantErr bool
    }{
        {"empty data", []byte{}, true},
        {"valid data", []byte("valid"), false},
        {"invalid data", []byte("invalid"), false},
    }
    // ...
}
```

## Integration Testing

### Using Build Tags

```go
//go:build integration
// +build integration

package myapp_test

import "testing"

func TestDatabaseIntegration(t *testing.T) {
    // A test that requires a real DB
}
```

```bash
# Run integration tests
go test -tags=integration ./...

# Exclude integration tests
go test ./...
```

### Using Test Containers

```go
import "github.com/testcontainers/testcontainers-go"

func setupPostgres(t *testing.T) *sql.DB {
    ctx := context.Background()

    req := testcontainers.ContainerRequest{
        Image:        "postgres:15",
        ExposedPorts: []string{"5432/tcp"},
        Env: map[string]string{
            "POSTGRES_PASSWORD": "test",
            "POSTGRES_DB":       "testdb",
        },
    }

    container, err := testcontainers.GenericContainer(ctx, testcontainers.GenericContainerRequest{
        ContainerRequest: req,
        Started:          true,
    })
    if err != nil {
        t.Fatal(err)
    }

    t.Cleanup(func() {
        container.Terminate(ctx)
    })

    // Connect to the container
    // ...
    return db
}
```

## Test Parallelization

### Parallel Tests

```go
func TestParallel(t *testing.T) {
    tests := []struct {
        name string
        fn   func(*testing.T)
    }{
        {"test1", testCase1},
        {"test2", testCase2},
        {"test3", testCase3},
    }

    for _, tt := range tests {
        tt := tt // Capture the loop variable
        t.Run(tt.name, func(t *testing.T) {
            t.Parallel() // Run this test in parallel
            tt.fn(t)
        })
    }
}
```

### Controlling Parallel Execution

```go
func TestWithResourceLimit(t *testing.T) {
    // Only 5 tests at a time
    sem := make(chan struct{}, 5)

    tests := generateManyTests()

    for _, tt := range tests {
        tt := tt
        t.Run(tt.name, func(t *testing.T) {
            t.Parallel()

            sem <- struct{}{}        // Acquire
            defer func() { <-sem }() // Release

            tt.fn(t)
        })
    }
}
```

## Go Tooling Integration

### Test Commands

```bash
# Basic tests
go test ./...
go test -v ./...                    # verbose output
go test -run TestSpecific ./...     # run a specific test

# Coverage
go test -cover ./...
go test -coverprofile=coverage.out ./...

# Race conditions
go test -race ./...

# Benchmarks
go test -bench=. ./...
go test -bench=. -benchmem ./...
go test -bench=. -cpuprofile=cpu.prof ./...

# Fuzzing
go test -fuzz=FuzzTest

# Integration tests
go test -tags=integration ./...

# JSON format (for CI integration)
go test -json ./...
```

### Test Configuration

```bash
# Test timeout
go test -timeout 30s ./...

# Short tests (skip long-running tests)
go test -short ./...

# Clear the build cache
go clean -testcache
go test ./...
```

## Best Practices

### DRY (Don't Repeat Yourself) Principle

```go
// Good: reduce repetition with table-driven tests
func TestValidation(t *testing.T) {
    tests := []struct {
        input string
        valid bool
    }{
        {"valid@email.com", true},
        {"invalid-email", false},
        {"", false},
    }

    for _, tt := range tests {
        t.Run(tt.input, func(t *testing.T) {
            err := Validate(tt.input)
            if (err == nil) != tt.valid {
                t.Errorf("Validate(%q) error = %v, want valid = %v",
                    tt.input, err, tt.valid)
            }
        })
    }
}
```

### Separating Test Data

```go
// Good: place test data in the testdata/ directory
func TestLoadConfig(t *testing.T) {
    data, err := os.ReadFile("testdata/config.json")
    if err != nil {
        t.Fatal(err)
    }

    config, err := ParseConfig(data)
    // ...
}
```

### Using Cleanup

```go
func TestWithCleanup(t *testing.T) {
    // Set up a resource
    file, err := os.CreateTemp("", "test")
    if err != nil {
        t.Fatal(err)
    }

    // Register cleanup (similar to defer, but works with subtests)
    t.Cleanup(func() {
        os.Remove(file.Name())
    })

    // Continue the test...
}
```

### Clarifying Error Messages

```go
// Bad: unclear error
if result != expected {
    t.Error("wrong result")
}

// Good: error with context
if result != expected {
    t.Errorf("Calculate(%d) = %d; want %d", input, result, expected)
}

// Better: use a helper function
assertEqual(t, result, expected, "Calculate(%d)", input)
```

## Anti-Patterns to Avoid

```go
// Bad: depends on external state
func TestBadDependency(t *testing.T) {
    result := GetUserFromDatabase("123") // Uses a real DB
    // The test is brittle and slow
}

// Good: inject the dependency
func TestGoodDependency(t *testing.T) {
    mockDB := &MockDatabase{
        users: map[string]User{"123": {ID: "123"}},
    }
    result := GetUser(mockDB, "123")
}

// Bad: sharing state between tests
var sharedCounter int

func TestShared1(t *testing.T) {
    sharedCounter++
    // Depends on test ordering
}

// Good: keep each test independent
func TestIndependent(t *testing.T) {
    counter := 0
    counter++
    // Doesn't affect other tests
}

// Bad: ignoring the error
func TestIgnoreError(t *testing.T) {
    result, _ := Process()
    if result != expected {
        t.Error("wrong result")
    }
}

// Good: check the error
func TestCheckError(t *testing.T) {
    result, err := Process()
    if err != nil {
        t.Fatalf("Process() error = %v", err)
    }
    if result != expected {
        t.Errorf("got %v, want %v", result, expected)
    }
}
```

## Quick Reference

| Command/Pattern | Purpose |
|--------------|---------|
| `go test ./...` | Run all tests |
| `go test -v` | Verbose output |
| `go test -cover` | Coverage report |
| `go test -race` | Detect race conditions |
| `go test -bench=.` | Run benchmarks |
| `t.Run()` | Subtest |
| `t.Helper()` | Test helper function |
| `t.Parallel()` | Run the test in parallel |
| `t.Cleanup()` | Register cleanup |
| `testdata/` | Directory for test fixtures |
| `-short` | Skip long-running tests |
| `-tags=integration` | Run tests with a build tag |

**Remember**: Good tests are fast, reliable, maintainable, and clear. Aim for clarity over complexity.

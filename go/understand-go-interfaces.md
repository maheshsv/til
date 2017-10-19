# Understand Go Interfaces

Excerpt from YouTube [video](https://www.youtube.com/watch?v=F4wUrj6pmSI).

### Why use interfaces?

- Write generic algorithms
- hiding implementation details
- provide interception points

A Stack interface

```go
type Stack interface {
  Push(interface{}) Stack
  Pop() Stack
  Empty() bool
}

// algorithms on Stack
func Size(s Stack) int {
  if s.Empty() {
      return 0
  }
  return Size(s.Pop()) + 1
}
```

A Sortable interface

```go
type Sortable interface {
  Less(i, j int) bool
  Swap(i, j int)
  Len() int
}
```

### Implicit interface implementation

### Type assertion


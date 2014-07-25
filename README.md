precond
=======

A library that contains utilities for checking functions' preconditions
in [Go programming language](http://golang.org). Precondition checking
is a concept intruduced in code design approach called [Design
by Contract](http://en.wikipedia.org/wiki/Contract_programming).
If preconditions of a function are not satisfied then, according
to [Crash Early Principle](http://pragmatictips.com/32), program
is invalid and should be immediately terminated. Termination should
be preceeded with proper message that describes a bug.

How To Use It?
--------------

As many other languages, Go does not provide nillability information
in its type system. Precond fills this gap by providing *precond.NotNil*
function. Checking if argument is not nil is the most simple and most common
way of using the library.

```go
import "github.com/gosmos/precond"

func trim(noBeTrimmed string) string {
  // if toBeTrimmed is nil, precond.NotNil will panic
  // with error passed as second argument
  precond.NotNil(toBeTrimmed, "trimmed string must not be null");

  ...
}
```

All methods in the *precond* and *check* namespace support passing arguments
to be used when formatting error message.

```go
import "github.com/gosmos/precond"

func (set *Set) get(index int) interface{} {
  // if index is not contained in <0, length> precond.InRange
  // eill panic with properly formatted error
  precond.InRange(index, 0, set.Length(), "index %v out of bounds", index);

  ...
}
```

Contradicting Official Documentation
------------------------------------

"Effective Go", which is a part of official Go's documentation, states that
[functions should avoid panic](http://golang.org/doc/effective_go.html#panic).
This library contradicts that guideline, because the guideline is againts
Crash Early Principle.

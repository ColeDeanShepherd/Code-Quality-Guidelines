# Code Quality Guidelines

## Underlying Principles

* Code is read more than it is written. So, make code **easy to read**!
* For software development to be considered a profession in the literal sense of the word, code quality needs to be a high-priority.
* Make it easiest to do the safe thing, harder to do the unsafe thing. Encapsulate unsafe code.
* 

## Code Examples

### Hello, World!

```
fn main() {
    Console.printLine("Hello, world!")
}
```

Concerns with this program:

* OS error
  * unable to open console
  * unable to print to console
* Out of memory?
  * "Hello, world!" is probably stored in static data section of .exe, so probably not.
  * But, if it was dynamically allocated, that's a concern.

### Fibonacci

```
fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)
fibonacci(0) = 0
fibonacci(1) = 1
```

Concerns with this program:

* Negative `n`
* non-integral `n`
* Stack overflow with large `n`.
* Needless re-computation of sub-problems.

```
fn fibonacci(n: NonNegativeInteger): NonNegativeInteger {
    if n = 0 {
        return 0
    } else if n = 1 {
        return 1
    }
    
    var fibNMinus2: NonNegativeInteger := 0
    var fibNMinus1: NonNegativeInteger := 1
    var fibN: NonNegativeInteger := uninitialized
    
    for (var curN: NonNegativeInteger := 2; curN <= n; curN++) {
        fibN := fibNMinus2 + fibNMinus1
        fibNMinus2 := fibNMinus1
        fibNMinus1 := fibN
    }
    
    return fibN
}
```

Concerns with this program:

* Slow due to arbitrary-precision integers.

```
fn fibonacci(n: NonNegativeInt32): NonNegativeInt32 {
    if n = 0 {
        return 0
    } else if n = 1 {
        return 1
    }
    
    var fibNMinus2: NonNegativeInt32 := 0
    var fibNMinus1: NonNegativeInt32 := 1
    var fibN: NonNegativeInt32 := uninitialized
    
    for (var curN: NonNegativeInt32 := 2; curN <= n; curN++) {
        fibN := fibNMinus2 + fibNMinus1
        fibNMinus2 := fibNMinus1
        fibNMinus1 := fibN
    }
    
    return fibN
}
```

Concerns with this program:

* Possible integer overflow at `fibN := fibNMinus2 + fibNMinus1`

## Naming

* Be descriptive enough to make names understandable without outside knowledge, given the context.
  * Avoid local acronyms. Global acronyms, used throughout the system, can be OK.
* Be consistent
  * 
* Use opposites

## Named Arguments

* The problem with "magic number" parameters.
  * `login("user", "pass", true, false)`
    * What is this function doing?
  * How about: `login("user", "pass", rememberMe: true, appearOffline: false)`

## Newlines & White-space

* Braces
* Multi-line alignment
* Tabs vs. spaces
* UNIX-style vs. Windows-style line endings

## Testing

* unit testing
* integration testing
* stress testing
* integration with D.B.C.

## Design By Contract

* preconditions
  * a condition that must always be true just prior to the execution of some section of code
* postconditions
  * a condition that must always be true just after the execution of some section of code
  * unit tests are just checking postconditions given certain inputs
* invariants
  * a condition that can be relied upon to be true during some portion of the execution of a program

## Overflow & Underflow

* How the hell do you handle this in reliable systems???

## malloc failures

* How the hell do you handle this in reliable systems???

## Performance

* Data-oriented design
* Bottlenecks
* Profiling
* Algorithm choice

## Commenting

* Prefer to make the code as descriptive as possible.
* Comments just add extra knowledge that you cannot convey in code.

## Version Control

* Use it!

## Global Variables

* Avoid them

## Parallelism

* Shared memory
  * Race conditions
    * Detection
    * Avoidance
* Message passing
* Software transactional memory?

## Variables & Constants

* Const-by-default

## File & Directory Organization

* Organize by feature? By file type?

## Security

* Password hashing and salting
* SQL injection
* Cross-site scripting
* Two-factor authentication
* Encryption
* Storing critical information
  * Credit cards
  * SSN,
  * etc.
* Logging

## Privacy & User Data

* EU General Data Protection Regulation (GDPR)
# Does functional programming relieve TDD?
## Talks
- "Does functional programming relieve TDD?" ("Macht funktionale Programmierung TDD überflüssig?"), Johannes Link (johanneslink.net) (slides via mail)

## Content
### TDD a la Kent Beck
- developer writes automated tests while programming
- tests will be written before the programm code
- design in small steps and continuously
- Test -> Code -> Refactor
- big amount of tests that are maintainable create trust in codebase
- focus on micro-tests

### Functional programming
- offer a new perspective
- necessary building blocks:
    - pure functions => possible in Java
    - higher order functions => possible in Java
    - immutable data structures => not that easy in Java
- nice to have building blocks:
    - functions as first class citizens => not in Java
    - anonymous functions aka lambdas => existing in Java
    - type system and syntax HOF - friendly (higher order functions) => not in Java
    - one-the fly creatable flexible datastructures => not in Java
    - pattern matching => not in Java
    - tail-recursion optimizing => not in Java
- additional perspectives
    - separation of pure and unpure functions
    - algebraic type system
    - lazy evaluation
   
### Writing OO tests with functional aspects
- to verify side effects and state, we need stubs and mocks (Steven: interesting thought! Never realized that we would not need those in functional programming). These tests often hard to maintain.
- "Test with mocks don't tell a story. They are very implementation-detailed: If x than z." ... "Hard to do it another way in Java" => easier in Haskell
- solution: "good object oriented design": "Everything that is a side effect and has nothing to do with the business logic should be provided via parameter.", for example console-object to print in
- functional design = "pressing IO-stuff to the sides" to focus on the main problem
- "list of strings in, list of strings out" is very easy to understand
- functional programming makes testing easy and readable
- in functional programming, mocks are only necessary in "outer hull". Within this hull, important business logic can be tested nicely.
- example: assertScore(1,3) as a method that encapsulates calls to getter. Similarities to Domain Driven Design!

### property testing
- classical approach = write function that should have a specific behavior, specify data points to test behavior of function
- property testing, for example [Scala Test](http://www.scalatest.org/user_guide/property_based_testing): data points are not to be provided, instead the contract of function is tested via provided generators or tables.
- tool for Java: [junit-quickcheck](https://github.com/pholser/junit-quickcheck)

### What can we learn for Java?
- more Immutables!
- more Pure functions!
- more total functions (every possible input can be processed without error)
- more property-testing for pure functions
- hexagonal architecture (aka ports and adaptors): side effects only at the "outer hull" of the implementation

### Conclusion
- TDD works with functional programs, too
- refactoring feels differently
- tests of pure functions easier to understand and don't need mocks
- Value objects needed for pure functions
- property testing work great for pure functions
- good type systems makes some tests redundant

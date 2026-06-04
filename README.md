# Notes on `Algebraic Effects` in Programming

**Algebraic effects** are a modern approach to managing side effects in programming by **separating the definition of an effectful operation from its execution logic**.

They act like an advanced version of `try/catch` blocks where, after an exception is "caught" and processed, the program can **resume execution exactly where it left off**.

## Core Concepts
#### **Effects**: 
Abstract declarations of what a program wants to do (e.g., `perform AskName`).
**Handlers**: Code blocks that intercept the effect and decide how to fulfill it.
**Continuations**: Captures the remaining execution path, allowing handlers to return a value back to the call site.

## How It Works vs. Exceptions

| Feature | Exceptions (`try/catch`) | Algebraic Effects |
| :--- | :--- | :--- |
| **Direction** | One-way unwinding | Two-way communication |
| **Control Flow** | Terminates the call stack | Pauses and resumes the stack |
| **Continuations** | Destroyed immediately | Captured and executable |


## Key Benefits

**Decoupled Architecture**: Functions state *what* they need, while handlers decide *how* to provide it.
**Context Independent**: The same function can use a network-based handler in production and a mocked handler in tests.
**No Color Incompatibility**: Unlike the `async/await` split ("colored functions"), functions do not need special keywords to pass effects up the stack.

**State Management**: Simplifies complex control flows like async operations, time-travel debugging, and generator-like behavior.

**Functional_Programming**: When a function needs to perform an effect, it does not actually run the effect. Instead, it returns a pure data structure that represents a request for that effect, alongside a continuation (a function representing the rest of the program).Impure Edge: The program remains 100% pure until it reaches the runtime or an outer handler, which finally interprets that data structure and executes the actual side effect.

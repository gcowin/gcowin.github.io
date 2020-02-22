What is a monad?
----------------
Technically, a “monad” is simply a term for something with three components:

1. A data structure
2. Some related functions
3. Some rules about how the functions must work

To be a monad, the data type must have two related functions as well, return and bind:

return (also known as pure) is a function that turns a normal value into a monadic type. Since the type we’re using is Result, the return function is just the Ok constructor.

bind (also known as flatMap) is a function that lets you chain together monadic functions (in our case, Result-generating functions).  

named after monoid and triad

Examples
--------
Maybe/Option
IO
SelectMany

Why?
----
Isolate side-effects declaratively; especially for functional languages.

Good for projecting state.

One other noteworthy use for monads is isolating side-effects, like input/output or mutable state, in otherwise purely functional code.


Formal Monad Definition
-----------------------
Given any well-defined, basic types T, U, a monad consists of three parts:

1. A type constructor M that builds up a monadic type M T[b]
2. A type converter, often called unit or return, that embeds an object x in the monad:
unit(x) : T → M T[c]
3. A combinator, typically called bind (as in binding a variable) and represented with an infix operator >>=, that unwraps a monadic variable, then inserts it into a monadic function/expression, resulting in a new monadic value:
(mx >>= f) : (M T, T → M U) → M U[d]
To fully qualify as a monad though, these three parts must also respect a few laws:

unit is a left-identity for bind:
unit(a) >>= λx → f(x) ↔ f(a)

unit is also a right-identity for bind:
ma >>= λx → unit(x) ↔ ma

bind is essentially associative:[e]
ma >>= λx → (f(x) >>= λy → g(y)) ↔ (ma >>= λx → f(x)) >>= λy → g(y)[2]

Algebraically, this means any monad both gives rise to a category (called the Kleisli category) and a monoid in the category of functors (from values to computations), with monadic composition as a binary operator and unit as identity. 


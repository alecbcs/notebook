# An Introduction to Rust
(Note: This document was created as part of a class assignment.)

### History and Current Status

Rust began as the brain child of software engineer Graydon Hoare in 2006. While Hoare was working for Mozilla, the company adopted the project began funding the development of Rust in 2009. As a fun fact, Rust was first originally built off of the Ocaml language before it’s own compiler successfully compiled itself in 2011. Since 2016 the language has consistently been ranked the most loved programming language in Stack Overflow’s annual developer survey. 

### Paradigm

Rust advertises itself as a multi-paradigm language, including aspects of concurrent, functional, generic, and imperative languages. Although early versions Rust also included objects, they were replaced by structured types before the first stable release in 2015. A driving feature of Rust as stated by the development team, is the ability safely handle race conditions and dangling pointers to help the development of better concurrent projects. Rust’s syntax (function signatures, etc…) was inspired by functional programming languages and their use of immutable data values, as well as inferred static typing from the function headers.

### Typing System

Rust is a statically typed language although, its’ implementation more closely follows that of Haskell’s than that of Java’s. Rust’s implementation of static typing, “tries to get out of the users way” by inferring the types of variables from the function’s signature.


### Control Structures
Rust supports many of the standard control flow mechanisms used by imperative languages such as, if, else, and else if, as well as standard for and while loops. Drawing from functional languages, Rust also implements matching (similar to guards in Haskell) which allow for pattern matching and recursive calls.

### Semantics
By default, all variable bindings in Rust are treated as immutable unless initialized with the keyword `mut`. 


### Desirable Language Characteristics (Efficiency, Security)

Rust makes a point to be a highly efficient and secure language without having a garbage collection system. This makes Rust a practical choice for writing operating systems, embedded device software, etc…. One of the guiding principles behind Rust is making it impossible to end up with dangling pointers. A dangling pointer occurs when a data structure is cleaned up while still having active pointers storing the structure’s address. After the object is removed these aliases no point to any valid object and thus are considered to be dangling.
# An Introduction to Rust
(Note: This document was created as part of a class assignment.)

### History and Current Status

Rust began as the brain child of software engineer Graydon Hoare in 2006. While Hoare was working for Mozilla, the company adopted the project began funding the development of Rust in 2009. As a fun fact, Rust was first originally built off of the Ocaml language before it’s own compiler successfully compiled itself in 2011. Since 2016 the language has consistently been ranked the most loved programming language in Stack Overflow’s annual developer survey. 

### Paradigm

Rust advertises itself as a multi-paradigm language, including aspects of concurrent, functional, generic, and imperative languages. Although early versions Rust also included objects, they were replaced by structured types before the first stable release in 2015. A driving feature of Rust as stated by the development team, is the ability safely handle race conditions and dangling pointers to help the development of better concurrent projects. Rust’s syntax (function signatures, etc…) was inspired by functional programming languages and their use of immutable data values, as well as inferred static typing from the function headers.

### Typing System

Rust is a statically typed language although, its’ implementation more closely follows that of Haskell’s than that of Java’s. Rust’s implementation of static typing, “tries to get out of the users way” by inferring the types of variables from the function’s signature.


### Control Structures
Rust supports many of the standard control flow mechanisms used by imperative languages such as, if, else, and else if, as well as standard for and while loops. Drawing from functional languages, Rust also implements matching (similar to guards in Haskell) which allow for pattern matching and recursive calls.

### Semantics
By default, all variable bindings in Rust are treated as immutable unless initialized with the keyword `mut`. In order to manually assign a value to a type we use **type annotations**. A type annotation suceededs the name of the variable being seperated by a colon. (Ex. `let x: i32;` which initializes the variable of x to be a 32-bit integer. ) Like many other languages, Rust follows a static method of assignming the scope of a variable. Thus the scope of a variable is determined by the block in which it is defined rather than the time the variable is created during the execution of the program.


### Desirable Language Characteristics (Efficiency, Security)

Rust makes a point to be a highly efficient and secure language without having a garbage collection system. This makes Rust a practical choice for writing operating systems, embedded device software, etc…. One of the guiding principles behind Rust is making it impossible to end up with dangling pointers. A dangling pointer occurs when a data structure is cleaned up while still having active pointers storing the structure’s address. After the object is removed these aliases no point to any valid object and thus are considered to be dangling.

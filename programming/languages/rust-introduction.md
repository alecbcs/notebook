# An Introduction to Rust
(Note: This document was created as part of a class assignment.)

## Table of Contents
- [History and Current Status](#history-and-current-status)
- [Paradigm](#paradigm)
- [Typing System](#typing-system)
- [Control Structures](#control-structures)
- [Semantics](#semantics)
- [Desirable Language Characteristics (Efficiency, Security)](#desirable-language-characteristics-efficiency-security)
- [**New!** Rust Project/Simulations!](#testing-rust)

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

## Testing Rust
As part of a project assignment to learn Rust, I chose to implement a multi-threaded Monte Carlo Simulation to calculate the value of Pi. From the get-go, while doing a bit of background research on Rust, I knew I wanted to test out Rust's parrallel computing capabilities. It seems as though almost every developer I bump into in the field of High Performance Computing/Research Computing seems to ask me if I've worked in Go or Rust yet. I've been developing Go applications for a number of years at this point for both work and personal projects, but until recently I hadn't taken the time to sit down and try out Rust. And honestly, I might have dismissed some of the love for Rust I heard as love some of us have for Mozilla as an open source organization over Google. Man, how wrong I was. (But I'll get to that at the end.)

After deciding that I wanted to focus on building multi-threaded project to test Rust's speed on a large amount of data, I set out see what computing problems would fit that goal. What I stumbled upon, was the Monte Carlo method for computing. Monte Carlo simulations are often used in physics for fluid dymamics, biology to simulate cell structures, as well as business and mathmatics when measuring uncertanty. Monte Carlo algorithms are defined by their use of randomness and random input to generate deterministic solutions. (Which is so cool!)

If that all sounds a bit abstract and confusing, here's an example. In this project I randomly generated hundreds of thousands (sometimes hundrends of millions) of points in a 1 by 1 square. So randomly generated x and y values ranging from -1 to 1. Then I calculated the distance for each of those points from the origin (center of the square). Using this distance from the origin, we can then determine if the points fall within or outside of a unit circle. (A circle starting at the same origin with a radius of 1.) Checking if each point's location, we get a ratio of the number of points within the circle to those outside of the circle. The value of this ratio is actually 1/4th of pi! (So multiplying by 4). We can, albeit very ineffeciently, calculate the value of pi from randomness!

However, I bet you're already seeing the problem with this approach. It's slow. Like generating hundreds of millions of points slow and then doing calculations on each of them slow. But that's exactly what we wanted! So this should be the perfect task to see how Rust's multi-threading implementation stacks up. So to break up the work, I set out to create worker theads. The main thread of the program calculates based off the the number of points entered and the number of processes how many points will get generated by each process. After that the main process kicks off the number of desired worker threads and collects the results of their calculations with a buffered channel in Rust. Here are the results of running this algorithm with 1 vs 8 theads!

``` plain
alecbcs@io ~/.../Part 3 $ time ./monte-pilo 1 80000000
Result: 3.14148315

real	0m1.486s
user	0m1.474s
sys	0m0.013s
alecbcs@io ~/.../Part 3 $ time ./monte-pilo 8 80000000
Result: 3.1417106

real	0m0.266s
user	0m1.851s
sys	0m0.024s

```

Pretty awesome right! We can see that increasing the number of cores and distributing the work makes the simulation signifigantly faster.

Okay but is Rust actually faster than Go? The language I spend most of my time in and love. Implementing the same exact program with multi-threading in Go, these are the results.

``` plain
alecbcs@io ~/.../Part 3 $ time ./montepi-go 8 80000000
Result:  3.1417699

real	0m9.401s
user	0m24.477s
sys	0m0.350s
alecbcs@io ~/.../Part 3 $ time ./montepilo-rust 8 80000000
Result: 3.14166615

real	0m0.263s
user	0m1.845s
sys	0m0.013s

```

Well...I was taken aback by these results. Not only is Rust faster, it's significantly faster than Go. And as it turns out, after reading into more documentation, that's actually (sort of) by design in Go. The Go compiler prioritizes the speed of compilation rather than finding the most optimal way to generate the machine code and taking a long time to develop. In scenarios like this finding the optimal machine code for these calculations makes a radical difference in the result but that might not always be the case with more complicated applications.

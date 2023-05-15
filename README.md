
# Review Questions

Explain the difference between dynamic scoping and lexical scoping. Provide examples of programming languages that use each of these scoping mechanisms.

<details>
<summary>Answer</summary>

Dynamic scoping and lexical scoping are two different approaches to variable scoping in programming languages.

In lexical scoping, also known as static scoping, the scope of a variable is determined by its position in the source code. Variables declared in an outer block are visible and accessible in all inner blocks, but variables declared in inner blocks are not visible in outer blocks. This means that the scope of a variable is determined by the lexical structure of the code.

For example, consider the following code snippet in JavaScript:

```
let x = 10;

function foo() {
  console.log(x);
}

function bar() {
  let x = 20;
  foo();
}

bar(); // output: 10
```

In this code, the variable `x` is declared outside the functions `foo` and `bar`, so it has a global scope and is visible in both functions. When `bar` calls `foo`, `foo` accesses the global variable `x` and outputs its value, which is `10`.

In dynamic scoping, the scope of a variable is determined by the calling context of a function. Variables are searched for in the calling function before they are searched for in the function being called. This means that the scope of a variable is determined by the dynamic flow of the program.

For example, consider the following code snippet in Perl:

```
$var = 10;

sub foo {
  print $var;
}

sub bar {
  local $var = 20;
  foo();
}

bar(); # output: 20
```

In this code, the variable `$var` is declared outside the functions `foo` and `bar`, so it has a global scope and is visible in both functions. When `bar` calls `foo`, it sets the value of `$var` to `20` in the local scope of `bar`, which is then accessed by `foo` because it was called from `bar`. Thus, the output of the program is `20`.

Dynamic scoping is less commonly used than lexical scoping, but some programming languages, such as Perl and Emacs Lisp, support it. Most modern programming languages, including JavaScript, Python, and Java, use lexical scoping.
</details>

Define the term "closure" in the context of functional programming. Provide an example of a closure in a programming language of your choice.

<details>
<summary>Answer</summary>

In functional programming, a closure is a function that has access to variables in its lexical scope, even after the scope has been destroyed. In other words, a closure "closes over" the variables in its environment, allowing them to be accessed and manipulated even after the function has returned.

Closures are a powerful feature of functional programming because they enable data encapsulation and abstraction, making it possible to create functions with hidden state that can be used as building blocks for larger programs.

Here is an example of a closure in JavaScript:

```javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  }
}

let add5 = makeAdder(5);
console.log(add5(3)); // output: 8
```

In this code, the `makeAdder` function returns a new function that adds a given number `x` to its argument `y`. When `makeAdder` is called with an argument of `5`, it returns a new function that adds `5` to its argument.

The returned function is a closure because it "closes over" the value of `x`, even after `makeAdder` has returned. When `add5` is called with an argument of `3`, it adds `5` (the value of `x`) to `3` (the argument passed to the closure), resulting in `8`.

In this example, the closure created by `makeAdder` is a simple example of how closures can be used to create functions with hidden state that can be used as building blocks for larger programs.
</details>

Explain the concept of higher-order functions. Provide examples of higher-order functions in Scheme.

<details>
<summary>Answer</summary>

Higher-order functions are functions that take other functions as arguments or return functions as results. In other words, they treat functions as first-class citizens, just like any other data type, allowing for more flexible and powerful programming constructs.

In Scheme, as in many other functional programming languages, higher-order functions are a fundamental feature. Here are some examples of higher-order functions in Scheme:

1. `map`: `map` is a higher-order function that takes a function and a list as arguments, and returns a new list obtained by applying the function to each element of the original list. For example:

   ```scheme
   (define (square x) (* x x))
   (map square '(1 2 3 4 5)) ; returns '(1 4 9 16 25)
   ```

   In this example, the `map` function applies the `square` function to each element of the list `(1 2 3 4 5)` to produce the new list `(1 4 9 16 25)`.

2. `filter`: `filter` is a higher-order function that takes a predicate function and a list as arguments, and returns a new list containing only the elements of the original list that satisfy the predicate. For example:

   ```scheme
   (define (even? x) (= (modulo x 2) 0))
   (filter even? '(1 2 3 4 5)) ; returns '(2 4)
   ```

   In this example, the `filter` function applies the `even?` predicate function to each element of the list `(1 2 3 4 5)` and returns only the elements that satisfy the predicate, which are `2` and `4`.

3. `compose`: `compose` is a higher-order function that takes two functions as arguments and returns a new function that applies the second function to the result of applying the first function. For example:

   ```scheme
   (define (square x) (* x x))
   (define (add-one x) (+ x 1))
   ((compose square add-one) 5) ; returns 36
   ```

   In this example, the `compose` function creates a new function that applies the `square` function to its argument, and then applies the `add-one` function to the result. The resulting function is then applied to the value `5`, producing the result `36`.

Overall, higher-order functions are a powerful tool for functional programming. They allow for more concise and expressive code, and enable the creation of complex abstractions and control structures.

</details>

Explain the concept of tail recursion optimization. Why is this optimization important in functional programming languages? Provide an example of a tail-recursive function in Scheme.

<details>
<summary>Answer</summary>

Tail recursion optimization is an optimization technique used in functional programming languages to optimize tail-recursive function calls, which are function calls where the recursive call is the last operation performed by the function. By optimizing these tail-recursive calls, the compiler or interpreter can reuse the same stack frame for each recursive call, rather than creating a new stack frame for each call, which can result in a significant improvement in performance and reduction of memory usage.

In a traditional recursive function, each recursive call creates a new stack frame, which is added to the call stack. This can lead to a stack overflow error if the recursion depth becomes too large. However, with tail recursion optimization, the last operation of a recursive function is a call to itself, and the current stack frame can be reused for each call, eliminating the need for additional stack frames.

Tail recursion optimization is important in functional programming languages because many functional programming algorithms are naturally expressed using recursion. By optimizing tail-recursive calls, functional programming languages can enable developers to write efficient recursive code without worrying about stack overflow errors.

Here is an example of a tail-recursive function in Scheme that calculates the factorial of a given number:

```scheme
(define (factorial n)
  (define (fact-iter n acc)
    (if (= n 0)
        acc
        (fact-iter (- n 1) (* n acc))))
  (fact-iter n 1))
```

In this code, the `factorial` function is defined to call the `fact-iter` function with two arguments: the input `n` and an accumulator value of `1`. The `fact-iter` function is tail-recursive because the recursive call to `fact-iter` is the last operation in the function, and it passes the new accumulator value as its second argument. By passing the new accumulator value as an argument, the tail recursion optimization can be applied, and the stack frame can be reused for each recursive call. This implementation of `factorial` is efficient and can calculate the factorial of large numbers without causing a stack overflow error.

</details>

Define the term "continuation" in the context of programming languages. Explain how continuations can be used to implement control structures such as loops and exceptions.

<details>
<summary>Answer</summary>

In programming languages, a continuation is a representation of the current state of execution in a program. More specifically, it captures the current call stack, including all local variables, and allows the program to be resumed from that point in the future. Continuations can be used to implement various control structures, such as loops and exceptions, by capturing the program state and allowing it to be manipulated.

One use of continuations is to implement loops. In languages without built-in loop constructs, such as Scheme, continuations can be used to create an iterative process by capturing the current state of the loop and passing it back to the loop's entry point. This creates a loop-like behavior without the need for explicit loop constructs.

Another common use of continuations is to implement exception handling. When an exception is thrown, the current continuation is saved and passed to an exception handler. The handler can then manipulate the continuation to either recover from the error or propagate it up the call stack. By capturing the current continuation, it is possible to recover from an error and resume execution from a known state.

Continuations can also be used to implement backtracking search algorithms, where the state of the program is captured at each branching point and different paths can be explored by manipulating the captured continuations.

In summary, continuations are a powerful language feature that allows programs to capture and manipulate their state of execution. By using continuations, it is possible to implement various control structures, such as loops and exceptions, without relying on language-specific constructs.

</details>

Explain the concept of continuation passing style. Provide examples in Scheme.

<details>
<summary>Answer</summary>

Continuation passing style (CPS) is a programming technique where functions are written to take an additional argument, called a continuation, which represents what should happen with the function's result. Rather than returning a value directly, a function in CPS takes the continuation as an argument and passes its result to the continuation.

The primary benefit of CPS is that it allows for more flexible control flow in a program. By passing continuations explicitly, it is possible to implement complex control structures such as exceptions, backtracking search, and coroutines. Additionally, CPS can simplify code by eliminating the need for nested function calls and intermediate variables.

Here is an example of a function written in CPS in Scheme:

```scheme
(define (factorial n k)
  (if (<= n 1)
      (k 1)
      (factorial (- n 1)
                  (lambda (result)
                    (k (* n result))))))

(factorial 5
           (lambda (result)
             (display result)))
```

In this example, `factorial` is a function that calculates the factorial of a given number `n`. It is defined to take an additional argument, `k`, which represents the continuation. Instead of returning a value directly, `factorial` passes its result to the continuation `k` using the `lambda` expression.

The second part of the example shows how to call the `factorial` function in CPS style. The second argument to `factorial` is a `lambda` expression that represents the continuation. In this case, the continuation simply displays the result of the computation.

Here is another example of a function in CPS that demonstrates how CPS can simplify code:

```scheme
(define (sum-list lst k)
  (if (null? lst)
      (k 0)
      (sum-list (cdr lst)
                (lambda (result)
                  (k (+ (car lst) result))))))

(sum-list '(1 2 3 4 5)
          (lambda (result)
            (display result)))
```

In this example, `sum-list` is a function that calculates the sum of a list of numbers. It is written in CPS style, taking an additional argument `k` which represents the continuation. By passing the continuation explicitly, the function can eliminate the need for nested function calls and intermediate variables.

Overall, continuation passing style is a powerful programming technique that allows for more flexible control flow in a program. By writing functions to take continuations as arguments, it is possible to implement complex control structures and simplify code.

</details>

Compare and contrast imperative programming and declarative programming paradigms. Provide examples in Scheme that use each of these paradigms.

<details>
<summary>Answer</summary>

Imperative programming and declarative programming are two different paradigms used in computer programming. Here are some of the key differences between the two:

1. Approach: Imperative programming is an approach where the programmer explicitly tells the computer how to do a task, whereas declarative programming is an approach where the programmer specifies what the task is, and the computer figures out how to do it.

2. Control flow: In imperative programming, the control flow is controlled by the programmer, and the order of instructions matters. In declarative programming, the order of instructions does not matter, and the program is executed based on the relationships between the different elements.

3. State: In imperative programming, the state of the program changes over time, and the programmer has to manage the state explicitly. In declarative programming, the state is implicit, and the program is written in a way that the state is automatically managed by the system.

4. Side effects: Imperative programming relies heavily on side effects, such as changing the values of variables or modifying data structures. Declarative programming, on the other hand, tries to minimize side effects and instead focuses on producing a result based on the inputs given.

Here's an example of an imperative program in Scheme that calculates the factorial of a number:

```scheme
(define (factorial n)
  (let ((result 1))
    (do ((i n (- i 1)))
        ((<= i 0) result)
      (set! result (* result i)))))
```

Declarative programming:

- Focuses on what outcome or result is desired, without necessarily specifying how to achieve it.
- Programs are made up of expressions that describe relationships between different values.
- Control structures like map, filter, and reduce are used to transform and manipulate data.
- Examples of declarative programming languages include SQL, Prolog, and Haskell.

Here's an example of a declarative program in Scheme that calculates the sum of the squares of the odd numbers in a list:

```scheme
(define (sum-of-squares-of-odds lst)
  (foldl +
         0
         (map (lambda (x) (* x x))
              (filter odd? lst))))
```

In this example, the program is composed of a sequence of function calls that describe the desired outcome: first, the `filter` function is used to select only the odd numbers in the list; then, the `map` function is used to calculate the squares of those numbers; and finally, the `foldl` function is used to add up the squares. This program is declarative because it focuses on what outcome is desired, without specifying how to achieve it.

Overall, the choice between imperative and declarative programming depends on the specific problem being solved and the preferences of the programmer. Imperative programming can be more flexible and efficient in some cases, while declarative programming can be more concise and expressive in others.

</details>

Explain how delay and force works in Scheme.

<details>
<summary>Answer</summary>

In Scheme, `delay` and `force` are two procedures that provide a way to implement lazy evaluation. Lazy evaluation is a programming technique that defers the computation of a value until it is actually needed. This can be useful in situations where the computation is expensive or where the value may not be needed at all.

The `delay` procedure takes a single argument, which is a Scheme expression. It returns a procedure that represents the delayed computation of that expression. The expression is not evaluated immediately, but is instead stored as a promise that will be evaluated the first time its value is needed.

The `force` procedure takes a single argument, which is a procedure that represents a delayed computation (such as one returned by `delay`). It forces the computation to be evaluated, returning the value that was computed. If the computation has already been evaluated, `force` simply returns the cached value.

Here's an example that shows how `delay` and `force` can be used in Scheme:

```
(define x (delay (+ 2 3)))

(display "The value of x has not been computed yet.\n")

(define y (force x))

(display "The value of x has been computed.\n")

(define z (force x))

(display "The value of x has already been computed, so force returns the cached value.\n")

(display y)
(display "\n")
(display z)
(display "\n")
```

In this example, we first define a delayed computation `x` that computes the sum of 2 and 3. We then use `force` to evaluate `x`, which causes the computation to be performed and the value 5 to be returned. We then use `force` again to evaluate `x`, but this time the cached value of 5 is returned immediately without performing the computation again. The output of the program is:

```
The value of x has not been computed yet.
The value of x has been computed.
The value of x has already been computed, so force returns the cached value.
5
5
```

In this example, `delay` creates a promise to compute the value of `(+ 2 3)` and returns a procedure that represents the promise. The computation is not actually performed until `force` is called on `x`. Once `force` is called, the promise is evaluated and the value 5 is returned. Subsequent calls to `force` simply return the cached value of 5.
</details>

Explain how delay and force can be used in Scheme to create delayed list and streams. Provide useful applications of such concepts.

<details>
<summary>Answer</summary>

In Scheme, `delay` and `force` can be used to create delayed lists and streams, which are data structures that allow for lazy evaluation.

A delayed list is a list where the elements are not evaluated until they are needed. This can be useful in situations where the list is very large or where some elements may never be needed. Here is an example of a delayed list in Scheme:

```
(define delayed-list
  (cons 1
    (delay (cons 2
      (delay (cons 3 '()))))))
```

In this example, `delayed-list` is a list containing the elements 1, 2, and 3. The elements 2 and 3 are delayed using `delay`, which creates a promise to evaluate them later when needed. To access the elements of the list, we can use `car` and `cdr`, as we would with a regular list. However, when we access the delayed elements, they are evaluated at that time, using the `force` procedure. For example:

```
(car delayed-list)
; returns 1

(car (force (cdr delayed-list)))
; returns 2
```

A stream is a similar concept to a delayed list, but is typically infinite and can be generated on-the-fly. Here is an example of a stream in Scheme that generates the Fibonacci sequence:

```
(define fib-stream
  (letrec ((fibgen (lambda (a b)
                    (cons a (delay (fibgen b (+ a b)))))))
    (fibgen 0 1)))
```

In this example, `fib-stream` is a stream that generates the Fibonacci sequence. The `letrec` form creates a recursive procedure `fibgen` that generates the sequence. The first element of the sequence is 0, and the second element is 1. Each subsequent element is the sum of the two previous elements. The elements are generated lazily using `delay`, which creates a promise to generate the next element when it is needed.

To access the elements of the stream, we can use `car` and `cdr`, as we would with a regular list. However, the elements are generated on-the-fly using the `force` procedure. For example:

```
(car fib-stream)
; returns 0

(car (force (cdr fib-stream)))
; returns 1

(car (force (cdr (force (cdr fib-stream)))))
; returns 1

(car (force (cdr (force (cdr (force (cdr fib-stream)))))))
; returns 2
```

Delayed lists and streams can be useful in situations where we want to generate a large or infinite amount of data, but don't want to compute it all upfront. This can save memory and processing time. Delayed lists and streams are also useful for implementing certain algorithms, such as infinite sequences and generators.

</details>

Define the term "monad" in the context of functional programming. Explain why monads are useful and provide an example of a monad in Scheme.

<details>
<summary>Answer</summary>

In functional programming, a monad is a design pattern used to encapsulate and compose operations that have side effects or that involve complex control flow. Monads provide a way to abstract away the details of the implementation of these operations, making them easier to reason about and compose.

The main idea behind a monad is to define a set of operations that are associated with a specific context, and to provide a way to sequence these operations while also handling errors and side effects. A monad consists of three components: a type constructor, which defines the context of the monad; a set of operations, which operate on values of this context; and a set of laws, which describe the behavior of the operations and ensure their consistency.

Monads are useful because they provide a structured way to manage side effects and control flow in a functional program. By encapsulating these operations within a monad, programmers can write code that is both more modular and more composable, making it easier to reason about and maintain.

Here's an example of a monad in Scheme, using the `maybe` monad. The `maybe` monad is used to represent computations that may or may not succeed, returning either a value or `#f` to indicate failure.

```scheme
(define (unit x)
  (if (not (eq? x #f))
      (lambda () x)
      #f))

(define (bind m f)
  (if (not (eq? m #f))
      (f (m))
      #f))

(define-syntax maybe
  (syntax-rules ()
    ((maybe expr)
     (bind (unit expr) (lambda (x) x)))
    ((maybe expr fail)
     (bind (unit expr) (lambda (x) (if (eq? x #f) fail x))))))

(define (safe-divide a b)
  (maybe (/ a b) #f))

(define (compute-ratio a b c)
  (maybe (safe-divide a b)
         #f
         (lambda (x) (safe-divide x c))))

(compute-ratio 6 2 3) ; returns 1
(compute-ratio 6 0 3) ; returns #f
(compute-ratio 6 2 0) ; returns #f
```

In this example, the `maybe` monad is implemented using the `unit` and `bind` operations, which allow computations to be sequenced and errors to be handled. The `safe-divide` function returns a `maybe` value representing the result of the division, and the `compute-ratio` function uses the `maybe` monad to compute the ratio of three numbers, handling errors along the way.

</details>

Source: those questions were generated by chatGPT in response to "Could you suggest exam problems for courses using the essentials of programming languages as text?"

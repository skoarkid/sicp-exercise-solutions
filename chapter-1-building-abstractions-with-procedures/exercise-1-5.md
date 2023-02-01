Ben Bitdiddle has invented a test to determine whether the interpreter he is faced with is using applicative-order evaluation or normal-order evaluation. He defines the following two procedures:
```scheme
(define (p) (p))

(define (test x y)
  (if (= x 0)
      0
      y))
```
Then he evaluates the expression
```scheme
(test 0 (p))
```
What behavior will Ben observe with an interpreter that uses applicative-order evaluation? What behavior will he observe with an interpreter that uses normal-order evaluation? Explain your answer. (Assume that the evaluation rule for the special form if is the same whether the interpreter is using normal or applicative order: The predicate expression is evaluated first, and the result determines whether to evaluate the consequent or the alternative expression.)

### `Answer`
Well, what on earth is this procedure p ? It does not take any arguments. It simply references itself. I wonder if there are any practical uses of such a procedure?

Anyways, evaluting (p) would take forever since its definition is a call to itself.

So, in the case of applicative order (where we evaluate the operands before performing the operation), we would have to evaluate (p) and that would run forever.

And in the case of normal order (where we replace the procedures with their defintion and substitute the actual params in place of the formal parameters), we would have something like:
```scheme
(if (= 0 0) 0 (p))
```
Since the question so helpfully tells us to assume that "the special form if is the same whether the interpreter is using normal or applicative order: The predicate expression is evaluated first, and the result determines whether to evaluate the consequent or the alternative expression.", the (= 0 0) is evaluated first to the value #t and the consquent expression is chosen which is '0'. This program terminates in a reasonable amount of time.

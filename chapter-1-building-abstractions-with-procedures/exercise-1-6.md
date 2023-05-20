Alyssa P. Hacker doesn't see why if needs to be provided as a special form. "Why can't I just define it as an ordinary procedure in terms of cond?'' she asks. Alyssa's friend Eva Lu Ator claims this can indeed be done, and she defines a new version of if:

```scheme
(define (new-if predicate then-clause else-clause)

  (cond (predicate then-clause)
        (else else-clause)))
```
Eva demonstrates the program for Alyssa:
```scheme
(new-if (= 2 3) 0 5) 5

(new-if (= 1 1) 0 5) 0
```
Delighted, Alyssa uses new-if to rewrite the square-root program:
```scheme
(define (sqrt-iter guess x)

  (new-if (good-enough? guess x)
          guess
          (sqrt-iter (improve guess x)
                     x)))
```
What happens when Alyssa attempts to use this to compute square roots? Explain.

### `Answer`
When we try to compute square roots with the above procedure, since lisp uses applicative order, it would try to evaluate the operands before performing the operation. So (sqrt-iter 1 2) would evaluate as:
```scheme
(new-if (good-enough? 1 2)
        1
        (sqrt-iter (improve 1 2)
                    2))
```
Next step:
```scheme
(new-if (good-enough? 1 2)
        1
        (sqrt-iter 1.5 2))
```
Next step:
```scheme
(new-if #f 1 (new-if (good-enough? 1.5 2)
            1.5
            (sqrt-iter (improve 1.5 2)
                        2)))
```
And so on till infinity...
In other words, since we evaluate the recursive procedure call before we bother to check if the guess is good enough, we would never stop evaluating.
The special form if is special because it bends the rules a bit...It still works via applicative order but it only evaluates the operands if it needs to. (i.e it evaluates the predicate first and only evaluates its corresponding expression depending on the truth value)

However, I still don't get why we need the special form if per say. We could just use the cond clause in place of it.(without using it do create a user defined procedure)
The cond clause is also a special form that follows the same rules as if - evaluate the predicate first and only evaluate its corresponding expression. I've checked the following implementation and it works perfectly:
```scheme
(define (sqrt-iter guess x)
    (cond ((good-enough? guess x) guess)
        (else (sqrt-iter (improve guess x) x))))
```
I guess if is provided for convenience rather than out of necessity.
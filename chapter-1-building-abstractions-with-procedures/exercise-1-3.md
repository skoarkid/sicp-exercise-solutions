### Define a procedure that takes three numbers as arguments and returns the sum of the squares of the two larger numbers.

### `Answer`
```scheme
 (define (sum-of-square-of-larger-numbers x y z)
    (cond ((and (<= x y) (<= x z)) (+ (* y y) (* z z)))
        ((and (<= y x) (<= y z)) (+ (* x x) (* z z)))
        (else (+ (* x x) (* y y)))))
```
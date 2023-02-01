### Observe that our model of evaluation allows for combinations whose operators are compound expressions. Use this observation to describe the behavior of the following procedure:
```scheme
(define (a-plus-abs-b a b)
  ((if (> b 0) + -) a b))
```

### `Answer`
The effect using a compound expression as an operator allows us to concisely define the behaviour of a procedure based on certain conditions. In this case, the compound expression
```scheme
(if (> b 0) + -)
```
evaluates to '+' if b is positive and '-' otherwise. This operation, when performed on a,b has the overall effect of a + |b| 

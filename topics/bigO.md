# Big O Notation
================

## Simplifying Big O Expressions
--------------------------------

Depending on what you count, the number of operations can be as low as 2n or as high as 5n + 2, but regardless of the exact number, the number of operations grows roughly proportionally with n, if n doubles, the number of operations will also roughly double

#### Constants Don't Matter
O(2n) ==> O(n)
O(500) ==> O(1)
O(13n^2) ==> O(n^2)

O(n + 10) ==> O(n)
O(1000n + 50) ==> O(n)

O(n^2 + 5n + 8) ==> O(n^2)

**Smaller terms** _don't matter_


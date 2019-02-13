# Big O Notation
[Topics](../README.md)

## Definition

An algorithm is **O(f(n))** if the number of simple operations the computer has to do is eventually less than a constant times f(n), as n increases

- f(n) could be linear (f(n) = n)
- f(n) could be quadratic (f(n) = n^2)
- f(n) could be constant (f(n) = 1)
- f(n) could also be (f(n) = log n) || (f(n) = n log n)

## Simplifying Big O Expressions

Depending on what you count, the number of operations can be as low as 2n or as high as 5n + 2, but regardless of the exact number, the _number of operations grows roughly proportionally with n_, if n doubles, the number of operations will also roughly double

**Constants Don't Matter**

    O(2n) ==> O(n)
    O(500) ==> O(1)
    O(13n^2) ==> O(n^2)
    O(n + 10) ==> O(n)
    O(1000n + 50) ==> O(n)
    O(n^2 + 5n + 8) ==> O(n^2)

**Smaller terms** _don't matter_

1. Arithmetic operations are constant `n + 1`
2. Variable assignment is constant `var i = 1`
3. Accessing elements in an array (by index) or object (by key) is constant `arr[0] || obj[key]`
4. In a loop, the time complexity is the length of the loop times the complexity of whatever happens inside of the loop

## Space Complexity

**Time Complexity:** How can we analyze the *runtime* of an algorithm as the size of the inputs increases?

**Space Complexity:** How much *additional memory do we need to allocate in order to run the code in our algorithm?

**Auxiliary Space Complexity:** Space required by the algorithm, not including space taken up by the inputs.

_Space Complexity Rules of Thumb:_

- Most primitives (booleans, numbers, undefined, null) are constant space
- Strings require O(n) space (where n is the string length)
- Reference types are generally O(n), where n is the length (for arrays) or the number of keys (for objects)

## Logarithms

    log2(8) = 3 ---> 2^3 = 8
    log2(value) = exponent ---> 2^exponent = value

The logarithm of a number roughly measures the number of times you can divide that number by 2 **before you get a value that's less than or equal to one.**

Certain searching algorithms have logarithmic time complexity.

Efficient sorting algorithms involve logarithms.

Recursion sometimes involves logarithmic space complexity.

## Recap

We use Big O Notation to **analyze the performance of an algorithm**

Big O Notation can give use a **high level understanding of the time or space complexity of an algorithm**

Big O Notation doesn't care about precision, only general trends (linear, quadratic, constant, etc.)

The time or space complexity measured by Big O depends **only on the algorithm**, not the hardware used to run the algorithm
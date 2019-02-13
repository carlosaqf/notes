# Recursion
[Topics](../README.md)

Recursion is a **process** (a function) that **calls itself**

Recursion is everywhere:

- JSON.parse / JSON.stringify
- document.getElementById and DOM traversal algorithms
- Object traversal
- Common with more complex algorithms
- Sometimes a cleaner alternative to iteration

## How recursive functions work

Invoke the same function with a different input until you reach a base case

*Two essential parts of a recursive function:*

1. **Base Case**: The condition where the recursion ends.
2. Different Input

Recursive function examples

1. 
```Javascript
function countDown(num){
    if(num <= 0){ // base case
        console.log("Done!");
        return;
    }
    console.log(num);
    num--; // different input
    countDown(num);
}
```
2.
```Javascript
function sumRange(num){
    if(num === 1) return 1; // base case
    return num + sumRange(num-1); // different input
}
```

## Pure Recursion

```Javascript
function collectOddValues(arr){
    let newArr = [];

    if(arr.length === 0){
        return newArr;
    }

    if(arr[0] % 2 !== 0){
        newArr.push(arr[0]);
    }

    newArr = newArr.concat(collectOddValues(arr.slice(1)));
    return newArr;
}
```

Tips:

- For arrays, use methods like **slice, the spread opearator**, and **concat** that make copies of arrays so you do not mutate them
- Remember strings are immutable so you will need to use methods like **slice, substr, or substring** to make copies of strings
- To make copies of objects use **Object.assign**, or the **spread operator**

Big O:

- Measure **time complexity** of a recursive function as **the number of recursive calls you need to make** relative to the input
- Measure **space complexity** as the **maximum number of functions on the call stack** at a given time, since the call stack requires memory.

## Tail Call Optimization

- ES2015 allows for _tail call optimization_, where you can make some functions calls without growing the call stack.
- By using the **return** keyword in a specific fashion we can extract output from a function without keeping it on the call stack.

## Recap

- A recursive function is a function that invokes itself
- Recursive functions should **always** have a base case and be invoked with a **different input** each time
- When using recursion, it is essential to return values from one function to another to extract data from each function call
- Helper method recursion is an alternative that allows us to use an external scope in our recursive functions
- Pure recursion eliminates the need for helper method recursion



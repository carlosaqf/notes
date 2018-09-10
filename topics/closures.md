# Closures and Keyword 'This'

A closure is a function that makes use of variables defined in outer functions that have previously returned
```Javascript
function outer(a){
    return function inner(b){
        // the inner function is making use of the variable 'a'
        // which was defined in an outer function called 'outer'
        // and by the time inner is called, that outer function has returned
        // this function called 'inner' is a closure
        return a + b;
    }
}

outer(5)(5); // 10

var storeOuter = outer(5);
storeOuter(10); //15
```
Note:
- We have to `return` the inner function for this to work
- We can either call the inner function right away by using an extra () or we can store the result of the function in a variable
- We DO NOT have to give the inner function a name - we can make it anonymous

### Examples
```Javascript
function outerFn1() {
    var data = "something from outer";
    return function innerFn(){
        return "Just returned from the inner function";
    }
}

function outerFn2(){
    var data = "something from outer";
    return function innerFn(){
        var innerData = "something from inner";
        return data + " " + innerData;
    }
}
```
The function outerFn1 is **NOT A CLOSURE** but outerFn2 **IS** 

- A closure only exists when an inner function makes use of variables defined from an outer function that has returned. If the inner function does not make use of any of the external variables all we have is a nested function.


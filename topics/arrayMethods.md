# Javascript Array Methods

## forEach
- Iterates through an array
- Runs a callback function on each value in the array
- Returns `undefined`

**forEach ALWAYS returns undefined**

```Javascript
[1,2,3].forEach( function(value, index, array){
    //Callback function will be executed 3 times 
    //since there are 3 values in the array
});
```
- Can call the parameters to the callback whatever you want
- Do not always need all three parameters, the order is important 

Example
```Javascript
var arr = [1,2,3];

arr.forEach(function(value, index, array){
    console.log(value);
});

//1
//2
//3
//undefined
```

How it works

- Iterates through an array
- Runs a callback function on each value in the array
- Returns `undefined`
```Javascript
function forEach(array, callback){
    for(var i=0; i < array.length; i++){
        callback(array[i], i, array);
    }
}
```

Using forEach in a function
```javascript
function halfValues(arr){
    var newArr = [];
    arr.forEach(function(val){
        newArr.push(val / 2);
    });
    return newArr;
}

halfValues([2,4,6]); // [1,2,3]
```

## MAP
- Creates a NEW ARRAY
- Iterates through an array
- Runs a callback function for each value in the array
- Adds the result of that callback function to the new array
- Returns the new array

**map ALWAYS returns a NEW ARRAY of the SAME length**

Example
```js
var arr = [1,2,3];

arr.map(function(value, index, array){
    return value * 2;
});

// [2,4,6]
```
How it works

- Creates a new array
- Iterates through an array
- Runs a callback function for each value in the array
- Pushes result of the callback function to the new array
- Returns the new array
```js
function map(array, callback){
    var newArr = [];
    for(var i = 0; i < array.length; i++){
        newArr.push(callback(array[i], i, array));
    }
    return newArr;
}
```
Map in a function
```js
function tripleValues(arr){
    return arr.map(function(value){
        return value * 3;
    });
}
tripleValues([1,2,3]); // [3,6,9]
```

## FILTER
- Creates a new array
- Iterates through an array
- Runs a callback function on each value in the array
- If the callback function returns true, that value will be added to the new array
- If the callback function returns false, that value will be ignored from the new array

**The result of the callback will ALWAYS be a boolean**

Example
```js
var arr = [1,2,3];

arr.filter(function(value, index, array){
    //No need for if statement
    //Just return an expression
    //that evaluates to true or false
    return value > 2;
});
// [3]
```
```js
var instructors = [{name: "Carlos"},
                   {name: "Antonio"},
                   {name: "Quan"},
                   {name: "Fegurgur"}];
instructors.filter(function(value, index, array){
    return value.name.length > 6;
});
// [{name: "Antonio"}, {name: "Fegurgur"}];
```

How it works

- Creates a new array
- Iterates through an array
- Runs a callback function on each value in the array
- If the callback function returns true, that value will be added to the new array
- If the callback function returns FALSE, that value will be ignored from the new array
```js
function filter(array, callback){
    var newArr = [];
    for(var i = 0; i < array.length; i++){
        if(callback(array[i], i, array)){
            newArr.push(array[i]);
        }
    }
    return newArr;
}
```

Filter in a function
```js
function onlyFourLetterNames(arr){
    return arr.filter(function(value){
        return value.length === 4;
    });
}

onlyFourLetterNames(['Rusty', 'Matt', 'Moxie', 'Colt']);
// ['Matt', 'Colt']
```

## REDUCE
- Accepts a callback function and an optional second parameter
- Iterates through an array
- Runs a callback on each value in the array
- The first parameter to the callback is either the first value in the array or the optional second parameter
- The first parameter to the callback is often called "accumulator"
- The returned value from the callback becomes the new value of accumulator

**Whatever is returned from the callback function, becomes the new value of the accumulator!**

```js
[1,2,3].reduce(function(accumulator, nextValue, index, array){
    //Whatever is returned inside here, will be the value of
    //accumulator in the next iteration
}, optional second parameter)
```

```js
var arr = [1,2,3,4,5];

arr.reduce(function(accumulator, nextValue){
    return accumulator + nextValue;
});
```
|accumulator |nextValue |returned value |
|------------|--------- |-------------  |
|1           |2         |3              |
|3           |3         |6              |    
|6           |4         |10             |   
|10          |5         |15             |

Adding a second parameter
```js
var arr = [1,2,3,4,5];

arr.reduce(function(accumulator, nextValue){
    return accumulator + nextValue;
}, 10);
```
|accumulator |nextValue |returned value |
|------------|--------- |-------------  |
|10          |1         |11             |
|11          |2         |13             |
|13          |3         |16             |
|16          |4         |20             |
|20          |5         |25             |

Example using Strings

```js
var names = ['Tim', 'Matt', 'Colt'];

names.reduce(function(accumulator, nextValue){
    return accumulator += ' ' + nextValue;
}, 'The instructors are');
```
|accumulator          |nextValue |returned value                      |
|---------------------|--------- |----------------------------------- |
|'The instructors are'|'Tim'     |'The instructors are Tim'           |
|'The instructors are'|'Matt'    |'The instructors are Time Matt'     |
|'The instructors are'|'Colt'    |'The instructors are Tim Matt Colt' |

Example using Objects
```js
var arr = [5,4,1,4,5];

arr.reduce(function(accumulator, nextValue){
    if(nextValue in accumulator){
        accumulator[nextValue]++;
    }else{
        accumulator[nextValue] = 1;
    }
    return accumulator;
}, {});
```
|accumulator |nextValue |returned value |
|------------|--------- |-------------  |
|{}          |5         |{5:1}          |
|{5:1}       |4         |{5:1, 4:1}     |
|{5:1, 4:1}  |1         |{5:1, 4:1, 1:1}|
|{5:1, 4:1, 1:1} |4     |{5:1, 4:2, 1:1}|
|{5:1, 4:2, 1:1} |5     |{5:2, 4:2, 1:1}|

Reduce in a function
```js
function sumOddNumbers(arr){
    return arr.reduce(function(accumulator, nextValue){
        if(nextValue % 2 !== 0){
            accumulator += nextValue;
        }
        return accumulator;
    }, 0);
}

sumOddNumbers([1,2,3,4,5]); // 9

function createFullName(arr){
    return arr.reduce(function(accumulator, nextValue){
        accumulator.push(nextValue.first + " " + nextValue.last);
        return accumulator;
    }, []);
}

createFullName([{first:"Carlos", last:"Fegurgur"}, {first:"Antonio", last:"Quan"}]);
// ["Carlos Fegurgur", "Antonio Quan"]
```

## RECAP
- forEach iterates over an array, runs a callback on each value and returns undefined
- MAP creates a new array, runs a callback on each value and pushes the result of each callback in the new array
- FILTER creates a new array, runs a callback on each value and if the result of the callback returns true, that value is added to the new array
- SOME iterates through an array and runs a callback on each value, if the callback for at least one value returns true, some returns true, otherwise false
- EVERY iterates through an array and runs a callback on each value, if the callback at any time returns false, every returns false
- REDUCE returns an accumulated value which is determined by the result of what is returned to each callback






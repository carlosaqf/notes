# Data Structures

- Data Structures are collections of values, the relationships among them, and the functions or operations that can be applied to the data
- Different data structures excel at different things. Some are highly specialized, while others are more generally used.
- Working with map/location data? Graph
- Ordered list with fast inserts/removals at the beginning and end? Linked list
- Web scraping nested HTML? Tree
- Scheduler? Binary heap

## Linked Lists
1. [Singly Linked Lists](./singlyLinked.md)
2. [Doubly Linked Lists](./doublyLinked.md)


## ES2015 Class Syntax

What is a class?
- A blueprint for creating objects with pre-defined properties and methods

```Javascript
class Student {
    constructor(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```
The method to create new objects **must** be called constructor

The class keyword creates a constant, so you can not redefine it.

### Creating objects from classes

Use the **new** keyword
```Javascript
class Student {
    constructor(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
}

let firstStudent = new Student("Carlos", "Fegurgur");
let secondStudent = new Student("Antonio", "Quan");
```

### Instance Methods
```Javascript
class Student {
    constructor(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
    fullName(){
        return `Your full name is ${this.firstName} ${this.lastName}`;
    }
}

let firstStudent = new Student("Carlos", "Fegurgur");
firstStudent.fullName()
```

### Class Methods
```Javascript
class Student {
    constructor(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
    fullName(){
        return `Your full name is ${this.firstName} ${this.lastName}`;
    }
    static enrollStudents(...students){
        // some code here
    }
}

let firstStudent = new Student("Carlos", "Fegurgur");
let secondStudent = new Student("Antonio", "Quan");

Student.enrollStudents([firstStudent, secondStudent]);
```

```Javascript
class DataStructure(){
    constructor(){
        // what default properties should it have?
    }
    someInstanceMethod(){
        // what should each object created from this class be able to do?
    }
}
```
### THIS
- Inside all of our **instance** methods and **constructor**, the keyword `this` refers to the _object created from that class_ (also known as an **instance**)

### Recap
- Classes are blueprints that when created make objects known as **instances**
- Classes are created with the **new** keyword
- The **constructor** function is a special function that gets run when the class is instantiated
- Instance methods can be added to class similar to methods in objects
- Class methods can be added using the **static** keyword
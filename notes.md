# Quick notes for js quirks

## 0. Primitives
```
string
number
boolean
null
undefined
symbol (the latest addition)
```

## 1. Object access by key
```
const car = {
  wheels: 4,
  color: "red",
}

console.log(car.wheels);
// 4
console.log(car['color']);
// 'red'
```

## 2. Clone
```
const car = {
  color:'red'
}

const secondCar = Object.assign({}, car)
```

## 3. Array 
### 3.1 Arrays can store js data type
```
var students = ["Mary", 10, "Barbara", 11, "David", 12, "Alex", 11];

var students = [];
```
### 3.2 Array methods
```
const fruitBasket = ['apple','banana','orange']

// length
fruitBasket.length;

// add a new value at the end of the array
fruitBasket.push('pear')
console.log(fruitBasket);
// ["apple", "banana", "orange", "pear"]

// add a new value at the beginning of the array
fruitBasket.unshift('melon')
console.log(fruitBasket);
// ["melon", "apple", "banana", "orange", "pear"]

// remove a value from the end of the array
fruitBasket.pop()
console.log(fruitBasket);
// ["melon", "apple", "banana", "orange"]

// remove a value from the beginning of the array
fruitBasket.shift()
console.log(fruitBasket);
// ["apple", "banana", "orange"]
```

## 4. typeof
```
const str = "hello"
console.log(typeof(str));
// string

const num = 12;
console.log(typeof(num));
// number

const arr = [1,2,3];
console.log(typeof(arr))
// object

const obj = {prop: 'value'};
console.log(typeof(obj));
// object

// this one is buggy, even tho it's primitive it return object
console.log(typeof(null));
// object
```

## 5. logical operators
The logical AND assignment **(x &&= y)** operator only assigns if x is truthy.

The logical OR assignment **(x ||= y)** operator only assigns if x is falsy.

**x ??= y** means y assigns to x only if x is null or undefined.

## 6. === !== vs == !=
good practice to use === and !== since it is more clear intent

The === and !== operators check that both values being compared are equal to (or not equal to) the same type and the same value.

```
var ageOfBill = 10;
var ageOfSally = "10";

console.log(ageOfBill == ageOfSally);
console.log(ageOfBill != ageOfSally);
```

## 7. undefined vs null
Null values intentionally are stored as null to indicate that the variable is empty. You should set a variable equal to null if and only if the variable is expected to have no value.
```
var declaredValue;   => this is undefined
var nothing = null;  => has to be intentially made null
```

## 8. functions
notice we don't do function(var x, var y) or function(x: number, y: number) in js
```
var sum = function(x, y){
  return x + y;
}
```
functions are just variables
```
//functions can be stored in an object as property values
var operations = {
  sum: function(x, y){ return x + y; }, 
  subtract: function(x, y){ return x - y; }, 
  multiply: function(x, y){ return x * y; }, 
  divide: function(x, y){ return x / y; }
};

//functions can be called from an object by accessing a property (dot or bracket)
//and using then the () operator
console.log(operations.multiply(5, 10));
console.log(operations["multiply"](5, 10));
```

## 9. Objects
### 9.1 declaration
```
var student = {
  name: "Mary", 
  age: 10, 
  grades: [90, 88, 95]
}

// interating through property

for(property in student) {
  console.log(property);
}
```

use a function that's basically a 'constructor' that creates objects

The this keyword allows us to create functions that modify the specific instance of the object to which the function is attached.
```
var createStudent = function(name, age) {
  var student = {
    name: name, 
    age: age, 
    birthday: function(){
     this.age++;
    }
  }
  return student;
}

var student1 = createStudent("Mary", 10);
var student2 = createStudent("Michael", 12);

student1.birthday();
console.log(student1.age)
```

### 9.2 Object types
All objects in JavaScript set out as nonspecific groups of data and related functionality. You create instances by utilizing a new operator that is followed by the name of the object type (constructor function).

The easiest way to instantiate objects is the Object() constructor that accepts an optional value as its argument. This value is stored as the wrapped value of the object, and it can be accessed through the valueOf() function.

try to avoid this practice for creating root 'Object'
```
var obj1 = new Object();
var obj2 = new Object(null);
var obj3 = new Object(undefined);
var obj4 = new Object(12.3);
var obj5 = new Object(true);
var obj6 = new Object("Hi");
console.log(obj1.valueOf()); // Object {}
console.log(obj2.valueOf()); // Object {}
console.log(obj3.valueOf()); // Object {}
console.log(obj4.valueOf()); // 12.3
console.log(obj5.valueOf()); // true
console.log(obj6.valueOf()); // Hi

// if you do not pass any arguments, you can ignore brackets
var obj = new Object;
```

### 9.3 Prototypes
```
function Car(manuf, type) {
    this.manufacturer = manuf;
    this.type = type;
}

Car.prototype.wheels = 4;
Car.prototype.getWheels =
    function () {
    return this.wheels;
    }
Car.prototype.name = "Car";

var car1 = new Car("Honda", "CR-V");
var car2 = new Car("BMW", "X5");

console.log("--- Car 1:")
console.log(car1.getWheels());
console.log(car1.name);
console.log(car1.manufacturer);
console.log(car1.type);
console.log("--- Car 2:")
console.log(car2.getWheels());
console.log(car2.name);
console.log(car2.manufacturer);
console.log(car2.type);

--- Car 1:
4
Car
Honda
CR-V
--- Car 2:
4
Car
BMW
X5

```

### 9.4 Object instance methods
```
hasOwnProperty() => indicate if the given property specified in the function argument exists on the object instance (and not prototype)
isPrototypeOf() => checks whether the object specified in the argument is a prototype of another object
propertyIsEnumberable() => indicate if the given property can be enumerated using the for-in statement
toLocaleString() => return a string representation of the object that is appropriate for the locale of execution env
toString() => return a string representation of the object
valueOf() => returns a string, number, or boolean equivalent of the object. It is often returns the same value as toString()
```

## 10. let vs var vs const
var => Variables declared with the var keyword are function scoped, which means that if we declare them inside a for loop (which is a block scope), they will be available even outside of it.
```
for (var i = 0; i < 10; i++) {
  var leak = "I am available outside of the loop";
}

console.log(leak);
// I am available outside of the loop
```
let => Variables declared with the let (and const) keyword are block scoped, meaning that they will be available only inside of the block where they are declared and its sub-blocks.
```
// using `let`
let x = "global";

if (x === "global") {
  let x = "block-scoped";

  console.log(x);
  // expected output: block-scoped
}

console.log(x);
// expected output: global
```
const => Similarly to let, variables declared with const are also block scoped, but they differ in the fact that their value can’t change through re-assignment and can’t be re-declared.
```
const constant = 'I am a constant';
constant = " I can't be reassigned";

// Uncaught TypeError: Assignment to constant variable
```

### 10.1 temporal dead space
var can be accessed before they're assigned. the value just won't exist
```
console.log(i);
var i = "I am a variable";

//  expected output: undefined
```

### 10.2 best practice opinions
i like option 1
```
Use const by default
Use let only if rebinding is needed.
var should never be used in ES6.
```
or
```
Use var for top-level variables that are shared across many (especially larger) scopes.
Use let for localized variables in smaller scopes.
Refactor let to const only after some code has to be written, and you’re reasonably sure that you’ve got a case where there shouldn’t be variable reassignment.
```

## 11. Arrow function
anoynomous functions same as c#

```
const greeting = function(name) {
  console.log("hello " + name);
}
```
vs 
```
var greeting = (name) => {
  console.log(`hello ${name}`);
}
```
variations with 1 param and no param
```
var greeting = name => {
  console.log(`hello ${name}`);
}
```
```
var greeting = () => {
  console.log(`hello ${name}`);
}
```
When you use an arrow function, the **this** keyword is inherited from the parent scope.
This can be useful in cases like this one:
```
document.addEventListener("DOMContentLoaded", function () {
  const box = document.querySelector(".box");
// listen for a click event
box.addEventListener("click", function() {
  // toggle the class opening on the div
  this.classList.toggle("opening");
  setInterval(function(){
    // try to toggle again the class
    this.classList.toggle("opening");
    },500);
});
});
```

avoid arrow functions when dealing with tricky this.
eg.1
```
const button = document.querySelector("btn");
button.addEventListener("click", () => {
  // error: *this* refers to the `Window` Object
  this.classList.toggle("on");
})
```
eg.2
```
const person1 = {
  age: 10,
  grow: function() {
    this.age++;
    console.log(this.age);
  }
}

person1.grow();
// 11

const person2 = {
  age: 10,
  grow: () => {
    // error: *this* refers to the `Window` Object
    this.age++;
    console.log(this.age);
  }
}

person2.grow();
```
eg.3 arguments
```
Another difference between arrow functions and normal functions is the access to the arguments object. The arguments object is an array-like object that we can access from inside functions and contains the values of the arguments passed to that function.

A quick example:

function example(){
  console.log(arguments[0])
}

example(1,2,3);
// 1
```
arrow function inherits arguments object from parent, which doesn't exist here    
```
 const showWinner = () => {
  const winner = arguments[0];
  console.log(`${winner} was the winner`)
}

showWinner( "Usain Bolt", "Justin Gatlin", "Asafa Powell" )

// would have to do it this way

const showWinner = (...args) => {
  const winner = args[0];
  console.log(`${winner} was the winner`)
}
showWinner("Usain Bolt", "Justin Gatlin", "Asafa Powell" )
// "Usain Bolt was the winner"
```
# Quick notes for js quirks

- [Quick notes for js quirks](#quick-notes-for-js-quirks)
  - [0. Primitives](#0-primitives)
  - [1. Object access by key](#1-object-access-by-key)
  - [2. Clone](#2-clone)
  - [3. Array](#3-array)
    - [3.1 Arrays can store js data type](#31-arrays-can-store-js-data-type)
    - [3.2 Array methods](#32-array-methods)
  - [4. typeof](#4-typeof)
  - [5. logical operators](#5-logical-operators)
  - [6. === !== vs == !=](#6---vs--)
  - [7. undefined vs null](#7-undefined-vs-null)
  - [8. functions](#8-functions)
  - [9. Objects](#9-objects)
    - [9.1 declaration](#91-declaration)
    - [9.2 Object types](#92-object-types)
    - [9.3 Prototypes](#93-prototypes)
    - [9.4 Object instance methods](#94-object-instance-methods)
  - [10. let vs var vs const](#10-let-vs-var-vs-const)
    - [10.0](#100)
    - [10.1 temporal dead space](#101-temporal-dead-space)
    - [10.2 best practice opinions](#102-best-practice-opinions)
  - [11. Arrow function](#11-arrow-function)
    - [Default arguments](#default-arguments)
  - [12. string methods](#12-string-methods)
  - [13. regex](#13-regex)
  - [14. Object notation](#14-object-notation)
    - [14.1 serialize](#141-serialize)
    - [14.2 parse (deserialize)](#142-parse-deserialize)
  - [15. function can return functions](#15-function-can-return-functions)
  - [16. Closures](#16-closures)
    - [16.1 this](#161-this)
    - [16.2 anonymous function issue (this scoping)](#162-anonymous-function-issue-this-scoping)
    - [16.3 unexpected behavior with closure in anonymous functions](#163-unexpected-behavior-with-closure-in-anonymous-functions)
    - [remove object property (Delete construct)](#remove-object-property-delete-construct)
  - [17. Modularity](#17-modularity)
  - [18. Spread operator](#18-spread-operator)
    - [18.1 spread combine arrays](#181-spread-combine-arrays)
    - [18.2 function param spread](#182-function-param-spread)
    - [18.3 object spread](#183-object-spread)
    - [18.4 Rest parameter spread](#184-rest-parameter-spread)
  - [19. Classes](#19-classes)
    - [19.1 set/get](#191-setget)
    - [19.2 extending class](#192-extending-class)
    - [19.3 extending arrays](#193-extending-arrays)
  - [20. Promises](#20-promises)
    - [20.1 chaining promise](#201-chaining-promise)
    - [20.2 Promise.resolve / Promise.reject](#202-promiseresolve--promisereject)
    - [20.3 Promise.all / Promise.race](#203-promiseall--promiserace)
    - [20.4 Promise.race](#204-promiserace)
    - [20.5 async await](#205-async-await)
  - [21. Generators](#21-generators)
  - [22. Array operators](#22-array-operators)
    - [22.1 Map](#221-map)
    - [22.2 Filter](#222-filter)
    - [22.3 Reduce](#223-reduce)
  - [23. Higher order functions](#23-higher-order-functions)
  - [24. Pure function](#24-pure-function)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


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

### 10.0
loop through properties
```
const person = {fname:"John", lname:"Doe", age:25};

let text = "";
for (let x in person) {
  text += person[x];
}
```

loop through array
```
Do not use for in over an Array if the index order is important.
The index order is implementation-dependent, and array values may not be accessed in the order you expect.
It is better to use a for loop, a for of loop, or Array.forEach() when the order is important.

for (variable in array) {
  code
}
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

### Default arguments
```
function calculatePrice(total, tax = 0.1, tip = 0.05){
  console.log(total + (total * tax) + (total * tip));
}
// In this case 0.15 will be bound to the tip
calculatePrice(100, undefined, 0.15)
```

a nicer way is to just pass in default object. With destructuring we can write this:

By writing = {} we default our argument to an Object and no matter what argument we pass in the function, it will be an Object:
```
function calculatePrice({
  total = 0,
  tax = 0.1,
  tip = 0.05} = {} ){
  console.log(total + (total * tax) + (total * tip));
}

const bill = calculatePrice({ tip: 0.15, total:150 });
// 187.5
```
destructure errors
```
function calculatePrice({
  total = 0,
  tax = 0.1,
  tip = 0.05}){
  return total + (total * tax) + (total * tip);
}
calculatePrice({});
// cannot destructure property `total` of 'undefined' or 'null'.
calculatePrice();
// cannot destructure property `total` of 'undefined' or 'null'.
calculatePrice(undefined)
// cannot destructure property `total` of 'undefined' or 'null'.
```

## 12. string methods
```
const str = "this is a short sentence";
console.log(str.indexOf("short"));
// Output: 10

const str = "pizza, orange, cereals"
console.log(str.slice(0, 5));
// Output: "pizza"

const str = "i ate an apple"
console.log(str.toUpperCase());
// Output: "I ATE AN APPLE"

const str = "I ATE AN APPLE"
console.log(str.toLowerCase());
// Output: "i ate an apple"

const code = "ABCDEFG";
console.log(code.startsWith("ABC"));
// true

const code = "ABCDEFGHI"
console.log(code.startsWith("DEF",3));
// true, it will begin checking after 3 characters

const code = "ABCDEF";
console.log(code.endsWith("DEF"));
// true

const code = "ABCDEFGHI"
console.log(code.endsWith("EF", 6));
// true, 6 means that we consider only the first 6 values ABCDEF, and yes this string ends with EF therefore we get *true*

const code = "ABCDEF"
console.log(code.includes("CDE"));
// true

let hello = "Hi";
console.log(hello.repeat(10));
// "HiHiHiHiHiHiHiHiHiHi"
```

## 13. regex
```
var pattern = /[A-Z]{3}-\d{3}/gi;

or

// RegExp constructor
// arguments: pattern; flags
var pattern = new RegExp("[A-Z]{3}-\\d{3}", "gi");
```

## 14. Object notation
js understand json natively
```
    var order = {
      "date": "11/20/2013",
      "customerId": 116,
      "items": [
        {
          "product": "Surface 4 Pro",
          "unitprice": "799",
          "amount": 1
        },
        {
          "product": "Type Cover 4",
          "unitprice": "129",
          "amount": 1
        },
        {
          "product": "Docking station",
          "unitprice": "199",
          "amount": 1
        }
      ]
    }
```

### 14.1 serialize
```
var orderJson = JSON.stringify(order, null, "  ");
console.log(orderJson);
```

### 14.2 parse (deserialize)
```
var order = JSON.parse(orderString);
```

## 15. function can return functions
```
var kind = "subtract";
var op = createOperation(kind);
console.log(op(35, 23)); // 12

function createOperation(kind) {
  if (kind == "add") {
    return function (a, b) {
      return a + b;
    };
  }
  else {
    return function (a, b) {
      return a - b;
    };
  }
}
```

## 16. Closures
A function that is defined inside another function adds the containing function’s activation object into its scope chain. This ensures that the internal function has access to the variables of the containing function. So, in createOp, the returned function’s scope chain includes the activation object for createOp. When the console.log() operation invokes the anonymous function through addOp, the execution context of addOp looks like as shown in the image below.
```
var addOp = createOp("add");
    var subtractOp = createOp("subtract");

    console.log(addOp(23, 12));      // 35
    console.log(subtractOp(23, 12)); // 11

    function createOp(kind) {
      return function (a, b) {
        if (kind == "add") {
          return a + b;
        }
        else if (kind == "subtract") {
          return a - b;
        }
      }
    }
```

### 16.1 this 
The this object is bound at run time based on the context in which a function is executed. When called in an object method, this equals the object you invoke the method on. In the constructor function, this represents the execution context of the object just being created. When used inside global functions, this is equal to the window object, which you’ll learn about soon.

### 16.2 anonymous function issue (this scoping)
They are not bound to an object when you invoke them…

```
var type = "Mercedes";

var myCar = {
  type: "BMW",

  getType: function () {
    return this.type;
  },

  getTypeFuncion: function () {
    return function () {
      return this.type;   // this anoynmous function will return global type
    }
  }
};

console.log(myCar.getType());
console.log(myCar.getTypeFuncion()());

BMW
Mercedes
```

### 16.3 unexpected behavior with closure in anonymous functions
The anonymous function is evaluated when it is invoked and using the execution context it resolves the value of i, using the context’s scope chain. When you call giveMeFunctions(), the i variable is set to 3 at the time it returns.

As you iterate through the elements in the returned function array, the i*i expression is evaluated using the value of i, which happens to be 3 each time. That is why you see only nines in the output. There is a quick fix for this issue.

```
  function giveMeFunctions() {
    var functions = [];
    for (var i = 0; i < 3; i++) {
      functions[i] = function () {
        return i * i;
      }
    }
    return functions;
  }

  var myFunctions = giveMeFunctions();
  for (var i = 0; i < myFunctions.length; i++) {
    console.log(i + ": " + myFunctions[i]());
  }

0: 9
1: 9
2: 9
```

```
function giveMeFunctions() {
  var functions = [];
  for (var i = 0; i < 3; i++) {
    functions[i] = function (arg) {
      return function () {
        return arg * arg;
      }
    }(i);
  }
  return functions;
}

0: 0
1: 1
2: 4
```

### remove object property (Delete construct)
```
var myObject = new Object();
myObject.intProp = 23;
myObject.strProp = "Hi!";

console.log(myObject.intProp); // 23
console.log(myObject.strProp); // Hi!

delete myObject.intProp;

console.log(myObject.intProp); // undefined
console.log(myObject.strProp); // Hi!
```

## 17. Modularity
js does not have a concept of modules, but most developers use the module pattern that mimics the behavior of modules in other programming languages.
```
var CircleOps = (function () {
  // --- Private stuff
  return {
    // --- Public stuff
  };
})();
```

## 18. Spread operator 
### 18.1 spread combine arrays
```
const veggie = ["tomato","cucumber","beans"];
const meat = ["pork","beef","chicken"];

const menu = [...veggie, "pasta", ...meat];
console.log(menu);
// Array [ "tomato", "cucumber", "beans", "pasta", "pork", "beef", "chicken" ]
```
copy
```
const veggie = ["tomato","cucumber","beans"];
// we created an empty array and put the values of the old array inside of it
const newVeggie = [].concat(veggie);
veggie.push("peas");
console.log(veggie);
// Array [ "tomato", "cucumber", "beans", "peas" ]
console.log(newVeggie);
// Array [ "tomato", "cucumber", "beans" ]
```
spread syntax copy
```
const veggie = ["tomato","cucumber","beans"];
const newVeggie = [...veggie];
veggie.push("peas");
console.log(veggie);
// Array [ "tomato", "cucumber", "beans", "peas" ]
console.log(newVeggie);
// Array [ "tomato", "cucumber", "beans" ]
```

### 18.2 function param spread
```
// OLD WAY
function doStuff (x, y, z) {
  console.log(x + y + z);
 }
var args = [0, 1, 2];

// Call the function, passing args
doStuff.apply(null, args);

// USE THE SPREAD SYNTAX

doStuff(...args);
// 3 (0+1+2);
console.log(args);
// Array [ 0, 1, 2 ]
```
if we pass in more, extras are ignored
```
const name = ["Jon", "Paul", "Jones"];

function greet(first, last) {
  console.log(`Hello ${first} ${last}`);
}
greet(...name);
// Hello Jon Paul
```

### 18.3 object spread
```
let person = {
  name : "Alberto",
  surname: "Montalesi",
  age: 25,
}

let clone = {...person};
console.log(clone);
// Object { name: "Alberto", surname: "Montalesi", age: 25 }
```

### 18.4 Rest parameter spread
this one will **condense**
```
const runners = ["Tom", "Paul", "Mark", "Luke"];
const [first,second,...losers] = runners;

console.log(...losers);
// Mark Luke
```

## 19. Classes
synatical sugar over js' prototype-based inheritance

prototype
```
function Person(name,age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function(){
  console.log("Hello, my name is " + this.name);
}

const alberto = new Person("Alberto", 26);
const caroline = new Person("Caroline",26);

alberto.greet();
// Hello, my name is Alberto
caroline.greet();
// Hello, my name is Caroline
```
class way
```
class Person {
  constructor(name,age){
    this.name = name;
    this.age = age;
  }
  greet(){
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old` );
  } // no commas in between methods
  farewell(){
    console.log("goodbye friend");
  }
}

const alberto = new Person("Alberto",26);

alberto.greet();
// Hello, my name is Alberto and I am 26 years old
alberto.farewell();
// goodbye friend
```

static methods

incorrect way
```
class Person {
  constructor(name,age){
    this.name = name;
    this.age = age;
  }
  static info(){
    console.log("I am a Person class, nice to meet you");
  }
}

const alberto = new Person("Alberto",26);

alberto.info();
// TypeError: alberto.info is not a function
```
correct way
```
class Person {
  constructor(name,age){
    this.name = name;
    this.age = age;
  }
  static info(){
    console.log("I am a Person class, nice to meet you");
  }
}
const alberto = new Person("Alberto",26);
Person.info();
// I am a Person class, nice to meet you
```

### 19.1 set/get
```
class Person {
  constructor(name,surname) {
    this.name = name;
    this.surname = surname;
    this.nickname = "";
  }
  set nicknames(value){
    this.nickname = value;
    console.log(this.nickname);
  }
  get nicknames(){
     console.log(`Your nickname is ${this.nickname}`);
  }
}

const alberto = new Person("Alberto","Montalesi");

// first we call the setter
alberto.nicknames = "Albi";
// "Albi"

// then we call the getter
alberto.nicknames;
// "Your nickname is Albi"
```
### 19.2 extending class
```
// our initial class
class Person {
  constructor(name,age){
    this.name = name;
    this.age = age;
  }
  greet(){
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old` );
  }
}


// our new class
class Adult extends Person {
  constructor(name,age,work){
    super(name,age);     // must call super or will error
    this.work = work;
  }
}
const alberto = new Adult("Alberto",26,"software developer");
```

### 19.3 extending arrays
classes can extend array
```
class Classroom extends Array {
  // we use rest operator to grab all the students
  constructor(name, ...students){
    // we use spread to place all the students in the array individually otherwise we would push an array into an array
    super(...students);
    this.name = name;
    // we create a new method to add students
  }
  add(student){
    this.push(student);
  }
}
const myClass = new Classroom('1A',
  {name: "Tim", mark: 6},
  {name: "Tom", mark: 3},
  {name: "Jim", mark: 8},
  {name: "Jon", mark: 10},
);

// now we can call
myClass.add({name: "Timmy", mark:7});
myClass[4];
// Object { name: "Timmy", mark: 7 }

// we can also loop over with for of
for(const student of myClass) {
  console.log(student);
  }
// Object { name: "Tim", mark: 6 }
// Object { name: "Tom", mark: 3 }
// Object { name: "Jim", mark: 8 }
// Object { name: "Jon", mark: 10 }
// Object { name: "Timmy", mark: 7 }
```

## 20. Promises
**avoid call back hell**
```
const makePizza = (ingredients, callback) => {
    mixIngredients(ingredients, function(mixedIngredients)){
      bakePizza(mixedIngredients, function(bakedPizza)){
        console.log('finished!')
      }
    }
}
```

use **promises** instead

We use .then() to grab the value when the promise resolves and .catch() when the promise rejects.

```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
      resolve("The value we get from the promise");
    }, 2000);
});

myPromise.then(
  data => {
    console.log(data);
  });
// after 2 seconds ...
// The value we get from the promise
console.log("hello");

hello
The value we get from the promise
```
```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
      reject(Error("this is our error"));
    }, 2000);
});

myPromise
  .then(data => {
    console.log(data);
  })
  .catch(err => {
    console.error(err);
  })
  // Error: this is our error
  // Stack trace:
  // myPromise</<@debugger eval code:3:14
```

### 20.1 chaining promise
We can chain promises one after the other, using what was returned from the previous one as the base for the subsequent one, whether the promise was resolved or rejected.

You can chain as many promises as you want and the code will still be more readable / shorter than callbacks
```
const myPromise = new Promise((resolve, reject) => {
  resolve();
});

myPromise
  .then(data => {
    // return something new 
    return 'working...'
  })
  .then(data => {
    // log the data that we got from the previous promise
    console.log(data);

    throw 'failed!';
  })
  .catch(err => {
    // grab the error from the previous promise and log it
    console.error(err);
    // failed!
  })
```

### 20.2 Promise.resolve / Promise.reject
Promise.resolve() and Promise.reject() will create promises that automatically resolve or reject.

```
//Promise.resolve()
Promise.resolve('Success').then(function(value) {
  console.log(value);
  // "Success"
}, function(value) {
  // not called
});

// Promise.reject()
Promise.reject(new Error('fail')).then(function() {
  // not called
}, function(error) {
  console.log(error);
  // Error: fail
});
```

### 20.3 Promise.all / Promise.race
Promise.all() returns a single Promise that resolves when all promises have resolved.
```
const promise1 =  new Promise((resolve,reject) => {
  setTimeout(resolve, 500, 'first value');
});
const promise2 =  new Promise((resolve,reject) => {
  setTimeout(resolve, 1000, 'second value');
});

Promise
  .all([promise1, promise2])
  .then(data => {
    const[promise1data, promise2data] = data;
    console.log(promise1data, promise2data);
  });
// after 1000 ms
// first value second value
```

If one of the promises was rejected, then all of them would asynchronously reject with the value of that rejection even if they resolved.

```
const promise1 =  new Promise((resolve,reject) => {
  resolve("my first value");
});
const promise2 =  new Promise((resolve,reject) => {
  reject(Error("oooops error"));
});

// one of the two promises will fail, but `.all` will return only a rejection.
Promise
  .all([promise1, promise2])
  .then(data => {
    const[promise1data, promise2data] = data;
    console.log(promise1data, promise2data);
  })
  .catch(err => {
    console.log(err);
  });
  // Error: oooops error
```

### 20.4 Promise.race
returns a promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects with the value from that promise.
```
const promise1 =  new Promise((resolve,reject) => {
  setTimeout(resolve, 500, 'first value');
});
const promise2 =  new Promise((resolve,reject) => {
  setTimeout(resolve, 100, 'second value');
});

Promise.race([promise1, promise2]).then(function(value) {
  console.log(value);
  // Both resolve, but promise2 is faster
});
// expected output: "second value"
```
### 20.5 async await

```
async function example() {
  const myPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("The value we get from the promise");
      }, 2000);
  });

  await myPromise();
}
```
## 21. Generators
a) we declared the function using function*

b) we used the keyword yield before our content

c) we start our function using .next()

d) the last time we call .next() we receive and empty object and we get done: true

e) Our function is paused between each .next() call.
```
function* fruitList(){
  yield 'Banana';
  yield 'Apple';
  yield 'Orange';
}

const fruits = fruitList();

fruits;
// Generator
console.log(fruits.next());
// Object { value: "Banana", done: false }
console.log(fruits.next());
// Object { value: "Apple", done: false }
console.log(fruits.next());
// Object { value: "Orange", done: false }
console.log(fruits.next());
// Object { value: undefined, done: true }
```
looping over generator
```
// create an array of fruits
const fruitList = ['Banana','Apple','Orange','Melon','Cherry','Mango'];

// create our looping generator
function* loop(arr) {
  for (const item of arr) {
    yield `I like to eat ${item}s`;
  }
}

const fruitGenerator = loop(fruitList);
console.log(fruitGenerator.next());
// Object { value: "I like to eat Bananas", done: false }
console.log(fruitGenerator.next());
// Object { value: "I like to eat Apples", done: false }
console.log(fruitGenerator.next().value);
// "I like to eat Oranges"
```
Using .return() we can return a given value and finish the generator.

```
function* fruitList(){
  yield 'Banana';
  yield 'Apple';
  yield 'Orange';
}

const fruits = fruitList();

console.log(fruits.return());
// Object { value: undefined, done: true }
```

catch error with throw
```
function* gen(){
  try {
    yield "Trying...";
    yield "Trying harder...";
    yield "Trying even harder..";
  }
  catch(err) {
    console.log("Error: " + err );
  }
}

const myGenerator = gen();
console.log(myGenerator.next());
// Object { value: "Trying...", done: false }
console.log(myGenerator.next());
// Object { value: "Trying harder...", done: false }
console.log(myGenerator.throw("ooops"));
// Error: ooops
// Object { value: undefined, done: true }
```
combine with Promise
```
const myPromise = () => new Promise((resolve) => {
  resolve("our value is...");
});

function* gen() {
  let result = "";
  // returns promise
  yield myPromise().then(data => { result = data }) ;
  // wait for the promise and use its value
  yield result + ' 2';
};

// Call the async function and pass params
const asyncFunc = gen(); 
const val1 = asyncFunc.next();
console.log(val1);
// call the promise and wait for it to resolve
// {value: Promise, done: false}
val1.value.then(() => {
  console.log(asyncFunc.next());
})
// Object { value: "our value is... 2", done: false }
```

## 22. Array operators
### 22.1 Map
```
const numbers = [1, 5, 10, 15];
// The associated function multiply each array number by 2
const doubles = numbers.map(x => x * 2);

console.log(numbers); // [1, 5, 10, 15] (no change)
console.log(doubles); // [2, 10, 20, 30]
```
### 22.2 Filter
```
const numbers = [1, 5, 10, 15];
// Keep only the number greater than or equal to 10
const bigOnes = numbers.filter(x => x >= 10);
```
### 22.3 Reduce
```
const numbers = [1, 5, 10, 15];
// Compute the sum of array elements
const sum = numbers.reduce((acc, value) => acc + value, 0);
```

## 23. Higher order functions
functions are first class in js (treated same as other types)

A function that takes another function as a parameter or returns another function is called a higher-order function.
```
const titles = movies => movies.map(movie => movie.title);
const byNolan = movie => movie.director === "Christopher Nolan";
const filter = (movies, func) => movies.filter(func);
const goodRating = movie => movie.imdbRating >= 7.5;
const ratings = movies => movies.map(movie => movie.imdbRating);
const average = array => array.reduce((sum, value) => sum + value, 0) / array.length;
```

## 24. Pure function
A pure function is a function that has the following characteristics:

* Its outputs depend solely on its inputs
* It has no side effect


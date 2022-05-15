- [1. DOM api](#1-dom-api)
  - [1.1 document.querySelector(selector)](#11-documentqueryselectorselector)
  - [1.2 modifying innerHTML](#12-modifying-innerhtml)
  - [1.3 element.id](#13-elementid)
  - [1.4 modifying outerHTML](#14-modifying-outerhtml)
  - [1.5 document.getElementById(id)](#15-documentgetelementbyidid)
  - [1.6 document.querySelectorAll(selector)](#16-documentqueryselectorallselector)
  - [1.7 document.getElementsByTagName](#17-documentgetelementsbytagname)
  - [1.8 iterating through doms (cannot use forEach because it's not an Array)](#18-iterating-through-doms-cannot-use-foreach-because-its-not-an-array)
- [2. Add / Remove elementd](#2-add--remove-elementd)
  - [2.1 createElement(element)](#21-createelementelement)
  - [2.2 removeElement](#22-removeelement)
- [3 modifying element attributes](#3-modifying-element-attributes)
  - [3.1 getAttributeNames()](#31-getattributenames)
  - [3.2 getAttributeName(name)](#32-getattributenamename)
  - [3.3 setAttribute(name, value) / removeAttribute(name)](#33-setattributename-value--removeattributename)
  - [3.4 changing element's style](#34-changing-elements-style)
- [4. event listeners](#4-event-listeners)
  - [4.1 onClicked](#41-onclicked)
  - [4.2 using .this with object](#42-using-this-with-object)
  - [4.3 more mouse events](#43-more-mouse-events)
  - [4.4 keyboard events](#44-keyboard-events)
  - [4.5 form events](#45-form-events)
  - [4.6 checkbox on change, check if it's checked](#46-checkbox-on-change-check-if-its-checked)
- [5. modify css](#5-modify-css)
  - [5.1 add multiple css with classList](#51-add-multiple-css-with-classlist)
  - [5.2 remove classList](#52-remove-classlist)
  - [5.3 check if classList contains class value](#53-check-if-classlist-contains-class-value)
  - [5.4 replace classList](#54-replace-classlist)
  - [5.5 toggle classList](#55-toggle-classlist)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## 1. DOM api
The DOM API allows full control, both querying and altering the DOM, and you have practically full support in the API to leverage all features provided by the HTML markup.

full list here

https://developer.mozilla.org/en-US/docs/Web/API/Element

### 1.1 document.querySelector(selector)
return the first element it finds with the selector provided. If no element is found using that particular selector, the function will return as null.
```
<html>
 <head>
   <title>Capturing DOM Nodes with querySelector</title>
 </head>
 <body>
   <h1>Hello, World!</h1>
 </body>
</html>
```
```
var h1 = document.querySelector('h1');
```
### 1.2 modifying innerHTML
innerHTML stores the HTML contents stored between the <h2> opening and </h2> closing tags:
```
// Write code here!
var p = document.querySelector("p");
p.innerHTML = "helloworld";
```
### 1.3 element.id
Use Element.id to return the value of the element node’s id attribute.

```
 <body>
   <h1 id="logo">Learn DOM Manipulation with Javascript</h1>
 </body>

var h1 = document.querySelector('h1');
console.log("h1 element's id value:", h1.id);
```

### 1.4 modifying outerHTML
Element.outerHTML returns a string-like value that contains both the content of the HTML element and its opening/closing tags.
```
var h1 = document.querySelector('h1');
console.log("h1 element:", h1.outerHTML);
```

### 1.5 document.getElementById(id)

```
<html>
 <head>
   <title>Accessing an Element Node using ID's</title>
 </head>
 <body>
   <h1 id="mainHeading">Learn DOM Manipulation with Javascript</h1>
 </body>
</html>

var mainHeading = document.getElementById('mainHeading');
mainHeading.innerHTML = "Access an element with an id attribute using <code>document.getElementById()</code>";
```

### 1.6 document.querySelectorAll(selector)
```
<html>
 <head>
   <title>Accessing Multiple Element Nodes</title>
 </head>
 <body>
   <h1>To-Do Items</h1>
   <ul id="todos">
     <li>Get groceries</li>
     <li>Go for a run</li>
     <li>Learn web development</li>
   </ul>
 </body>
</html>

var todoItems = document.querySelectorAll('#todos > li');

for(var i = 0; i < todoItems.length; i++) {
  todoItems[i].innerHTML = "Todo Item #" + (i+1);
}
```

### 1.7 document.getElementsByTagName
return an array-like object with all the elements that match the tag name you place in the argument:
```
<html>
 <head>
   <title>Getting elements by tag name.</title>
 </head>
 <body>
   <h1>Heading 1</h1>
   <p>Paragraph 1</p>
   <h1>Heading 2</h1>
   <p>Paragraph 2</p>
   <h1>Heading 3</h1>
   <p>Paragraph 3</p>
 </body>
</html>

var headings = document.getElementsByTagName('h1');
var paragraphs = document.getElementsByTagName('p');

for(var i = 0; i < headings.length; i++){
  headings[i].style.color = "green";
}

for(var i = 0; i < paragraphs.length; i++){
  paragraphs[i].style.color = "blue";
}
```
### 1.8 iterating through doms (cannot use forEach because it's not an Array)

## 2. Add / Remove elementd
### 2.1 createElement(element)
```
<html>
 <head>
   <title>Creating New Elements</title>
 </head>
 <body>
   <div id="content"></div>
 </body>
</html>

var h1 = document.createElement('h1');
h1.innerHTML = "A new HTML element!";

// this by default won't show up. we have to attach it to another element first
var content = document.querySelector('#content');
content.appendChild(h1);
```

### 2.2 removeElement
```
<html>
 <head>
   <title>Removing HTML Elements</title>
 </head>
 <body>
   <div id="content">
     <h1>Removing an HTML Element</h1>
     <p>This element will be removed.</p>
   </div>
 </body>
</html>

var content = document.querySelector('#content');
var contentParagraph = document.querySelector('#content > p');

var oldElement = content.removeChild(contentParagraph);
console.log(oldElement.innerHTML);
```

## 3 modifying element attributes

### 3.1 getAttributeNames()
get an array containing the names of the HTML element’s attributes.
```
<html>
 <head>
   <title>Javascript + HTML Attributes</title>
 </head>
 <body>
   <h1 id="logo">Learn DOM Manipulation with Javascript</h1>
   <label for="question">What do you want to learn about the DOM?</label>
   <input type="text" name="question" id="question" placeholder="Insert Question Here">
 </body>
</html>

var h1 = document.querySelector('h1');
var input = document.querySelector('input[type=text]');

console.log("input attributes:", input.getAttributeNames());

input attributes:
[4 items
0:"type"
1:"name"
2:"id"
3:"placeholder"
]
```

### 3.2 getAttributeName(name)
```
var h1 = document.querySelector('h1');
var input = document.querySelector('input[type=text]');

console.log("input type:", input.getAttribute('type'));
```

### 3.3 setAttribute(name, value) / removeAttribute(name)
```
var h1 = document.querySelector('h1');
var input = document.querySelector('input[type=text]');

input.setAttribute('type', "checkbox");
input.removeAttribute('placeholder');

console.log(input.getAttributeNames());
```

### 3.4 changing element's style
style.color example
```
// random color generator 
var randomColor = function(){
  var rvalue = function() {
  	return Math.round(Math.random()*255); 
  }

 	return 'rgb(' + rvalue() + "," + rvalue() + "," + rvalue() + ")";
}

// get button element from DOM
var button = document.querySelector('button');

// create event listener to change color on button click
button.onclick = function(){
	button.style.color = randomColor();
}
```

## 4. event listeners
every interaction user have with a page (e.g. a mouse click, scrolling, window resizing, etc.) is recorded as a series of events.

### 4.1 onClicked
```
var button = document.querySelector('button');
var body = document.querySelector('body');
button.onclick = function() {
  var p = document.createElement('p');
  p.innerHTML = 'Clicked!';
  body.appendChild(p);
}
```

### 4.2 using .this with object

since button is an object, this.style affect's the button.
```
// random color generator 
var randomColor = function(){
  var rvalue = function() {
  	return Math.round(Math.random()*255); 
  }

 	return 'rgb(' + rvalue() + "," + rvalue() + "," + rvalue() + ")";
}

// get button element from DOM
var button = document.querySelector('button');

// create event listener to change background color on button click
button.onclick = function(){
	this.style.backgroundColor = randomColor();
}
```

### 4.3 more mouse events
events occur with a user's mouse
* ondblclick: occurs when an element is double clicked
* onmouseenter: occurs when the mouse pointer moves onto an element
* onmouseleave: occurs when the mouse pointer moves away from an element
```
<html>
  <head>
    <title>Exercise: DOM manipulations using onclick event listener</title>
  </head>
  <body>
    <button type="button">Click Me!</button>
  </body>
</html>


var button = document.querySelector('button');

button.onmouseenter = function(){
  this.innerHTML = "Mouse entered!";
}

button.onmouseleave = function(){
  this.innerHTML = "Mouse left!";
}

button.ondblclick = function(){
  this.innerHTML = "Double clicked!!";
}
```

### 4.4 keyboard events
keypresses on the user’s keyboard
* onkeypress: occurs when a key is pressed on the user’s keyboard
* onkeydown: occurs when a user is pressing down on a key
* onkeyup: occurs when a user releases a key press
```
<html>
  <head>
    <title>Keyboard Events</title>
  </head>
  <body>
    <p>Click into the window and press a key.</p>
    <h1>Key Down:</h1>
  </body>
</html>

var h1 = document.querySelector('h1');
document.onkeydown = function(event){
  h1.innerHTML = "Key Down: " + event.key;
}
```

### 4.5 form events
interactions with form elements, such as \<input>

* onfocus: occurs when focus is placed on an \<input> field
* onchange: occurs when an \<input>'s value is changed (useful for radio or checkbox type inputs)
* oninput: occurs when a user provides input to an element (useful for text type inputs or \<textarea> elements)

```
<html>
  <head>
    <title>Data Binding with oninput</title>
  </head>
  <body>
    <h1 id="inputContent"></h1>
    <input type="text" name="textInput" id="textInput" placeholder="Write here to change the h1 element's contents">
  </body>
</html>

var inputContent = document.getElementById('inputContent');
var textInput = document.getElementById('textInput');

textInput.oninput = function(){
  inputContent.innerHTML = this.value;
}
```
### 4.6 checkbox on change, check if it's checked
```
var checkbox = document.getElementById('checkbox');
checkbox.onchange = function(){ 
  if(this.checked) { 
      ...
```

## 5. modify css
```
var h1 = document.querySelector('h1');
h1.style.border = "3px dashed black";
h1.style.textAlign = "center";
```

### 5.1 add multiple css with classList
```
<html>
 <head>
   <title>Applying Multiple Styles</title>
 </head>
 <body>
   <h1>Highlight this element on a click</h1>
 </body>
</html>

var h1 = document.querySelector('h1');

h1.onclick = function(){
  this.classList.add('highlight');
  
  this.classList.toggle('highlight');
}
```

### 5.2 remove classList
```
Element.classList.remove(class)
```

### 5.3 check if classList contains class value
```
Element.classList.contains(class)
```

### 5.4 replace classList
```
Element.classList.replace(oldClass, newClass)
```

### 5.5 toggle classList
```
this.classList.toggle('highlight');
```
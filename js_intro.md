Quick Intro to Javascript
=========================


Running
-------

To run javascript in node.js, one must make sure node.js is already downloaded and installed. Then, write your javascript code into a file, let's call it `script.js`. To run this script, simply call `node script.js` (or the path to the script if it is in another directory).

To run javascript in the browser, we must edit the HTML of the page the javascript will be on. You may put javascript inline with HTML like so:

```html
<script type="text/javascript">
    var myvar = 5;
    myvar++;
    console.log(myvar);
</script>
```

but it is considered better practice to put your code into distinct script files. Write your code into a file, again let's call it `script.js`. This file must be placed in a web-accessible directory like your HTML files. It can then be referenced by URL in your HTML:

```html
<script type="text/javascript" src="/path/to/script.js" />
```



Debugging
----------

Javascript has fairly well-developed debugging tools. The most common are your web browser, and node.js. Both come with a REPL (Read-Eval-Print-Loop) which act somewhat similarly to a shell prompt. You can interactively enter and run commands and receive input with each line. This is in contrast to writing a full script file, running, and reading print statements afterwards (which you can still do, and is better when testing apps or full scripts).

### Developer Tools

Most browsers (Chrome, Safari, Firefox, Opera, maybe recent IE's) come with javascript developer tools. This is most commonly accessed by right-clicking anywhere on an open web page and selecting "Inspect" or "Inspect Element" or something similar. There are varying keyboard shortcuts to bring this menu up as well, varying by OS and browser, but commonly cmd+shift+C for chrome. At the bottom of this window should be the "console". This is where you may enter javascript commands at the bottom, and have them evaluated. The developer tools are fairly advanced in helping view objects: instead of looping through an array and printing each item, simply type in the array's variable name, or in a function just return the array, and the developer tools will allow you to view all the elements, or have dropdowns to view portions. The same goes with object types: the developer tools should have an advanced viewer for simply returned objects. The autocomplete typeahead available in some browsers helps discover available properties or methods of an object you might not know or remember. For instance, typing `document.get` in the chrome console presents an autocomplete with `getElementById`, `getElementsByClassName`, `getElementsByName` etc. You can discover lots of information from this, or just entering the object you want to inspect: try just entering `Math` and hitting enter. 


In addition to the browser's REPL, there is one available with node.js. Node is a program you install on your computer to run javascript outside of the browser (like you might run python or shell scripts). After installing, just running `node` should present you with a REPL just like the browser console. You may not have the fancy autocomplete and drop-downs available, but most features should work the same in both. Just Be aware that node does **not** work with DOM objects, `document` and `window`. You will need a browser environment to play with HTML.


**Logging**: javascript's version of "print statements" is `console.log()`. Whatever needs to be printed or logged (objects, arrays, or other variables can be put in there) can be called with console.log. In node this will print to your terminal; in the browser this will print to your developer tools console.


Other Resources
---------------

**MDN** (Mozilla Developer Network) should be your best friend during javascript development. It is generally the best reference, most up-to-date, and contains the best helpful guides and hints for pits or confusing behavior that may trip up a new developers. When searching for any javascript reference I highly recommend googling as such: "javascript [your words here] MDN". 

when possible, sections are linked to MDN references for more information

https://developer.mozilla.org/en-US/docs/Web/JavaScript



Syntax
------


### [Variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Variables)

Variables are created using the `var` keyword, and then the name of the variable. You may find that ommitting the `var` keyword does work, but you have implicitly created a global variable and that is not a good idea, generally. Stick to `var`. Variable names should start with a letter (upper or lower case) or some certain unicode symbols. They may not start with a number or digit, but may contain them after the first character. Variable names _are_ case sensitive. Variables may not be the same as a javascript reserved word (things like `if`, `var`, `false`, `else`, `for`, `while`, etc). You may immediately assign a value to your variable with `=` but it is not required; The `var` keyword only needs to be written when creating your variable for the first time. After that it may be referenced with just it's name.

```js
var MyNumber = 5;
var can_humans_fly = false;
var aVariable;
```

### [Comments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Comments)

Comments are created using `//` for single-line comments and the pair `/*  */` for multi-line comments.

```js
//this is a one-line comment. 
var this_line_is_code;

/* This comment
 can go on as many lines
 as needed.
as long as it's eventually closed with */
```

### [Conditionals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Conditional_statements)

Conditional statements in javascript are things like `if` and `switch`:

```js

if ( myVar ) {
    //this code runs when myVar is true
}


if ( something ){
    //this will run if something is true
} else if ( something_else ){
    //this will run if something was false and something_else is true
} else {
    //this will only run if both were false
}

```


**[Equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)** in javascript can be typed or non-typed. This means there are different operators to determine if two variables' values match, or both values _and_ type:

```js

var five = 5;


five == 5; //true, they are both the number 5
five == "5"; //true. The string "5" is converted to number form, it gives 5 which is equal

five === "5"; //false. The string "5" is not converted, and this fails because they are different types

```

So `==` does not check the type of variables but rather tries to convert them to the same type and then checks. The inverted form of this is `!=`

And `===` checks for type equality as well. The variables must be the same type and the same value. The inverted form is `!==`



**[Logic Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Logical_operators)** are things used to join statements in conditions (if-statements). You "and" two things together with `&&` or "or" them with `||`. Conditions are inverted ("NOT"-ed) with an exclamation point (also called bang): `!`. You may invert twice to turn a non-boolean (true/false) variable into one, depending on whether it's value is falsey. This looks like "!!myVar" and will give you either `true` or `false`. True, when it is a number that is anything but 0 (0 is considered false). If the variable is a string, it will give you true for anything but an empty string (`""`). You do not need to convert to true and false using `if` statements or anything else. Double-bang is only for when you explicity want something to become `true` or `false` in variable type (see **Types** below). 

```js
if ( a && b ){
    // do something
}

if ( true || false ) {
    //something else
}
```

Similar to `true` and `false`, are `null` and `undefined`. Variables that are created but never given a value are `undefined`. If a variable is `undefined` and checked in a conditional, it will be false. `null` is in a similar boat, and will evaluate to false.

### [Loops](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)

Loops in javascript are fairly simple:


```js

for (var i=0; i<15; i++){
    console.log(i);
}


var check = true;
while (check){
    doSomething();
}
```


To break out of a loop at any time, you can simply call `break;`. To skip to the next iteration of the loop, call `continue;`


### [Postfix Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#Increment_and_decrement)

Numbers can be incremented (increased by one) using the `++` operator. The reverse (decrement) applies for `--`. `myNum++;`

### Properties

Objects contain properties, which are accessed using a period: `myObj.property` or  `car.wheels`. You may assign to properties just like a normal variable: `myObj.foo = "bar";`


### [Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Functions)

Functions can be created in a few different ways. The simplest is using a named function:

```js
function add(a,b){
    return a + b;
}
```

For more, and other examples, see the _Function_ type below.


[Types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Data_structures_and_types)
-----

Javascript is a loosely-typed language. This means that variables do not have to store a specific type, but can store anything. This doesn't mean Javascript doesn't have types, though. The few it has are:

### [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type)

These are things like integers and floating-point numbers (decimals). Most of the typical mathematical operators you would expect to work on Number types do: `+`, `-`, `*`, `%` (modulus). **Note**: exponentiation does not use the carat (i.e. _not_ `2^3`, but rather use Math.pow(2,3). The carat (`^`) operator in Javascript is the XOR operation. Several other common functions are available in the Math object:

- `Math.floor()` and `Math.ceil()`
- `Math.round()`
- `Math.abs()`
- `Math.min()` and `Math.max()`
- `Math.random()`

Other types of variables (like strings, see below) can be converted to numbers with `parseInt()` and `parseFloat()`. 

**Note**: When doing floating-point math, you may experience unusual results in decimal precision:

```
node> 0.1 +0.2
0.30000000000000004
```

This is due to the inability to store certain decimals in binary representation. It is encouraged to pick the precision necessary for what you're doing (e.g. 2 decimal places) and either scale everything up by 100, work with integers, and divide by 100 at the end, or round to two places at the end using a similar method.


### [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#String_literals)

Strings in Javascript are similar to those in most languages. You can create a string using 'single' quotes or "double" quotes, they are equivalent. Strings may be joined together using the `+` operator. They may also be joined using the `.concat()` method attached to all strings (e.g. `"pumpkin" + " pie"` and `"pumpkin".concat(" pie")`). Strings have a few other methods available for text manipulation, `toUpperCase()` and `toLowerCase()`. These are called as functions on the String object just like concat was. There are various other methods available attached to String objects:

- `replace()`: substitute part of a string with a replacement. `"foobar".replace("b","g") == "foogar"`
- `match()`: determine if your string contains a particular expression. `"foobar".match("bar")`
- `split()`: separate a string based on a given character. `"a:b:c".split(":") == ["a","b","c"]`
- `substr()`: retreive parts of a string based on index and length. `"ABCDEFGHIJKL".substr(4,3) == "EFG"`

Other types of variables (like Numbers, Arrays, etc) may be converted into strings by calling the method attached to them: `.toString()`: 

```js
var mynum = 5;
var mystr = mynum.toString();

console.log(mynum);
>>> 5
console.log(mystr);
>>> "5"
```


### [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Other_types)

Booleans are your standard `true`/`false` values commonly used in conditions, checks, loops, etc. In Javascript they are case-sensitive and must be all lowercase. A variable can be created as `var canFly = false;`, using the single or double bang operator as described above, or joining statements with `&&` and `||`.


### [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#Array_object)

Arrays are simple lists of values. Arrays can store any type of variable, and each item of the array does not have to be the same type, or the same size. Arrays themselves do not have a fixed size, and elements can be added or removed at any time. An empty array can be created with empty square brackets:

```js
var mylist = [];
```

You may create an array with values in it already like:

```js
var shopping = ["milk","eggs","butter"];

//oh, I forgot to add bread
shopping.push("bread"); //'shopping' is now 4 elements long, since we added bread to the end, after butter
```

The length of an array is available as the `.length` property of your array variable.




### [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)

Objects are rather abstract to explain, but are very flexible containers. Objects in javascript are commonly used for complex representations (a Point, a Rectangle, a Car, a Continent), to group common items together (like a module or library), or to represent the state of something without too many global variables. Objects are created with curly brackets, `{}`, and contain named properties. Those properties can be created, accessed, or changed using a dot `.` on the object. Properties work similarly to variables in that they are given names similar to variable naming rules, and can contain values of any type (including other objects, or functions).

```js
var empty_object = {};

var car = {
    wheels: 4,
    type: "sedan",
    radio: true,
    gas: 10,
    postion: 0,
    go: function(){ 
        this.position++;
        this.gas--;
    }
};

car.wheels;
>>> 4
car.type;
>>> "sedan"
car.type = "hatchback";
car.type;
>>> "hatchback"
car.gas;
>>> 10
car.go();
car.gas;
>>> 9
car.position;
>>> 1
```




### [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)

Functions can be created in a few different ways. The simplest is using a named function:

```js
function add(a,b){
    return a + b;
}
```

Functions created this way must start with the `function` keyword, then the name of the function (similar naming rules as variables above), then parenthesis describing any parameters necessary (no parameters would just be `()`).  After that, curly braces. Your code must go between the curly braces. To receive a value from a function, the function must _return_ that value. For instance:

```js
function add_wrong(a,b){
    a + b;
}


var sum = add_wrong(2,3);
```


The `sum` variable will not contain `5`, it will be nothing or, in Javascript: `null` or `undefined`. This is because the result of the addition is not `return`'ed in the function.

Functions may also be declared without explicit names, and stored in variables:

```js
var myFunc = function(a){
    return a*a;
}
```

This syntax is slightly different, and does result in slightly different code. In the _named_ example where we called our function **add**, that name could not be changed, and the function could always be called as `add()`. Here, the function was not given an explicit name, but instead stored in a variable we gave the name `myFunc`. This function can be called like `myFunc(3)`, which will give us 9. Note that variables in javascript may be reassigned at any time, so this may not always be the name of the function. Take, for example:

```js
var result;

var myFunc = function(a){
    return a*a;
}
result = myFunc(3);  // 9

var square = myFunc; //our new variable square now stores the function as well
result = square(2); // result is now 4

result = myFunc(4); // result is now 16

myFunc = 0; // myFunc is set to something else now. We cannot call it as a function anymore, but we can still use square()
```

You may additionally see functions as part of objects, or in arrays, or as another function's argument. These are commonly not given named functions, since you will have a variable-like reference to the function as the object property, or the array's index, or the function's argument name.

```js
var myObject = {
    foo: function(a){ return a*a };
}

myObject.foo(3); // 9

// --------------------------------------

var myArray = ["a","b",function(x){ return x*x; }];

myArray[2](3); // get the thing at array index 2, and run it as a function with the parameter 3

// ----------------------------------------

//Let's define a function to take three parameters, where the last one is another function we will run here
function doStuff(a, b, funcName){
    funcName();
    return a+b;
}

doStuff(1, 7, function(){ console.log("I was run in doStuff"); }); //doStuff will call our function, whatever it is, right before adding the numbers
```

DOM
---

The **DOM**, or Document Object Model, is how javascript interacts with a web page. The DOM is unavailable with node.js so this section is purely for browser-based javascript. Interacting with the DOM and browser is primarily done with two global objects: [`window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) and [`document`](https://developer.mozilla.org/en-US/docs/Web/API/document). The `window` object generally represents user's browser tab. It represents things outside of the HTML like the window size, the current URL, the ability to go forward and backward in the user's history as if they pressed the back/forward buttons. The `document` object generally represents the HTML content of the page. `document` is used to find and access elements, modify them, or create and delete elements. It is also how behaviors are attached to elements (mouse over, click, etc). 



```js
var article_title = document.getElementById("title");
article_title.innerHTML = "New Title";

var tags_to_delete = document.getElementsByTagName("p");
tags_to_delete.remove();


window.location.pathname;
>>> "/en-US/Web/API/document"
window.location = "http://purple.com"; //this will totally redirect the user immediately

window.innerHeight;
>>> 969
window.innerWidth;
>>> 1894
```

A big trap to watch out for when dealing with browsers is that javascript and HTML modifications do not work the same across every browser. Not every browser has implemented every method on elements, or elements may behave and look differently on each. The way to attach behaviors (click, mouse over, key presses) are generally different from browser to browser. MDN usually provides the information of which browsers support a given behavior in javascript, and what the code should be for the popular ones that do implement something in a different way. This is another reason why MDN should be your first reference whenever possible.


Libraries
---------

Javascript does not have the concept of "installed" libraries like one might import in python. However, something similar is acheived by referencing third-party scripts. Just like one might use the `<script>` tag to point to one's own javascript file, multiple `<script>` tags can be used which each reference files downloaded from or provided by third parties as libraries. Generally this code is exposed as an object that your code may use (as long as your code is loaded *after* the libraries, by putting the script tag to your code after or **below** the others). As mentioned in the above section, browser differences can be a large pain when developing for the web. There are several libraries designed to ease that pain and handle the browser differences for you. [jQuery](https://jquery.com/) and [Modernizr](https://modernizr.com/) are two such popular libraries. [Underscore.js](http://underscorejs.org/) is available for a handful of convenience functions just to make your life easier. There are even libraries to make working with dates and times easier: [momentjs](http://momentjs.com/) provides some helpful resources to transform dates in a possibly easier way than javascript's native `Date` object. And of course there are libraries available that make drawing, charting, and graphing better:

- [leaflet](http://leafletjs.com/)
- [d3.js](http://d3js.org/)
- [mapbox](https://www.mapbox.com/)
- [GMaps](https://hpneo.github.io/gmaps/)
- [Paper.js](http://paperjs.org/)
- [Processing.js](http://processingjs.org/)
- [three.js](http://threejs.org/)

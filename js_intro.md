Quick Intro to Javascript
=========================

`@todo:` Debugging, node, web console


`@todo:` MDN links

Syntax
------


### Variables

Variables are created using the `var` keyword, and then the name of the variable. You may find that ommitting the `var` keyword does work, but you have implicitly created a global variable and that is not a good idea, generally. Stick to `var`. Variable names should start with a letter (upper or lower case) or some certain unicode symbols. They may not start with a number or digit, but may contain them after the first character. Variable names _are_ case sensitive. Variables may not be the same as a javascript reserved word (things like `if`, `var`, `false`, `else`, `for`, `while`, etc). You may immediately assign a value to your variable with `=` but it is not required; The `var` keyword only needs to be written when creating your variable for the first time. After that it may be referenced with just it's name.

```js
var MyNumber = 5;
var can_humans_fly = false;
var aVariable;
```

### Comments

Comments are created using `//` for single-line comments and the pair `/*  */` for multi-line comments.

```js
//this is a one-line comment. 
var this_line_is_code;

/* This comment
 can go on as many lines
 as needed.
as long as it's eventually closed with */
```

### Conditionals

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


**Equality** in javascript can be typed or non-typed. This means there are different operators to determine if two variables' values match, or both values _and_ type:

```js

var five = 5;


five == 5; //true, they are both the number 5
five == "5"; //true. The string "5" is converted to number form, it gives 5 which is equal

five === "5"; //false. The string "5" is not converted, and this fails because they are different types

```

So `==` does not check the type of variables but rather tries to convert them to the same type and then checks. The inverted form of this is `!=`

And `===` checks for type equality as well. The variables must be the same type and the same value. The inverted form is `!==`



**Logic Operators** are things used to join statements in conditions (if-statements). You "and" two things together with `&&` or "or" them with `||`. Conditions are inverted ("NOT"-ed) with an exclamation point (also called bang): `!`. You may invert twice to turn a non-boolean (true/false) variable into one, depending on whether it's value is falsey. This looks like "!!myVar" and will give you either `true` or `false`. True, when it is a number that is anything but 0 (0 is considered false). If the variable is a string, it will give you true for anything but an empty string (`""`). You do not need to convert to true and false using `if` statements or anything else. Double-bang is only for when you explicity want something to become `true` or `false` in variable type (see **Types** below). 

```js
if ( a && b ){
    // do something
}

if ( true || false ) {
    //something else
}
```

Similar to `true` and `false`, are `null` and `undefined`. Variables that are created but never given a value are `undefined`. If a variable is `undefined` and checked in a conditional, it will be false. `null` is in a similar boat, and will evaluate to false.

### Loops

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


### Postfix Operators

Numbers can be incremented (increased by one) using the `++` operator. The reverse (decrement) applies for `--`. `myNum++;`

### Properties

Objects contain properties, which are accessed using a period: `myObj.property` or  `car.wheels`. You may assign to properties just like a normal variable: `myObj.foo = "bar";`


### Functions

Functions can be created in a few different ways. The simplest is using a named function:

```js
function add(a,b){
    return a + b;
}
```

For more, and other examples, see the _Function_ type below.


Types
-----

Javascript is a loosely-typed language. This means that variables do not have to store a specific type, but can store anything. This doesn't mean Javascript doesn't have types, though. The few it has are:

### Number

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


### String

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


### Boolean

Booleans are your standard `true`/`false` values commonly used in conditions, checks, loops, etc. In Javascript they are case-sensitive and must be all lowercase. A variable can be created as `var canFly = false;`, using the single or double bang operator as described above, or joining statements with `&&` and `||`.


### Array

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

`@todo:` finish arrays


`@todo:` Object type



### Functions

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


`@todo:` DOM, `window`, `document`, and "libraries"

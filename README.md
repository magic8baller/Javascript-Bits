# Javascript-Bits

## STRINGS

### 1. String.replace() to replace all the values
The String.replace() function allows you to replace strings using String and Regex.

```javascript
var string = "login login";  
console.log(string.replace("in", "out")); // "logout login"  
```
append <b>/g</b> to replace all
```javascript
console.log(string.replace(/in/g, "out")); //"logout logout"
```

### 2.String to Array with Spread syntax 
```javascript
let a= 'This is a String';
let b = [...a]; // and this will be an array
console.log(b); //output: 
[ "T", "h", "i", "s", " ", "i", "s", " ", "a", " ", … ]
```
<hr/>

## OBJECTS

### OPTIMIZE 1. Checking values in an Object with Object.keys(Obj).length
To check whether an object is empty or not,  use
```javascript
Object.keys(YOUR_OBJECT).length 
```
example:
```javascript
user1 = { id: 1, name: 'John Doe'}
user2 = {}

Object.keys(user1).length // 2

Object.keys(user2).length // 0
```



<hr/>

## ARRAYS

### 1) Array#splice to delete array elements
It optimizes speed of your JS code.

Using splice instead of delete is a good practice, it will save some”null/undefined space” in your code.

The downside of using delete is it will delete the object property, but will not reindex the array or update its length, leaving undefined values. Also it consumes a-lot of time in execution.

Example
```javascript
myArray = ["a", "b", "c", "d"] 
myArray.splice(0, 2) ["a", "b"]

myArray // ["c", "d"]
```

### 2) Merging arrays without causing server load

If your requirement is of merging two arrays, use Array.concat() function

For merging two arrays:
```javascript
const array1 = [1, 2, 3];  
const array2 = [4, 5, 6];  
array1.concat(array2);
console.log(array1); // [1,2,3,4,5,6];  
```
This function works best for small arrays.

To merge large arrays we use

Array.push.apply(arr1, arr2)
Reason is using Array.concat() function on large arrays will consume lot of memory while creating a separate new array.

In this case, you can use Array.push.apply(arr1, arr2) which instead will merge the second array in the first one, hence reducing the memory usage.

Example:
```javascript
const array1 = [1, 2, 3];  
const array2 = [4, 5, 6];  
array1.push.apply(array1, array2);
console.log(array1); // [1,2,3,4,5,6];
```
It will also optimize the performance of your Javascript code irrespective of size of array.

### 3) Caching the array.length in the loop
This tip is very simple and causes a huge impact on the performance when processing large arrays during a loop. Basically, almost everybody writes this synchronous for to iterate an array:
```javascript
for (let i = 0; i < array.length; i++) {  
    console.log(array[i]);
}
```
If you work with smaller arrays – it’s fine, but if you process large arrays, this code will recalculate the size of array in every iteration of this loop and this will cause a bit of delays. To avoid it, you can cache the array.length in a variable to use it instead of invoking the array.length every time during the loop:
```javascript
let length = array.length;  
for (let i = 0; i < length; i++) {  
    console.log(array[i]);
}
```
Further abstraction:
```javascript
for (let i = 0, length = array.length; i < length; i++) {  
    console.log(array[i]);
}
```

### 4) Array truncation
This technique can lock the array’s size, this is very useful to delete some elements of the array based on the number of elements you want to set. For example, if you have an array with 10 elements, but you want to get only the first five elements, you can truncate the array, making it smaller by setting the array.length = 5. See this example:
```javascript
const array = [1, 2, 3, 4, 5, 6];  
console.log(array.length); // 6  
array.length = 3;  
console.log(array.length); // 3  
console.log(array); // [1,2,3] 
```

### 5) Shuffling array’s elements
To shuffle the array’s elements without using any external library like Lodash, just run this magic trick:
```javascript
const list = [1, 2, 3];  
console.log(list.sort(function() {  
    return Math.random() - 0.5
})); // [2,1,3]
```
<hr/>

### 6) Array#reduce()
// Sum array
```javascript
 const sum = (arr) => arr.reduce((a, b) => (a + b), 0)
 sum([1, 2, 3, 4]) // output: 10
```

### 7) Array#slice for the last item in the array
If you want to cut the arrays, you can set the begin and end arguments like Array.prototupe.slice(begin, end).  Not setting the end argument means that the function will automatically go for the max value for the array. This function also accepts the negative values. If you set a negative number as begin an argument, you will obtain the last element from the array.
```javascript
const array=  [1, 2, 3, 4, 5, 6];

console.log(array. Slice(-1)); // [6]
console.log(array. Slice(-2)); // [5, 6]
console.log(array. Slice(-3)); // [4, 5, 6]
```
<hr/>

## MATH

### 1. Convert to floating number without killing performance
Often we use math.floor, math.ceil and math.round for eliminating decimals. Instead of using them use “~~” to eliminate decimals for a value.

It is also helpful in increasing performance when it comes to micro optimizations in a code.

Example:

Use
```javascript
~~ (math.random*100)
```
Instead of
```javascript
math.round(math.random*100)
```

### 2. Max value

// Find max value
```javascript
 const max = (arr) => Math.max(...arr);
 max([123, 321, 32]) // outputs: 321
 ```
<hr/>

## OPERATORS

### 1) Converting to boolean using !! operator
Sometimes we need to check if some variable exists or if it has a valid value, to consider them as true value. For do this kind of validation, you can use the !!(Double negation operator) a simple !!variable, which will automatically convert any kind of data to boolean and this variable will return false only if it has some of these values: 0, null, "", undefined or NaN, otherwise it will return true. To understand it in practice, take a look this simple example:
```javascript
function Account(cash) {  
    this.cash = cash;
    this.hasMoney = !!cash;
}
const account = new Account(100.50);  
console.log(account.cash); // 100.50  
console.log(account.hasMoney); // true

const emptyAccount = new Account(0);  
console.log(emptyAccount.cash); // 0  
console.log(emptyAccount.hasMoney); // false 
```
In this case, if an account.cash value is greater than zero, the account.hasMoney will be true.


<hr/>


### 2) Converting to number using + operator
This magic is awesome! And it’s very simple to be done, but it only works with string numbers, otherwise it will return NaN(Not a Number). Have a look on this example:
```javascript
function toNumber(strNumber) {  
    return +strNumber;
}
console.log(toNumber("1234")); // 1234  
console.log(toNumber("ACB")); // NaN  
```
This magic will work with Date too and, in this case, it will return the timestamp number:
```javascript
console.log(+new Date()) // 1461288164385  
```
### 3) Short-circuits conditionals
If you see a similar code:
```javascript
if (conected) {  
    login();
}
```
You can shorten it by using the combination of a variable (which will be verified) and a function using the && (AND operator) between both. For example, the previous code can become smaller in one line:
```javascript
conected && login();  
```
You can do the same to check if some attribute or function exists in the object. Similar to the below code:
```javascript
user && user.login();
```

### 4) Default values using || operator
Today in ES6 there is the default argument feature. In order to simulate this feature in old browsers you can use the || (OR operator) by including the default value as a second parameter to be used. If the first parameter returns false the second one will be used as a default value. See this example:
```javascript
function User(name, age) {  
    this.name = name || "Oliver Queen";
    this.age = age || 27;
}
const user1 = new User();  
console.log(user1.name); // Oliver Queen  
console.log(user1.age); // 27

const user2 = new User("Barry Allen", 25);  
console.log(user2.name); // Barry Allen  
console.log(user2.age); // 25  
```

### 5) Use "in": Detecting properties in an object
This trick is very useful when you need to check if some attribute exists and it avoids running undefined functions or attributes. If you are planning to write cross-browser code, probably you will use this technique too. For example, let’s imagine that you need to write code that is compatible with the old Internet Explorer 6 and you want to use the document.querySelector(), to get some elements by their ids. However, in this browser this function doesn’t exist, so to check the existence of this function you can use the in operator, see this example:
```javascript
if ('querySelector' in document) {  
    document.querySelector("#id");
} else {
    document.getElementById("id");
}
```
example:
```javascript
const user1 = { id: 1, name: 'John Doe'}
'name' in user1 ? console.log('prop exists in obj :)') : console.log('prop doesn't exist in obj :( ')
// 'prop exists in obj :)'
```

## DOM

### 1. handle search params with URLSearchParams 
[MDN URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)
can use URLSearchParams interface to build and manipulate the URL query string.

To get the search params from the current window's URL, you can do this:
```javascript
// https://some.site/?id=123
const parsedUrl = new URL(window.location.href);
console.log(parsedUrl.searchParams.get("id")); // 123
```
The toString method of URL is the href property, so the constructor can be used to normalise and encode a URL directly.
```javascript
const response = await fetch(new URL('http://www.example.com/démonstration.html'));
```

### 2.Event handler on the parent
Adding list elements dynamically, eg. links:

``` javascript
<ul id="parent">
  <li><a href="link#1">Home</a></li>
  <li><a href="link#2">About</a></li>
  <li><a href="link#3">Contact</a></li>
  <li><a href="link#4">Support</a></li>
  <li><a href="link#5">Medium</a></li>
</ul>
```

``` javascript
(function(d){
  let parent = d.querySelector('#parent');
  parent.addEventListener('click', function(e){
    let x = e.target; // The clicked element
    if(x.nodeName.toLowerCase() === 'a') {
      console.log('The clicked link is' + x)
    }
  });
})(document);
```


<hr/>

## ARRAY DESTRUCTURING:

### 1) Swap variables
You can make this happen by using the array destruction to swap the values. Use this code to do it:
```javascript
let a = 'world', b = 'hello'
 [a, b] = [b, a]
 console.log(a) // -> hello
 console.log(b) // -> world
```

### 2) Async/ await with destructing
async await destructuring to further simplify flow:
```javascript
const [user, account] = await Promise.all([
 fetch('/user'),
 fetch('/account')
 ])
 ```
<hr/>
<hr/>

##

#### Cache the variable
Caching the variable tremendously increase javascript performance.

Everytime we use document.getElementById() or getElementsByClassName(), JS travels through all elements repeatedly upon each similar element request.

In Order to boost performance, cache your selections to some variable (if using the same selection multiple times).

Example:
```javascript
var cached = document.getElementById('someElement');
cached.addClass('cached-element');
```
It is a simple optimization tip with drastic impact on performance, recommended for processing large arrays in loop(s).
[Performance example](https://jquery-howto.blogspot.com/2008/12/caching-in-jquery.html "jquery-ex")

## SHORTCUTZ

### 1. Values: truthy and falsy
Most new JavaScript developers may be aware of the built-in data types in JavaScript. However, not so many may know about JavaScript’s classification of truthy and falsy values.

Anytime JavaScript expects a boolean value, a truthy value will behave like true, whereas a falsy value works like false. These are the falsy values:

0
-0
null
undefined
''
NaN
As you can see, even an empty string is considered a falsy value. All other values besides the above mentioned are truthy values.

The ! operator can be used to convert any value to a boolean. When using the ! operator with values, truthy values evaluate to false, while falsy values evaluate to true. You can use the double (!!) operator to get the corresponding boolean for any value.

```javascript
// FALSY VALUES

console.log(!!0); // false
console.log(!!-0); // false
console.log(!!''); // false
console.log(!!false); // false
console.log(!!NaN); // false
console.log(!!null); // false
console.log(!!undefined); // false

// TRUTHY VALUES

console.log(!!+Infinity); // true
console.log(!!-Infinity); // true
console.log(!![]); // true
console.log(!!{}); // true
console.log(!!new String('')); // true
console.log(!!new RegExp('')); // true
console.log(!!'Non-empty'); // true
```

Let’s say a variable person can either contain an object or null. You can verify that the person variable is not null, by using the following condition:
```javascript
if (person !== null) { ... }
```
Considering that null is falsy while every other object is truthy, you can use this (less strict condition):
```javascript
if (person) { ... }
```
### 2. Type Conversion: Number and String
One of the most common things you find yourself doing in JavaScript is using arithmetic operators: +, -, *, /. These operators expect operands that are numbers. So when any of the operands is not a number, JavaScript implicitly coerces it into a number. But there are times when you may not get the result you may be expecting, especially when you are using the + operator. This is majorly because the + operator is also used for string concatenation. See the following snippet:

```javascript

console.log(100 + 50); // 150
console.log(100 - 50); // 50

console.log('100' + 50); // "10050"
console.log('100' - 50); // 50

console.log(null + 50); // 50
console.log(null - 50); // -50

console.log(void 0 + 50); // NaN
console.log(void 0 - 50); // NaN

console.log(true + 50); // 51
console.log(true - 50); // -49

console.log(false + 50); // 50
console.log(false - 50); // -50

console.log([] + 50); // "50"
console.log([] - 50); // -50

console.log([100] + 50); // "10050"
console.log([100] - 50); // 50

console.log({} + 50); // "[object Object]50"
console.log({} - 50); // NaN

console.log(new Date + 1000); // "Thu May 31 2018 18:27:51 GMT+0100 (WAT)1000"
console.log(new Date - 1000); // 1527787670595
```

As you can see, implicit type coercion may not always give you the result you are expecting. This is because of how JavaScript handles type conversion especially for objects. The difference is due to the order in which JavaScript calls the toString() and valueOf() methods on the object for object-to-primitive conversion.

Now here is the trick. The + operator when used as a unary operator always converts its operand to a number. Hence, the following:
```javascript
console.log(+'100'); // 100

console.log(+null); // 0
console.log(+void 0); // NaN

console.log(+true); // 1
console.log(+false); // 0

console.log(+[]); // 0
console.log(+[100]); // 100
console.log(+[100, 50]); // NaN

console.log(+{}); // NaN

console.log(+new Date); // 1527790306576
```

Using the unary + operator on a value is functionally equivalent to casting the value using the Number() function.
```javascript
+new Date === Number(new Date); // true
```
The + operator can also be used to convert values to string. Concatenate an empty string('') to any value using the + operator to convert the value to a string.

```javascript
console.log(100 + ''); // "100"

console.log(null + ''); // "null"
console.log(void 0 + ''); // "undefined"

console.log(true + ''); // "true"
console.log(false + ''); // "false"

console.log([] + ''); // ""
console.log([100] + ''); // "100"
console.log([100, 50] + ''); // "100,50"

console.log({} + ''); // "[object Object]"

console.log(new Date + ''); // "Thu May 31 2018 19:28:09 GMT+0100 (WAT)"
```

Using the + operator to convert values to string is functionally equivalent to casting values to string using the String() function.
```javascript
([100, 50] + '') === String([100, 50]); // true
```

### 3. Short-Circuiting
When working with the (|| and &&) logical operators, you may have noticed an interesting behavior called short-circuiting. Here is how it works:

The logical && operator returns the first operand if it is falsy, otherwise it returns the second operand.

The logical && short-circuiting is commonly used as a replacement for very simple if statements as shown in the following snippet:
```javascript
// METHOD 1: Using if statement
if (person) {
  fetchProfile(person);
}

// METHOD 2: Using short-circuiting
person && fetchProfile(person);
```


Note that using short-circuiting actually returns a value since it is a JavaScript expression. Hence, the result of a short-circuiting operation can be stored in a variable or used anywhere JavaScript expects a value.
```javascript
const personProfile = person && fetchProfile(person);
```
However, using if statement does not return a value because it is a JavaScript statement.

The logical || operator returns the first operand if it is truthy, otherwise it returns the second operand.

The logical || short-circuiting is commonly used when assigning fallback values to local variables as shown in the following snippet:
```javascript
// METHOD 1: Using if/else statements
let requestAnimFrame = null;

if (window.requestAnimationFrame) {
  requestAnimFrame = window.requestAnimationFrame;
}

else if (window.webkitRequestAnimationFrame) {
  requestAnimFrame = window.webkitRequestAnimationFrame;
}

else if (window.mozRequestAnimationFrame) {
  requestAnimFrame = window.mozRequestAnimationFrame;
}

// METHOD 2: Using short-circuiting
const requestAnimFrame2 = (
  window.requestAnimationFrame ||
  window.webkitRequestAnimationFrame ||
  window.mozRequestAnimationFrame ||
  null
);
```
In the following snippet, short-circuiting is used to create two functions that always return a boolean value. If the first argument is a boolean value, it is returned, otherwise the desired fallback boolean value is returned.
```javascript
// Function that accepts a boolean as first argument
// and returns the boolean otherwise `false`
const booleanOrFalse = value => (typeof value == 'boolean') && value;

// Function that accepts a boolean as first argument
// and returns the boolean otherwise `true`
const booleanOrTrue = value => (typeof value != 'boolean') || value;

console.log(booleanOrFalse(true)); // true
console.log(booleanOrFalse(false)); // false
console.log(booleanOrFalse(1)); // false
console.log(booleanOrFalse(0)); // false
console.log(booleanOrFalse('String')); // false
console.log(booleanOrFalse({})); // false
console.log(booleanOrFalse([])); // false

console.log(booleanOrTrue(true)); // true
console.log(booleanOrTrue(false)); // false
console.log(booleanOrTrue(1)); // true
console.log(booleanOrTrue(0)); // true
console.log(booleanOrTrue('String')); // true
console.log(booleanOrTrue({})); // true
console.log(booleanOrTrue([])); // true
```
### 4. Ternary Operator
The ternary operator can be used as a substitute for very simple if/else statements. Here is the syntax:
```javascript
(condition) ? (return value if truthy) : (return value if falsy)
```
The ternary operation requires 3 operands. The first is a condition value or expression. The second is a value or expression that is evaluated and returned if the condition is truthy. The third is a value or expression that is evaluated and returned if the condition is falsy.

Here is a quick example showing how to use the ternary operation as a shortcut for simple if/else statements.
```javascript
// METHOD 1: Using if/else statements
if (loggedIn) {
  showUserProfile();
} else {
  showLoginForm();
}

// METHOD 2: Using ternary operation
loggedIn ? showUserProfile() : showLoginForm();
```

This feels good already, but it gets more interesting knowing that ternary operations can be nested. The ternary operator has a right-to-left associativity. Hence, the following expression:
```javascript
a ? b : c ? d : e ? f : g
```
is evaluated as:
```javascript
(a ? b : (c ? d : (e ? f : g)))
```
Nested ternary operations can be used as alternatives to multiple if/else statements. Here is a simple example:
```javascript
var MIN_VALUE = 1;
var MAX_VALUE = 5;

/**
 * boundedValue(val)
 *
 * Returns val if val between MIN_VALUE and MAX_VALUE both inclusive
 *
 * Otherwise, returns MIN_VALUE if val is less than MIN_VALUE
 *
 * Else, returns MAX_VALUE if val is greater than MAX_VALUE
 */

// METHOD 1: Using if/else statements
function boundedValue(val) {
  if (val > MAX_VALUE) {
    return MAX_VALUE;
  } else if (val < MIN_VALUE) {
    return MIN_VALUE;
  } else {
    return val;
  }
}

// METHOD 2: Using ternary operation
function boundedValue(val) {
  return (val > MAX_VALUE) ? MAX_VALUE : (val < MIN_VALUE) ? MIN_VALUE : val;
}

boundedValue(0); // 1
boundedValue(3); // 3
boundedValue(7); // 5
```

Notice how concise the ternary operation is in comparison to using multiple if/else statements.

Note that the ternary operation returns a value since it is a JavaScript expression. Hence, the result of a ternary operation can be stored in a variable or used anywhere JavaScript expects a value. That is the reason why the value of the ternary operation could be returned from the boundedValue() function.

### 5. Working with Numbers
Random Numbers
As a JavaScript developer, it is possible that you have used Math.random() at one point or the other. The Math.random() function returns a floating-point, pseudo-random number in the range from 0 inclusive up to but not including 1.
```javascript
console.log(Math.random()); // 0.684408535330514
```
If you want to create a random floating-point number in the range from 0 inclusive up to but not including let’s say 10, you multiply Math.random() by 10.
```javascript
console.log(Math.random() * 10); // 8.368613312939646
```
Math.random() when combined with other functions like Math.floor() or Math.ceil() can be used for some cool number generation combos.

Here is a simple function that generates a random integer from 1 to the given maxvalue.
```javascript
function randomInteger(maxvalue) {
  return 1 + Math.floor(Math.random() * maxvalue);
}
```

Min/Max Numbers
The Math.min() and Math.max() functions also come in very handy when trying to deal with bounded numbers. For example the previous boundedValue() example can be implemented using Math.min() and Math.max() as follows:
```javascript
var MIN_VALUE = 1;
var MAX_VALUE = 5;

/**
 * boundedValue(val)
 *
 * Returns val if val between MIN_VALUE and MAX_VALUE both inclusive
 *
 * Otherwise, returns MIN_VALUE if val is less than MIN_VALUE
 *
 * Else, returns MAX_VALUE if val is greater than MAX_VALUE
 */

function boundedValue(val) {
  return Math.max(MIN_VALUE, Math.min(MAX_VALUE, val));
}
```

Number Base Conversion
In JavaScript, number literals are primitives. However, you can access any method available on number objects created using the Number() constructor, one of which is toString().

The Number.prototype.toString() method accepts a radix integer argument which specifies the base to which the number must be converted. If this argument is not specified, it defaults to 10, which means the number is left the same way and then converted to a string.

Hence, you can convert a number to different bases as shown in the following snippet:
```javascript
(255).toString(); // "255"
(255).toString(2); // "11111111"
(255).toString(8); // "377"
(255).toString(16); // "ff"
```
Cool huh? The following snippet shows a function rgbToHex() for converting RGB color value to hex color value.
```javascript
function leftZeroPad(value, maxlength) {
  while (value.length < maxlength) {
    value = '0' + value;
  }
  return value;
}

function boundedValue(minvalue, maxvalue) {
  return function(value) {
    return Math.max(minvalue, Math.min(maxvalue, +value || 0));
  }
}

function colorValue(value) {
  var hex = boundedValue(0, 255)(value).toString(16);
  return leftZeroPad(hex, 2);
}

function rgbToHex(red, green, blue) {
  red = colorValue(red);
  green = colorValue(green);
  blue = colorValue(blue);
  
  return '#' + red + green + blue;
}

console.log(rgbToHex()); // "#000000"
console.log(rgbToHex(255)); // "#ff0000"
console.log(rgbToHex(255, 128)); // "#ff8000"
console.log(rgbToHex(255, 128, 64)); // "#ff8040"

```


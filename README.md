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
<hr/>

## DOM

### 1.Event handler on the parent
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
ok

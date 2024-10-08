# JSX Cheatsheet

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

If you're just starting to learn JSX and expressions for After Effects, it can be overwhelming to remember all the syntax and concepts involved. That's why I've created this JSX cheatsheet as a quick reference guide to help you when you get stuck.

## Declaration

In programming, a _declaration_ is a statement that tells the computer what a particular variable or function is going to be named and what type of value it will hold or return. To declare a variable in JavaScript, use the `var` keyword followed by the variable name. You can declare multiple variables in one line by separating them with a comma.&#x20;

```javascript
var myVariable;
var x,y,c
```

## Initialization

_Initialization_ is the process of giving a variable its first value when it is created. When you declare a variable, the computer sets aside a specific amount of memory to store its value. Initialization is the act of assigning a value to that memory location. To initialize a variable, assign a value to it using the = operator. You can initialize an array with multiple values using square brackets \[] and separating the values with commas.

```javascript
var myVariable = 5;
var myArray = [a,b,c,d,h,i,j,k];
```

## String

Strings are used to represent text in JavaScript.

```javascript
"string is text"
```

## For-Loops

For-loops are used to iterate over a block of code multiple times.

```javascript
for (var i = 0; i < value; i++) {
  // statement
}
```

## While Loops

While-loops are used to iterate over a block of code as long as a particular condition remains true.

```javascript
while (i < 20) {
  // statement
  i++
}
```

## If/Else Statements&#x20;

If/else statements are used to execute different blocks of code depending on whether a condition is true or false.

```javascript
if (x==20) {
  statement
} else {
  statement
}
```

### Shorthand If Statement

The shorthand if statement is used when you want to return a value based on a condition.

```javascript
if (x == 1) 10;
```

### Ternary

Ternary operations are a shorthand way to write if/else statements and return a value based on a condition.

```javascript
x = (y >= 5) ? 20 : 50;
```

## Function

A function is a block of code in programming that performs a specific task or set of tasks. It's like a reusable mini-program within a larger program. Imagine them as a pre-compositions in After Effects.

Functions are designed to take some input (known as **arguments** or parameters), process that input, and then **return** an output or perform an action.

Similar to variables, functions must be declared. In the below example, a function `double` that accepts an **argument** called `x` and **returns** the double of x :

```javascript
function double(x) {
  return 2 * x;
}
```

## Object

Objects in JavaScript are used to store collections of key/value pairs.

```javascript
var x = { firstName "John", lastName "Doe" };
```

## Single Line Comment

Single line comments are used to add comments to your code that will not be executed.

```java
// This is a single line comment
```

## Multi-Line Comment

Multi-line comments are used to add comments to your code that span multiple lines.

```javascript
/* This is a 
multi-line comment 
that spans multiple lines */
```

## Regular Expressions (Regex)

Regular expressions are patterns used to match character combinations in strings.

```javascript
"\n" // Line break
```

## Additional Readings

**JavaScript**

* [https://gitbook.gitbook.io/learn-javascript/](https://gitbook.gitbook.io/learn-javascript/)
* [https://learnjavascript.online/app.html?id=1437](https://learnjavascript.online/app.html?id=1437)

**Regex**

* [https://regexone.com](https://regexone.com)

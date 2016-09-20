# JavaScript Functions

You're already very familiar with the idea of wrapping our code as methods in
Ruby in order to make them reusable. In JavaScript, we call them functions and
the syntax is slightly different, but the general idea is the same.

## Objectives
+ Explain how function return values work
+ Write a function in JavaScript without parameters
+ Return a value from a function in JavaScript
+ Write a function with parameters
+ Write a function with default parameters

## Function Without Parameters

Here's the basic syntax for a function that doesn't take any parameters (you
know them as arguments):

```javascript
function nameOfFunction() {
  // code goes here
  return valueToReturn;
}
```

Notice the `def` keyword has been replaced with the `function` keyword. The name
of the function is always followed by `()` and then curly braces that begin and
end the function.

Further, the name of the function is not snake_cased, but rather
lowerCamelCased. Snakecase is not used in JavaScript so leave your underscores
at home people!

One last important thing to note is that JavaScript functions will always return
`undefined` unless you use the `return` keyword. In Ruby, writing `return` is
optional because Ruby always returns the value of the last line of code
evaluated. However, JavaScript has no implicit-return-value concept, so you must
write `return` before the value you want to return.

**NOTE**: This isn't exactly true in [ECMAScript 6](http://es6-features.org/).
For [arrow function](http://es6-features.org/#ExpressionBodies) expression
bodies that are not wrapped in curly brackets, you can omit the return:

``` javascript
[1, 2, 3, 4].filter(i => i % 2 === 0) // [2, 4]
```

But if you wrap the function body in curly brackets, you must explicitly
return your desired value:

``` javascript
[1, 2, 3, 4].filter(i => { return i % 2 === 0 }) // [2, 4]

// alternatively

[1, 2, 3, 4].filter(i => {
    return i % 2 === 0
})
```

Here's a simple example of a function that will will greet us good morning:

```javascript
function greet() {
  return "Good morning you!";
}
```

To call a function, you type the functions name followed by a beginning parenthesis and followed by an ending parenthesis, followed by a semicolon:

```javascript
// Returns "Good morning you!"
greet();
```

If you try to call on a function using just its name, as you can in Ruby, the entire function will get returned back to you instead of the function's return value so be careful!

```javascript
// Returns [Function: greet]
greet;
```

It's important to note that JavaScript does not run the code during a function definition. All it does is read that there is a function called `greet` and store it in memory. It doesn't actually create any of the variables inside the function (if there are any) until the method is called.

## Function Return Values

Unless you use the `return` keyword or call a function that explicitly returns a value, the implicit return value in JavaScript is  `undefined`.

> Undefined represents the absence of a primitive value

Other special return values in JavaScript are `null`

> Null represents the absence of an object

and `NaN`

> NaN represents an error from the improper use of a math operator.

## Parameters

The above is function is fine, but it could be better. For instance, what if you wanted your program to say the person's name instead of just "you" (ex. "Good morning Adam!" or "Good morning Steph!"). Well, just like in Ruby, you'd want to pass this function an argument. In JavaScript, arguments are called parameters.

```javascript
function greet(name) {
  return "Good morning " + name + "!";
}

// Returns "Good morning Adam!"
greet("Adam");

// Returns "Good morning Steph!"
greet("Steph");
```

Cool! So much better and more dynamic than having JavaScript return "Good morning you!". What if we also wanted it to greet us based on the time of day, for instance "Good afternoon Harold!" or "Good night Jasmine!"? Well, then we'd have to pass our function a second parameter, the time of day:

```javascript
function greet(name, timeOfDay) {
  return "Good "+ timeOfDay + " "+ name + "!";
}

// Returns "Good afternoon Harold!"
greet("Harold", "afternoon");

// Returns "Good night Jasmine!"
greet("Jasmine", "night");
```

Like in Ruby, you can add as many parameters to your JavaScript functions as you like. Or you can pass them none. Just depends on what task you're trying to accomplish.

## Function Expression

There are two different ways to write functions in JavaScript. You can write
them as a function **declaration** which is how we've been writing them, or as a
function *expression**.

A function expression looks something like this:

```js
var greet = function(name, timeOfDay){
  return "Good "+ timeOfDay + " "+ name + "!";
};
```

We can still call this function in the same way we would a function written with a function declaration:

```js
// Returns "Good afternoon Grover!"
greet("Grover", "afternoon");
```

Function declarations are hoisted to the top of the current scope; function
expressions are not.

``` javascript

// this works, even though we're calling
// the function before the declaration —
// the `sayGoodbye` function is *hoisted*
// to the top of the current scope when
// the script is evaluated
sayGoodbye();

function sayGoodbye() {
    return 'Goodbye!';
}


// this does not work, as the function
// is not hoisted in a function expression

sayHello(); // TypeError: sayHello is not a function

var sayHello = function() {
    return 'Hello!';
};
```

It's good to be familiar with both ways of writing a function for when you start
working with other developers, or using Google resources for help.

## Default parameters

Ruby has an idea of allowing you to pass optional arguments by defaulting
argument values. To create a default argument, you add an equal sign where you
define the variable name of your argument and set it equal to the value you want
it to default to:

```ruby
def greet(name="you")
  "Good morning #{name}!";
end
```

This way, you can call on the method with the argument and it will set `name` to
be the string you passed.

Ruby:

```ruby
greet("Jasmine")
# => "Good morning Jasmine!"
```

**or** you can call on the method without the argument and `name` will default
to the string `"you"`:

```ruby
greet
# => "Good morning you!"
```

In JavaScript, you can make functions behave has though they have default
arguments. Here again is the simple greeting function:

```javascript
function greet(name) {
  return "Good morning " + name + "!";
}
```

To give the variable `name` a default value, you check to see if `name` has been
defined on the first line of your function. To do this, you call JavaScript's
`typeof` operator, which is a lot like calling `.class` in Ruby.
If the function wasn't passed a parameter, then the variable will be
`"undefined"`.

```javascript
function greet(name) {
  if (typeof name === "undefined") {
    // add code
  }
  return "Good morning " + name + "!";
}
```

Inside the `if` statement, go ahead and set the default value you desire:

```javascript
function greet(name) {
  if (typeof name === "undefined") {
    name = "you";
  }
  return "Good morning " + name + "!";
}
```

Let's now see our function in action:

```javascript
// Returns "Good morning Blake!"
greet("Blake");

// Returns "Good morning you!"
greet();
```

Unlike Ruby, JavaScript doesn't force you to call a function with a set number
of parameters. If a JavaScript function it defined to accept two parameters, and
you call the function with only one parameter, the function will still run, but
place `undefined` in the spot of the missing paramater:

```js
function greet(name, timeOfDay) {
  return "Good "+ timeOfDay + " "+ name + "!";
}

greet("joe");
// returns "Good undefined joe!"
```

Be careful when calling functions with parameters. This could inadvertently mess
up your return values.

### **ES6 Note**

ECMAScript 6 introduces [default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
in JavaScript. Their syntax should look familiar:

``` javascript
function greet(name="Sue", timeOfDay="morning") {
    return "Good " + timeOfDay + " " name + "!";
}

// 'Good morning, Sue!'
greet();

// 'Good morning, George!'
greet('George');

// 'Good afternoon, Dory!'
greet('Dory', 'afternoon');
```

## Example

If you'd like more practice with JavaScript functions, this section covers how to rewrite a Ruby method that converts feet to meters in JavaScript. Here's that Ruby method:

```ruby
def convert_to_meters(feet)
  meters = feet / 3.2808
  rounded = meters.round(2)
  "#{rounded} meters"
end
```

Now let's make it a JavaScript function!

The first step is to change the `def` keyword into a `function` keyword. The next step is to change the method's name, which is in snake case, into lower camelCase. The third step will be to change the `end` keyword into an ending curly brace and add a beginning curly brace after the argument, like so:

```javascript
function convertToMeters(feet) {
  // add code
  // add code
  // add code
}
```

The next step is to take the variable, `meters` and preempt it with the keyword `var` so that it's limited in its scope. We'll then end that line of code with a semicolon:

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  // add code
  // add code
}
```

Just like we changed the `meters` variable from having a global scope to having a local scope, we'll do the same for the `rounded` variable:

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  var rounded = // add code
  // add code
}
```

To round a float in JavaScript, you call `.toFixed()` on the number. If you're operating on the literal number, remember to wrap it in parentheses, but since we're storing it in the variable `num`, we don't have to worry about that. You then pass `.toFixed()` a parameter, the number 2, meaning you would like two digits after the decimal:

```javascript
var num = 3.14159;

// Returns the number 3.14
num.toFixed(2);
```

Let's incorporate the `.toFixed()` function to the second line of our new JavaScript function:

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  var rounded = meters.toFixed(2);
  // add code
}
```

Finally, let's concatenate our rounded meter value with the string " meters":

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  var rounded = meters.toFixed(2);
  rounded + " meters";
}
```

This looks about right. To see if this function works, we'll call on the function by name, just like in Ruby:

```javascript
// Returns undefined
convertToMeters(16)
```

Alright, so instead of getting our desired result of `"4.88 meters"`, we got `undefined`. As mentioned above, this is because JavaScript functions, unlike Ruby methods, will always return `undefined` unless you use the `return` keyword. Let's add that keyword to the left of the function's last line:

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  var rounded = meters.toFixed(2);
  return rounded + " meters";
}
```

And if we try to run our function again, we can see if that did the trick:

```
// Returns "4.88 meters"
convertToMeters(16)
```

And it did! Now try this out for yourself. Turn the Ruby method below into a JavaScript function. If you get stuck, take a look at the solution at the end of this document.

```ruby
def convert_to_fahrenheit(celsius=0)
  celsius *  9/5 + 32
end
```

## Resources

* [Eloquent JavaScript - Functions](http://eloquentjavascript.net/03_functions.html)
* [MDN - Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)
* [MDN - Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [MDN - Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

## Solution

Here's the Ruby method that converts Celsius to Fahrenheit:

```ruby
def convert_to_fahrenheit(celsius=0)
  (celsius *  9/5) + 32
end
```

Here's the JavaScript method that converts Celsius to Fahrenheit:

```javascript
function convertToFahrenheit(celsius) {
  if (typeof(celsius) === "undefined") {
    var celsius = 0;
  }
  return (celsius *  9/5) + 32;
}
```

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/intro-to-functions.js' title='JavaScript Functions'>JavaScript Functions</a> on Learn.co and start learning to code for free.</p>

# JavaScript Functions

## Overview

* About
* Syntax
* Parameters
* Default parameters
* Example
* Resources
* Solution

## About

In Ruby, it's a common practice to wrap code that you reuse in a method using the `def` keyword. For example, let's take a look at this conversion method that takes feet and returns meters:

```ruby
def convert_to_meters(feet)
  meters = feet / 3.2808
  rounded = meters.round(2) 
  "#{rounded} meters"
end

convert_to_meters(16)
# => "4.88 meters"
```

Notice that the return value of a Ruby method is the return value for the last line of code that the method evaluated.

JavaScript also had a way to wrap lines of code into reusable chunks. Instead of calling them methods as we do in Ruby, these wrapped lines of code are called functions. 

## Syntax

Here's the basic syntax for a function that doesn't take any parameters (you know them as arguments):

```javascript
function nameOfFunction() {
  // code goes here
  return valueToReturn;
}
```

Notice that curly braces begin and end the function and that the `def` keyword has been replaced with the `function` keyword. 

Further, the name of the function is not snake_cased, but rather lowerCamelCased. Snakecase is not used in JavaScript so leave your underscores at home people!

One last important thing to note is that JavaScript functions will always return `undefined` unless you use the `return` keyword. In Ruby, writing `return` was optional because Ruby always returns the value of the last line of code evaluated. However, JavaScript has no implicit-return-value concept, so you must write `return` before the value you want to return.

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

## Default parameters

Ruby has an idea of allowing you to pass optional arguments by defaulting argument values. To create a default argument, you add an equal sign where you define the variable name of your argument and set it equal to the value you want it to default to:

```ruby
def greet(name="you")
  "Good morning #{name}!";
end
```

This way, you can call on the method with the argument and it will set `name` to be the string you passed:

```ruby
greet("Jasmine")
# => "Good morning Jasmine!"
```

**or** you can call on the method without the argument and `name` will default to the string `"you"`:

```ruby
greet
# => "Good morning you!"
```

You can make functions that behave as though they have default arguments using JavaScript. Here again is the simple greeting function:

```javascript
function greet(name) {
  return "Good morning " + name + "!";
}
```

To give the variable `name` a default value, you check to see if `name` has been defined on the first line of your function. To do this, you call JavaScript's `typeof()` function, which is a lot like calling `.class` in Ruby. If the function wasn't passed a parameter, then the variable you defined will be `"undefined"`. 

```javascript
function greet(name) {
  if (typeof(name) === "undefined") {
    // add code
  }
  return "Good morning " + name + "!";
}
```

Inside the `if` statement, go ahead and set the default value you desire:

```javascript
function greet(name) {
  if (typeof(name) === "undefined") {
    var name = "you";
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

And that's all there is for optional parameters folks!

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

To round a float in JavaScript, you wrap the number in parentheses and then call `.toFixed()` on the number. You then pass the function `.toFixed()` the number 2, meaning you would like two digits after the decimal.

```javascript
var num = 3.14159;

// Returns the number 3.14 
(num).toFixed(2);
```

Let's incorporate the `.toFixed()` function to the second line of our new JavaScript function:

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  var rounded = (meters).toFixed(2);
  // add code
}
```

Finally, let's concatenate our rounded meter value with the string " meters":

```javascript
function convertToMeters(feet) {
  var meters = feet / 3.2808;
  var rounded = (meters).toFixed(2);
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
  var rounded = (meters).toFixed(2);
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
* [MDN - Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

## Solution

Here's the Ruby method that converts Celsius to Fahrenheit:

```ruby
def convert_to_fahrenheit(celsius=0)
  celsius *  9/5 + 32
end
```

Here's the JavaScript method that converts Celsius to Fahrenheit:

```javascript
function convertToFahrenheit(celsius) {
  if (typeof(celsius) === "undefined") {
    var celsius = 0;
  }
  return celsius *  9/5 + 32;
}
```

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/intro-to-functions.js' title='JavaScript Functions'>JavaScript Functions</a> on Learn.co and start learning to code for free.</p>

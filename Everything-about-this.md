[Why and how to bind methods in your React component classes?](http://reactkungfu.com/2015/07/why-and-how-to-bind-methods-in-your-react-component-classes/)

Four patterns of invoking functions that defines the context of the function being called:

> JavaScript works quite surprisingly here. Because in JavaScript function context is defined while calling the function, not while defining it! 

## Function invocation pattern
```javascript
var func = function() {
  // ...
};

func();
```
Calling function in this way will set its context (this) to a global variable of an environment.
```javascript
var unicorns = {
  func: function() { // ... }
};

var fun = unicorns.func;
fun();
```
In this way, the context of the function 'func' will be changed from unicorn to the global variable. The context binding is determined by the way you call this function.

## Method invocation pattern
If the function is defined within an object, calling it directly from an object will set its context to the object on which the function is being called.
```javascript
var frog = {
  RUN_SOUND: "POP!!",
  run: function() {
    return this.RUN_SOUND;
  }
};

frog.run(); // returns "POP!!" since this points to the `frog` object.
var runningFun = frog.run;
runningFun(); // returns "undefined" since this points to the window
```
If object is nested, the most nested object will be set as a context of the function call.
```javascript
var foo = {
  bar: {
    func: function() { ... }
  }
};

foo.bar.func(); // this will point to `bar`
```
## Constructor invocation pattern

> Every time you see a new followed by a function name, your this will point to a newly created empty object.

```javascript
function Wizard() {
  this.castSpell = function() { return "KABOOM"; };
}

var merlin = new Wizard(); // this is set to an empty object {}. Returns `this` implicitly.
merlin.castSpell() // returns "KABOOM";
```


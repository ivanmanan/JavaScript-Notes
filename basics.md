# Introduction to JavaScript

## Developer Tools Console

```js
    console.log("variable");
    console.alert("variable");
    prompt("variable");
```

## Operators in JavaScript

* Assignment: `=` as in `a = 2`.
* Math: `+` (addition), `-` (subtraction), `*` (multiplication), and `/` (division), as in `a * 3`.
* Compound Assignment: `+=`, `-=`, `*=`, and `/=` are compound operators that combine a math operation with assignment, as in `a += 2` (same as `a = a + 2`).
* Increment/Decrement: `++` (increment), `--` (decrement), as in `a++` (similar to `a = a + 1`).
* Object Property Access: `.` as in `console.log()`.

   Objects are values that hold other values at specific named locations called properties. `obj.a` means an object value called `obj` with a property of the name `a`. Properties can alternatively be accessed as `obj["a"]`. See Chapter 2.
* Equality: `==` (loose-equals), `===` (strict-equals), `!=` (loose not-equals), `!==` (strict not-equals), as in `a == b`.

   See "Values & Types" and Chapter 2.
* Comparison: `<` (less than), `>` (greater than), `<=` (less than or loose-equals), `>=` (greater than or loose-equals), as in `a <= b`.

   See "Values & Types" and Chapter 2.
* Logical: `&&` (and), `||` (or), as in `a || b` that selects either `a` *or*
  `b`.

## Types and Coercion

Coercion - Converting from one type to another; e.g. converting a number to a
string or vice versa.

For the `==` loose equals operator, as in `"99.99" == 99.99`, JavaScript will
convert the left-hand side to its number form `99.99`. The comparison then
becomes `99.99 == 99.99`, which is `true`.

## Variables

Static Typing - type enforcement; a variable is declared to hold a specific type
of value, such as `number` or `string`. C++ uses static typing.

Weak Typing - dynamic typing; allows a variable to hold any type of value at any
time. JavaScript uses dynamic typing.

## Functions

Example

```js
    function printAmount() {
        console.log( amount.toFixed( 2 ) );
    }

    var amount = 99.99;

    printAmount(); // "99.99"

    amount = amount * 2;

    printAmount(); // "199.98"
```

## Scope

Technically called lexical scope.

In JavaScript, each function gets its own scope. Scope is a collection of
variables as well as the rules for how those variables are accessed by
name. Only code inside that function can access that function's scoped
variables.

Examples

```js
    function one() {
	    // this `a` only belongs to the `one()` function
	    var a = 1;
	    console.log( a );
    }

    function two() {
	    // this `a` only belongs to the `two()` function
	    var a = 2;
	    console.log( a );
    }

    one();		// 1
    two();		// 2
```

```js
function outer() {
	var a = 1;

	function inner() {
		var b = 2;

		// we can access both `a` and `b` here
		console.log( a + b );	// 3
	}

	inner();

	// we can only access `a` here
	console.log( a );			// 1
}

outer();
```

Lexical scope rules say that code in one scope can access variables of either
that scope or any scope outside of it.

Code inside the `inner()` function has access to both variables `a` and `b`, but
code in `outer()` has only access to variable `a` - it cannot access `b` because
that variable is only inside `inner()`.

# Basics of JavaScript

## Values and Types
JavaScript has typed values, not typed variables. The built-in types are:
* `string`
* `number`
* `boolean`
* `null` and `undefined`
* `object`
* `symbol` (ES6)

JavaScript provides a `typeof` operator that can examine a value and tell you
the type.

```js
var a;
typeof a;				// "undefined"

a = "hello world";
typeof a;				// "string"

a = 42;
typeof a;				// "number"

a = true;
typeof a;				// "boolean"

a = null;
typeof a;				// "object" -- weird, bug

a = undefined;
typeof a;				// "undefined"

a = { b: "c" };
typeof a;				// "object"
```
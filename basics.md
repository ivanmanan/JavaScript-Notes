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
typeof a;				// "objec"t
```

## Objects

The `object` type refers to a compound value where you can set properties (named
locations) that each hold their own values of any type.

```js
var obj = {
	a: "hello world",
	b: 42,
	c: true
};

obj.a;		// "hello world"
obj.b;		// 42
obj.c;		// true

obj["a"];	// "hello world"
obj["b"];	// 42
obj["c"];	// true
```

Properties can either be accessed with dot notation (i.e. `obj.a`) or bracket
notation (i.e. `object["a"]`).

Why use bracket notation? When you want to access a property/key but the name is
stored in another variable, such as

```js
var obj = {
	a: "hello world",
	b: 42
};

var b = "a";

obj[b];			// "hello world"
obj["b"];		// 42
```

Arrays and functions are thought of as specialized versions of the `object` type.

### Arrays
An array is an `object` that holds values (of any type) not particularly in
named properties/keys, but rather in numerically indexed positions.

Example
```js
var arr = [
	"hello world",
	42,
	true
];

arr[0];			// "hello world"
arr[1];			// 42
arr[2];			// true
arr.length;		// 3

typeof arr;		// "object"
```

Arrays have built-in properties, such as `length`.

The most natural approach is to use arrays for numerically positioned values and
use `objects` for named properties.

### Functions
Functions are a subtype of `objects`.

## Built-In Type Methods
The built-in types and subtypes have properties and methods that are useful.

Example
```js
var a = "hello world";
var b = 3.14159;

a.length;				// 11
a.toUpperCase();		// "HELLO WORLD"
b.toFixed(4);			// "3.1416"
```

The "how" behind being able to call `a.toUpperCase()` is more complicated than just that method existing on the value.

## Comparing Values
Two forms of coercion - explicit and implicit.

Explicit Coercion - You can see obviously from the code that a conversion from
one type to another will occur.

Example of explicit coercion
```js
var a = "42";

var b = Number( a );

a;				// "42"
b;				// 42 -- the number!
```

Implicit Coercion - The type conversion can happen as more of a non-obvious side
effect of some other operation.

Example of implicit coercion
```js
var a = "42";

var b = a * 1;	// "42" implicitly coerced to 42 here

a;				// "42"
b;				// 42 -- the number!
```

### True or False
Specific list of "false" values in JavaScript:
* `""` (empty string)
* `0`, `-0`, `NaN` (invalid `number`)
* `null`, `undefined`
* `false`

Anything other than the values in the "false" list are considered "true". This
includes:
* `[]`, `{}` (empty arrays, empty objects)

### Equality operators
Four equality operators: `==`, `===`, `!=`, `!==`

The difference between `==` and `===` is that `==` checks for value equality
with coercion allowed while `===` checks for value equality without allowing
coercion. Hence, `===` is considered as "strict equality".

Example
```js
var a = "42";
var b = 42;

a == b;			// true
a === b;		// false
```

The coercion goes from `string` to `number`.

When to use `==` and `===`:
* If either value (aka side) in a comparison could be the `true` or `false` value, avoid `==` and use `===`.
* If either value in a comparison could be of these specific values (`0`, `""`, or `[]` -- empty array), avoid `==` and use `===`.
* In *all* other cases, you're safe to use `==`. Not only is it safe, but in many cases it simplifies your code in a way that improves readability.

When using the equality operator with `objects`, their values are held by
reference so both `==` and `===` will check whether the references match.

Example
```js
var a = [1,2,3];
var b = [1,2,3];
var c = "1,2,3";

a == c;		// true
b == c;		// true
a == b;		// false
```

### Inequalities

Example
```js
var a = 41;
var b = "42";
var c = "43";

a < b;		// true
b < c;		// true
```
When comparing `strings`, the comparison is made lexicographically
(alphabetically like a dictionary). If one or both are not `strings`, then both
values are coerced to be `numbers`.

```js
var a = 42;
var b = "foo";

a < b;		// false
a > b;		// false
a == b;		// false
```

The value of `b` is being coerced to the "invalid number value" `NaN` in the
comparison operators. `NaN` is neither greater-than nor less-than any other
value.

## Variables
A variable must start with `a`-`z`, `A`-`Z`, `$`, or `_`. It can then contain
any of those characters and the numerals `0`-`9`.

Certain words cannot be used as variables, but are OK as property names. They
are called "reserved words", such as `for`, `in`, `if`, `null`, `true`, `false`.

### Function Scopes
You can use `var` to declare a variable that will belong to the current function
scope, or the global scope if at hte top level outside of any function.

#### Hoisting
Whenever a `var` appears inside a scope, that declaration is taken to belong to
the entire scope and accessible everywhere throughout.

Hoisting - when a `var` declaration is conceptually "moved" to the top of its
enclosing scope.

Example
```js
var a = 2;

foo();					// works because `foo()`
						// declaration is "hoisted"

function foo() {
	a = 3;

	console.log( a );	// 3

	var a;				// declaration is "hoisted"
						// to the top of `foo()`
}

console.log( a );	// 2
```

Warning: It's not common or a good idea to rely on variable hoisting to use a variable earlier in its scope than its `var` declaration appears; it can be quite confusing. It's much more common and accepted to use hoisted function declarations, as we do with the `foo()` call appearing before its formal declaration.

#### Nested Scopes
When you declare a variable, it is available anywhere in that scope, as well as any lower/inner scopes. For example:

```js
function foo() {
	var a = 1;

	function bar() {
		var b = 2;

		function baz() {
			var c = 3;

			console.log( a, b, c );	// 1 2 3
		}

		baz();
		console.log( a, b );		// 1 2
	}

	bar();
	console.log( a );				// 1
}

foo();
```

Notice that `c` is not available inside of `bar()`, because it's declared only inside the inner `baz()` scope, and that `b` is not available to `foo()` for the same reason.

If you try to access a variable's value in a scope where it's not available, you'll get a `ReferenceError` thrown. If you try to set a variable that hasn't been declared, you'll either end up creating a variable in the top-level global scope (bad!) or getting an error, depending on "strict mode" (see "Strict Mode"). Let's take a look:

```js
function foo() {
	a = 1;	// `a` not formally declared
}

foo();
a;			// 1 -- oops, auto global variable :(
```
This is bad practice. Never do this; always declare variables.

In addition to creating declarations for variables at the function level, ES6 lets you declare variables to belong to individual blocks (pairs of `{ .. }`), using the `let` keyword. Besides some nuanced details, the scoping rules will behave roughly the same as we just saw with functions:

```js
function foo() {
	var a = 1;

	if (a >= 1) {
		let b = 2;

		while (b < 5) {
			let c = b * 2;
			b++;

			console.log( a + c );
		}
	}
}

foo();
// 5 7 9
```
Because of using `let` instead of `var`, `b` will belong only to the `if` statement and thus not to the whole `foo()` function's scope. Similarly, `c` belongs only to the `while` loop. Block scoping is very useful for managing your variable scopes in a more fine-grained fashion, which can make your code much easier to maintain over time.

## Strict Mode
ES5 added a "strict mode" to JavaScript. Should use it for all programs since it
makes the code safer.

The placement of the `"use strict";` pragma matters.

Compare this to the function right below:
```js
function foo() {
	"use strict";

	// this code is strict mode

	function bar() {
		// this code is strict mode
	}
}

// this code is not strict mode
```

```js
"use strict";

function foo() {
	// this code is strict mode

	function bar() {
		// this code is strict mode
	}
}

// this code is strict mode
```

One key difference (improvement!) with strict mode is disallowing the implicit auto-global variable declaration from omitting the `var`:

```js

function foo() {
	"use strict";	// turn on strict mode
	a = 1;			// `var` missing, ReferenceError
}

foo();
```

## Functions As Values

All `function` names are variables that are given references to the `function`
being declared.

```js
var foo = function() {
	// ..
};

var x = function bar(){
	// ..
};
```

The first function `foo` is called *anonymous* because it has no `name`.

Second function expression is named `bar`.

### Immediately Invoked Function Expressions (IIFEs)

```js
(function IIFE(){
	console.log( "Hello!" );
})();
// "Hello!"
```

These are the same:
```js
function foo() { .. }

// `foo` function reference expression,
// then `()` executes it
foo();

// `IIFE` function expression,
// then `()` executes it
(function IIFE(){ .. })();
```

Since functions create variable scope, using an IIFE to declare variables won't
affect the surrounding code outside the IIFE:
```js
var a = 42;

(function IIFE(){
	var a = 10;
	console.log( a );	// 10
})();

console.log( a );		// 42
```

## Closure
Think of closure as a way to "remember" and continue to access a function's
scope (its variables) even once the function has finished running.

```js
function makeAdder(x) {
	// parameter `x` is an inner variable

	// inner function `add()` uses `x`, so
	// it has a "closure" over it
	function add(y) {
		return y + x;
	};

	return add;
}
```

The reference to the inner `add(..)` function that gets returned with each call to the outer `makeAdder(..)` is able to remember whatever `x` value was passed in to `makeAdder(..)`. Now, let's use `makeAdder(..)`:

```js
// `plusOne` gets a reference to the inner `add(..)`
// function with closure over the `x` parameter of
// the outer `makeAdder(..)`
var plusOne = makeAdder( 1 );

// `plusTen` gets a reference to the inner `add(..)`
// function with closure over the `x` parameter of
// the outer `makeAdder(..)`
var plusTen = makeAdder( 10 );

plusOne( 3 );		// 4  <-- 1 + 3
plusOne( 41 );		// 42 <-- 1 + 41

plusTen( 13 );		// 23 <-- 10 + 13
```

1. When we call `makeAdder(1)`, we get back a reference to its inner `add(..)` that remembers `x` as `1`. We call this function reference `plusOne(..)`.
2. When we call `makeAdder(10)`, we get back another reference to its inner `add(..)` that remembers `x` as `10`. We call this function reference `plusTen(..)`.
3. When we call `plusOne(3)`, it adds `3` (its inner `y`) to the `1` (remembered by `x`), and we get `4` as the result.
4. When we call `plusTen(13)`, it adds `13` (its inner `y`) to the `10`
   (remembered by `x`), and we get `23` as the result.

### Modules
Most common usage of closure in JavaScript is the module pattern. Modules let
you define private implementation details (variables, functions) that are hidden
from the outside world, as well as a public API that is accessible from the
outside.

```js
function User(){
	var username, password;

	function doLogin(user,pw) {
		username = user;
		password = pw;

		// do the rest of the login work
	}

	var publicAPI = {
		login: doLogin
	};

	return publicAPI;
}

// create a `User` module instance
var fred = User();

fred.login( "fred", "12Battery34!" );
```


The `User()` function serves as an outer scope that holds the variables `username` and `password`, as well as the inner `doLogin()` function; these are all private inner details of this `User` module that cannot be accessed from the outside world.

**Warning:** We are not calling `new User()` here, on purpose, despite the fact that probably seems more common to most readers. `User()` is just a function, not a class to be instantiated, so it's just called normally. Using `new` would be inappropriate and actually waste resources.

Executing `User()` creates an *instance* of the `User` module -- a whole new scope is created, and thus a whole new copy of each of these inner variables/functions. We assign this instance to `fred`. If we run `User()` again, we'd get a new instance entirely separate from `fred`.

The inner `doLogin()` function has a closure over `username` and `password`, meaning it will retain its access to them even after the `User()` function finishes running.

`publicAPI` is an object with one property/method on it, `login`, which is a reference to the inner `doLogin()` function. When we return `publicAPI` from `User()`, it becomes the instance we call `fred`.

At this point, the outer `User()` function has finished executing. Normally, you'd think the inner variables like `username` and `password` have gone away. But here they have not, because there's a closure in the `login()` function keeping them alive.

That's why we can call `fred.login(..)` -- the same as calling the inner `doLogin(..)` -- and it can still access `username` and `password` inner variables.

## `this` Identifier
While it may often seem that `this` is related to "object-oriented patterns," in
JavaScript `this` is a different mechanism.

If a function has a `this` reference inside it, that `this` reference usually
points to an `object`. But which `object` it points to depends on how the
function was called.

Note: `this` does not refer to the function itself, as is the most common
misconception.

```js
function foo() {
	console.log( this.bar );
}

var bar = "global";

var obj1 = {
	bar: "obj1",
	foo: foo
};

var obj2 = {
	bar: "obj2"
};

// --------

foo();				// "global"
obj1.foo();			// "obj1"
foo.call( obj2 );		// "obj2"
new foo();			// undefined
```

There are four rules for how `this` gets set, and they're shown in those last four lines of that snippet.

1. `foo()` ends up setting `this` to the global object in non-strict mode -- in strict mode, `this` would be `undefined` and you'd get an error in accessing the `bar` property -- so `"global"` is the value found for `this.bar`.
2. `obj1.foo()` sets `this` to the `obj1` object.
3. `foo.call(obj2)` sets `this` to the `obj2` object.
4. `new foo()` sets `this` to a brand new empty object.

## Prototypes

When you reference a property on an object, if that property doesn't exist, JavaScript will automatically use that object's internal prototype reference to find another object to look for the property on. You could think of this almost as a fallback if the property is missing.

The internal prototype reference linkage from one object to its fallback happens at the time the object is created. The simplest way to illustrate it is with a built-in utility called `Object.create(..)`.

```js
var foo = {
	a: 42
};

// create `bar` and link it to `foo`
var bar = Object.create( foo );

bar.b = "hello world";

bar.b;		// "hello world"
bar.a;		// 42 <-- delegated to `foo`
```

The `a` property doesn't actually exist on the `bar` object, but because `bar` is prototype-linked to `foo`, JavaScript automatically falls back to looking for `a` on the `foo` object, where it's found.

The most common way this feature is used (or abused) is to emulate/fake a
"class" mechanism with "inheritance".

But a more natural way of applying prototypes is a pattern called "behavior delegation," where you intentionally design your linked objects to be able to delegate from one to the other for parts of the needed behavior.

## Old And News
What happens if a JavaScript feature does not work in an older browser?

Solution: Polyfilling and Transpiling.

### Polyfilling
Polyfill - taking the definition of a newer feature and producing a piece of
code that's equivalent to the behavior, but is able to run in older JS
environments.

Example: If the user is not in an ES6 browser, this is the back-up polyfill code
that can be used:
```js
if (!Number.isNaN) {
	Number.isNaN = function isNaN(x) {
		return x !== x;
	};
}
```
If the ES6 feature is not present, an `if` statement like this would be
executed.

### Transpiling
Transpiling - a process that converts newer code into older code equivalents; a
term for transforming + compiling.

ES6 only:
```js
function foo(a = 2) {
	console.log( a );
}

foo();		// 2
foo( 42 );	// 42
```

In pre-ES6 engines, transpiler will do this:
```js
function foo() {
	var a = arguments[0] !== (void 0) ? arguments[0] : 2;
	console.log( a );
}
```

Babel transpiles ES6+ into ES5.


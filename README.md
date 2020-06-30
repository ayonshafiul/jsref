# jsref
JS reference
# Primitive Types
```javascript
// Primitive types [Number, String, Boolean, Undefined, Null, Object, Symbol]
// Variables do not have types, the values do
// Use typeof operator to see the type of a variable in "string"
var a; 
typeof a; // undefined {default value of uninitialized variables}
a = 4;
typeof a; // "number"
a = 'Hello';
typeof a; // "string"
a = "World";
typeof a; // "string"
a = true;
typeof a; // "boolean"
a = {};
typeof a; // "object"
a = Symbol();
typeof a; // "symbol"
a = null;
typeof a; // "object" "oooooopss"
a = function() {};
typeof a; // "function"
a = [1, 2, 3];
typeof a; // "object"
Array.isArray(a); // true

// undefined is by default set to declared but not initialized variables
// undeclared variables return a ReferenceError

// special values
a = NaN;
typeof a; // "number"
isNaN(a); // true
NaN === NaN; // false {NaN is the only value in javascript that is not equal to itself}
isNaN("hello"); // true
Number.isNaN("hello"); // false
Object.is(NaN, NaN); // true

// Object representation of types
a = new Number(); // 0
a = Number(); // 0

a = new Number(1);
typeof a; // "object" {Hidden property [[PrimitiveValue]] holds 1}
a = Number(1);
typeof a; // "number" {call to Number() function coerces to number primitive}
a = Boolean(); // false
a = String(); // ""

```

# Coersion

```javascript
// Convert to string
// first toString() then valueOf()
var a;
a = String(null); // "null"
a = String(undefined); // "undefined"
a = String(true); // "true"
a = String(false); // "false"
a = String(-0); // "0"
a = String([]); // ""
a = String([1,2,3]); // "1,2,3"
a = String([null, undefined]); // "," {ignores null and undefined}
a = String([null, undefined, 1, , 3]); // ",,1,,3"
a = String({}); // "[object Object]" 


// Convert to number
// first valueOf() then toString()
var a;
a = Number(""); // 0 {oops}
a = Number("-0"); // -0 
a = Number("  0056 "); // 56 {trims whitespaces and leading zeros}
a = Number("0."); // 0
a = Number(" .001"); // 0.001 {adds 0.} 
a = Number("."); // NaN {only dots are invalid}
a = Number(null); // 0 {oops}
a = Number(undefined); // NaN 
a = Number(true); // 1
a = Number(false); // 0
a = Number("true"); // NaN
a = Number([]); // 0 { #1: first [] converts to "" then "" becomes 0}
a = Number([""]); // 0 #1
a = Number([null]); // 0 #1
a = Number([undefined]); // 0 #1
a = Number([1,2,3]); // NaN
a = Number({}); // NaN

// Convert to boolean
// Falsy list: 0, -0, null, undefined, false, "", NaN
// If the value is not on the falsy list then it is true
var a;
a = Boolean(0); // false 
a = Boolean(null); // false
a = Boolean(undefined); // false
a = Boolean(false); // false
a = Boolean(NaN); // false
a = Boolean(""); // false
a = Boolean("anything else"); // true

```

# Equality

```javascript

// if the types match then == performs strict equality ===
var word1 = "hello";
var word2 = "hello";

word1 == word2; // true
word1 === word2; // true

// double equals allows coersion only if the types are different and prefers to convert to number

var x = null;
var y = undefined;
x == y; // true

x = undefined;
y = null;
x == y; // true;

x = 16;
y = "16";
x == y; // true

x = true;
y = 1;
x == y; // true

x = false;
y = 0;
x == y; // true

x = 16;
y = [16];
x == y; // true {[16] => "16" => 16}

// triple equals disallows coersion and returns false if the types are different

x = "16"; 
y = 16;
x === y; // false

x = -0;
y = 0;
x === y; // true

x = {x: 2};
y = {x: 2};
x == y; // false

x = {x: 2};
y = x;
x === y; // true;

```

# Scope

```javascript
// lexical scope refers to the idea of scopes being nested inside each other and determined at compile time by the author

// js is lexically scoped

// js functions create new scopes

function abc(word) {
    console.log(word)
    function xyz() {
        console.log("Bye");
    } // xyz is declared within the scope of abc
    xyz();
} // abc is declared in the global scope

abc("Hi");
xyz(); //Reference Error


// function expression

var abc = function xyz() {
    console.log(abc);
}
xyz(); // Reference Error
abc(); // works { #2 functions expressions do not pollute the enclosing scope }

// scopes using IIFE

(function xyz(word) {
    console.log(word);
})("HI"); // works because #2

xyz(); // Reference Error

// scopes using let or const inside Blocks

{
    let abc = "HI";
    console.log(abc);
}

abc; // Reference Error

// var vs let

function abc() {
    try {
        var a = 1;
    } catch (err) {
        var a = 2;
    }
    var a = 3; // redeclaring var is allowed
    console.log(a);
}
abc();

function abc() {
    let a;
    try {
        let a = 1; // Syntax error
    } catch (err) {
        let a = 2;
    }
    let a = 3; // Syntax error {redeclaring let is dis allowed}
    console.log(a);
}

abc();

// let doesn't hoist

// const

{
    const a = "HI";
    const b = { x: 2};
    b.x = 3; // allowed
    a = 4; // TypeError
}


```
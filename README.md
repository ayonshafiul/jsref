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
typeof a; // "number" {call to Number() function coercers to number primitive}
a = Boolean(); // false
a = String(); // ""

```


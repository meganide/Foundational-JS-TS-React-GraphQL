# Javascript

## Event Loop
Javascript is single threaded, meaning it can execute one piece of code at a time.
In order to avoid freezing the entire app while we do long running tasks like API calls, background jobs, I/O etc. we have the event loop in which we can send these tasks to run in the background to not block the main thread.

The event loop is JavaScript's mechanism for handling asynchronous operations. The call stack executes synchronous code, while the event loop manages the callback queue and microtask queue, processing them when the call stack is empty.

## Race conditions
A race condition happens when two or more parts of a program try to access or modify shared data at the same time, and the final result depends on the order in which things happen — which is often unpredictable.

A race condition is when timing decides your program’s result — and that’s dangerous, because timing can change every run.

## Data Types

### Primitive values
- **String:** Text data (e.g., "hello")
- **Number:** Integers and floats (e.g., 42, 3.14)
- **Boolean:** true or false
- **Undefined:** Variable declared but not assigned
- **Null:** Intentional absence of value
- **Symbol:** Unique identifier (ES6+)
- **BigInt:** Large integers beyond Number.MAX_SAFE_INTEGER

--> Stored by value in memory

### Non-Primitive values
- **Object:** Collections of key-value pairs (includes arrays, functions, dates, etc.)
- **Array:** Ordered lists of values
- **Function:** Reusable blocks of code
- **Date:** Date and time objects

--> Stored by reference in memory

## Variables

### Var
- **Function-scoped:** Accessible throughout the entire function
- **Hoisted:** Declaration moved to top of scope (initialized as undefined)
- **Can be redeclared:** Same variable name can be declared multiple times
- **No block scope:** Ignores block boundaries (if, for, while)

### Let
- **Block-scoped:** Confined to the nearest block (loops, conditionals)
- **Hoisted but not initialized:** Exists in "temporal dead zone" until declaration
- **Cannot be redeclared:** Same name cannot be declared twice in same scope
- **Can be reassigned:** Value can be changed after declaration

### Const
- **Block-scoped:** Confined to the nearest block
- **Must be initialized:** Must be assigned a value at declaration
- **Cannot be reassigned:** Value cannot be changed (but object/array contents can be mutated)
- **Hoisted but not initialized:** Exists in "temporal dead zone" until declaration

## Variable Scope
- **Global Scope:** Outermost level (accessible everywhere)
- **Local Scope**: Inner functions can access variables from their parent functions.
- **Function Scope:** Variables are confined to the function they are declared in.
- **Block Scope:** Variables declared with let or const are confined to the nearest block (loops, conditionals, etc.)

## Truthy vs falsy values
- **Falsy:** false, 0, "" (empty string), null, undefined, NaN
- **Truthy:** Everything else (e.g., any non empty string, any non-zero number, objects, arrays).

## Null vs undefined
A null value is something that we intentionally set as empty/doesn't exist. In contrast to undefined which means doesn't exist, but we haven't explicitly
set it to empty, for example accessing a variable that doesn't exist. It means "value not assigned yet".

## `this` keyword
The *this* keyword in JS is a special keyword that refers to the object that is currently executing the code. It varies depending on where you use it.

1. Regular functions
- They create their own this based on how they are called.
- When you call them:
    - As an object method → this = that object.
    - As a plain function → this = global object (or undefined in strict mode).
    - As a constructor (new) → this = the new instance.

2. Arrow functions
- They do NOT create their own this.
- Instead, they lexically inherit this from the scope in which they were defined.
- The this inside an arrow function is locked in when the function is created.

## `bind`, `call`, `apply` methods
They manually let you set what `this` will be when a function runs.
Sometimes, this doesn’t point to what you expect — so you can force it.

```typescript
const boundGreet = user.greet.bind(user);
```

## Hoisting
This basically means that the variables and function declarations are moved to the top of their scope (in the compilation phase, before the code runs).

1. Function declarations are hoisted completely, meaning you can call them before they are defined.
2. `var` declarations are hoisted and initialized with undefined. Accessing this before the declaration gives you undefined.
3. `let` and `const` declarations are hoisted but not initialized. Accessing them before declarations causes an error.

## == vs ===
== is the loose equality operator, which compares two values for equality after converting the type to the same.
=== is the strict equality operator which compares both the values and their types.

## References in JS
- Primitive values are stored directly in memory.
- Objects (arrays, functions, plain objects) are stored by reference - meaning the variable holds a pointer to where the object lives in memory.

```javascript
let obj1 = { name: "Alice" };
let obj2 = obj1; // obj2 now points to the same memory

obj2.name = "Bob";
console.log(obj1.name); // "Bob" → same object in memory
```

Both variables point to the same object. Changing one changes the other.

## Shallow vs deep copy
### Shallow
A shallow copy creates a new object, but:

It copies references for any nested objects/arrays, not the actual nested data.

Example:

```javascript
let original = { name: "Alice", address: { city: "NY" } };

let shallow = { ...original }; // or Object.assign({}, original)

shallow.name = "Bob";          // only changes shallow
shallow.address.city = "LA";   // changes BOTH!

console.log(original.address.city); // "LA" → still linked
```

Why? Because `address` is an object — only the reference was copied.

### Deep Copy
A deep copy makes a completely independent clone, including all nested objects.
Changing the copy does not affect the original at any level.

Example:

```javascript
let original = { name: "Alice", address: { city: "NY" } };

let deep = structuredClone(original); // or JSON method for simple objects

deep.address.city = "LA";

console.log(original.address.city); // "NY" → completely separate
```

# 📘 JavaScript Variable Declarations

JavaScript provides three primary ways to declare variables: `var`, `let`, and `const`. Each has its own behavior with regard to **scope**, **hoisting**, **reassignment**, and **redeclaration**.

## 🔍 Comparison Table

| Keyword | Scope    | Hoisted           | Reassignment | Redeclaration |
|---------|----------|-------------------|--------------|----------------|
| `var`   | Function | ✅ Yes             | ✅ Yes       | ✅ Yes         |
| `let`   | Block    | ✅ Yes (undefined) | ✅ Yes       | ❌ No          |
| `const` | Block    | ✅ Yes (undefined) | ❌ No        | ❌ No          |

---


## 📖 Explanation

### `var`
- **Scope**: Function-scoped.
- **Hoisting**: Hoisted to the top of its function, initialized with `undefined`.
- **Reassignment**: Allowed.
- **Redeclaration**: Allowed in the same scope.

### `let`
- **Scope**: Block-scoped (limited to `{}`).
- **Hoisting**: Hoisted but not initialized. Accessing before declaration causes a *ReferenceError* (Temporal Dead Zone).
- **Reassignment**: Allowed.
- **Redeclaration**: Not allowed in the same scope.

### `const`
- **Scope**: Block-scoped.
- **Hoisting**: Hoisted but not initialized (same TDZ behavior as `let`).
- **Reassignment**: Not allowed — must be assigned at declaration.
- **Redeclaration**: Not allowed in the same scope.

---

## ✅ Best Practices
- Use `let` when the variable's value needs to change.
- Use `const` by default to enforce immutability unless reassignment is necessary.
- Avoid using `var` in modern JavaScript — it's error-prone due to its function scope and redeclaration behavior.

# 📚 JavaScript Data Types

JavaScript data types fall into two main categories: **Primitive Types** and **Reference Types**.

---

## 🧮 Primitive Types

These are immutable and hold a single value.

- **String** → `"hello"`
- **Number** → `42`
- **Boolean** → `true`, `false`
- **Undefined** → A variable declared but not assigned a value.
- **Null** → Represents intentional absence of any value.
- **Symbol** → A unique and immutable identifier (often used as object property keys).
- **BigInt** → Used for very large integers (`9007199254740991n` and beyond).

---

## 🧱 Reference Types

These types are more complex and can hold multiple values or functionalities.

- **Object** – Key-value pairs.
- **Array** – Ordered list of values.
- **Function** – Block of reusable code.
- **Other built-ins** – Such as `Date`, `RegExp`, etc.

---

## ✅ Example

```js
let name = "Abubakar";       // string
let age = 30;                // number
let isOnline = true;         // boolean
let nothing = null;          // null
let notAssigned;             // undefined
let big = 9007199254740991n; // bigint

```
## 3. 🧪 Type Checking in JavaScript

JavaScript provides built-in operators to check the type of a value. The two most common are `typeof` and `instanceof`.

---

### ✅ `typeof` Operator

Used for checking the **primitive type** of a value.

```js
console.log(typeof "Hi");        // string
console.log(typeof null);        // object (JS quirk!)
console.log(typeof undefined);   // undefined
```

## 4. 🔄 Type Conversion vs Coercion

JavaScript handles data types in two ways: **conversion** (explicit) and **coercion** (implicit). Understanding the difference helps avoid unexpected behavior in your code.

---

### 🔧 Type Conversion (Manual)

You *explicitly* convert one data type to another using built-in functions like `String()`, `Number()`, and `Boolean()`.
✅ Use this when you want full control over how data types are changed.

```js
String(123);     // "123"
Number("456");   // 456
Boolean(0);      // false
```
### 🔁 Type Coercion (Automatic)

JavaScript *implicitly* converts values during operations when it expects a certain type.

```js
console.log("5" + 2); // "52" → number 2 is coerced into a string
console.log("5" - 2); // 3   → string "5" is coerced into a number
```

## 📌 5. Template Literals

Template literals in JavaScript provide a cleaner way to work with strings, especially when combining variables or creating multiline text.

---

### 🔄 Instead of String Concatenation

```js
const name = "Abubakar";
console.log("Hello, " + name); // old way
```

### ✅ Use Backticks

```js
console.log(`Hello, ${name}`); // Hello, Abubakar
```
## 1. 🧠 Deep vs Shallow Copy (🔥 Must-Know in Interviews)

Understanding the difference between **shallow** and **deep** copies is crucial when working with **reference types** in JavaScript — and it's a favorite interview topic!

---

### 🧮 Primitive vs Reference Types

- **Primitive types** (e.g., `number`, `string`, `boolean`) are **copied by value**.
- **Reference types** (e.g., `objects`, `arrays`) are **copied by reference**, meaning changes affect the original.

---

### 📋 Shallow Copy

In a shallow copy, both variables refer to the **same object** in memory.
⚠️ Modifying the copy also modifies the original.


```js
const original = { name: 'Abubakar' };
const copy = original;

copy.name = 'Changed';
console.log(original.name); // Changed ❗
```

### 🧬 Deep Copy
A deep copy creates a completely independent copy of the original object.

```js
const original = { name: 'Abubakar' };
const deep = JSON.parse(JSON.stringify(original));

deep.name = 'Changed';
console.log(original.name); // Abubakar ✅
```

## 🧊 Object Mutability and Freezing

In JavaScript, objects are **mutable by default**, meaning their properties can be changed even if the object is declared with `const`.

---

### 🔒 `Object.freeze()`

`Object.freeze()` makes an object **immutable** — you can’t add, remove, or modify its properties.

```js
const obj = { a: 1 };
Object.freeze(obj);

obj.a = 2;
console.log(obj.a); // 1 (doesn't change)
```
⚠️ Frozen objects cannot be changed — any attempt to modify is silently ignored (in non-strict mode) or throws an error (in strict mode).

### 🧷 Object.seal()
Object.seal() prevents adding or removing properties, but allows modifying existing values.

```js
const sealed = { a: 1 };
Object.seal(sealed);

sealed.a = 2;       // ✅ allowed
sealed.b = 3;       // ❌ not added
delete sealed.a;    // ❌ not deleted

console.log(sealed); // { a: 2 }
```
🧠 Use seal() when you want to lock down the object structure, but still allow updates to existing properties.

## ⚖️ Falsy vs Truthy Gotchas

JavaScript has the concept of **truthy** and **falsy** values, which can lead to unexpected behavior in conditional statements if you're not careful.

---

### ❌ Falsy Values

The following values are considered **falsy** (they evaluate to `false` in boolean contexts):

- `false`
- `0`
- `''` (empty string)
- `null`
- `undefined`
- `NaN`

```js
const values = [false, 0, '', null, undefined, NaN];
values.forEach(v => console.log(Boolean(v))); // All false
```

## 🔐 Symbols (for Private-like Properties)

`Symbol` is a primitive data type in JavaScript used to create **unique and hidden** property keys, often used to simulate private properties in objects.

---

### 🛠️ Creating and Using a Symbol

```js
const sym1 = Symbol('id');
const obj = {
  [sym1]: 123
};

console.log(obj[sym1]); // 123
```

### ⚠️ Symbol Properties Are Hidden
🧠 Symbols are not enumerable:

* They do not appear in for...in loops

* They do not appear in Object.keys(), Object.values(), or JSON.stringify()

This makes them useful for adding internal or "private-like" properties to objects that shouldn't be accessed accidentally or exposed unintentionally.

```js
for (let key in obj) {
  console.log(key); // No output
}

console.log(Object.keys(obj)); // []
```
## 🧩 Destructuring (Objects & Arrays)

Destructuring is a concise way to **unpack values** from arrays or **extract properties** from objects into variables. It improves readability and reduces repetitive code.

---

### 🔹 Object Destructuring

```js
const user = { name: 'Abubakar', age: 28 };
const { name, age } = user;

console.log(name); // Abubakar
console.log(age);  // 28
```

### 🔹 Array Destructuring

```js
const [a, b, ...rest] = [1, 2, 3, 4];

console.log(a);    // 1
console.log(b);    // 2
console.log(rest); // [3, 4]
```

### 🔹 Nested Destructuring

```js
const user = {
  name: 'Ali',
  location: {
    city: 'Lahore'
  }
};

const { location: { city } } = user;

console.log(city); // Lahore
```
🧠 Destructuring is especially useful when working with APIs, props in React, and large objects or arrays.

## 🌪️ Rest vs Spread Operators

JavaScript’s `...` syntax can be used as both a **rest operator** (for gathering values) and a **spread operator** (for spreading values).

---

### 🔹 Rest Operator (`...`)

Used to **collect** the remaining properties or elements into a new object or array.

```js
const obj = { a: 1, b: 2, c: 3 };
const { a, ...rest } = obj;

console.log(rest); // { b: 2, c: 3 }
```

🧠 In objects and function parameters, the rest operator is used to gather remaining data.

### 🔹 Spread Operator (...)

Used to expand an object or array into individual elements or properties.

```js
const arr = [1, 2, 3];
const newArr = [...arr, 4];

console.log(newArr); // [1, 2, 3, 4]
```
✅ Spread is commonly used for cloning and merging arrays or objects.

```js
const obj1 = { x: 1 };
const obj2 = { y: 2 };
const combined = { ...obj1, ...obj2 }; // { x: 1, y: 2 }
```

🔄 The same ... syntax, but different use depending on context — rest collects, spread expands.


## 🔗 Optional Chaining (`?.`) + Nullish Coalescing (`??`)

These two modern JavaScript features help you safely access deeply nested properties and provide smart fallbacks without unexpected behavior.

---

### ✅ Optional Chaining (`?.`)

Allows you to safely access nested object properties **without throwing an error** if a property doesn’t exist.

```js
const user = { profile: { name: 'Abubakar' } };

console.log(user?.profile?.name);     // Abubakar
console.log(user?.settings?.theme);   // undefined (no error)
```
🛡️ Prevents "Cannot read property 'x' of undefined" errors.

### ⚡ Fallback: || vs ??

🔸 Using Logical OR (||)

```js
console.log(user?.settings?.theme || 'light'); // "light"
```

⚠️ Falls back even if the value is "", 0, or false (because they are falsy).

✅ Using Nullish Coalescing (??)
```js
console.log(user?.settings?.theme ?? 'light'); // ✅ "light"
```
✅ Falls back only if the value is null or undefined — safer when you expect 0, "", or false to be valid values.

🧠 Tip
Use ?? instead of || when you only want to fall back on truly missing values (null or undefined) — not falsy ones.

## 🧪 Custom Type Checking Utility (🔥 Interview Use Case)

In JavaScript, sometimes you need more precise type checks than `typeof` can offer — especially when distinguishing between objects and arrays.

---

### ✅ `isObject()` Utility Function

This function checks if a value is a **plain object** (not `null` and not an array).

```js
function isObject(obj) {
  return obj !== null && typeof obj === 'object' && !Array.isArray(obj);
}
```
🧠 Why This Is Useful
- typeof null returns "object" — which is misleading.

- Array.isArray([]) returns true, but you may want to exclude arrays.

- Great for validating configs, payloads, and guarding logic.

```js
isObject({});        // true
isObject([]);        // false
isObject(null);      // false
isObject('string');  // false
```

## ⚙️ Control Flow Mastery & Shortcuts (Advanced Logic & Patterns)

Mastering control flow patterns in JavaScript leads to cleaner, more readable, and more maintainable code. Here's a breakdown of advanced logic patterns every serious JS dev should know.

---

### 1. 🔁 Short-Circuiting with `&&`, `||`, and `??`

```js
const user = null;

const name = user && user.name;           // null
const fallback = user || 'Guest';         // 'Guest'
const strictFallback = user ?? 'Guest';   // 'Guest'
```

🧠 Use ?? instead of || when values like '', 0, or false should be considered valid and not trigger fallback.

### 2. ❓ Ternary Operators (with nesting pattern)
```js
const score = 75;
const grade = score >= 90 ? 'A' : score >= 70 ? 'B' : 'C';
```

🧠 Avoid deeply nested ternaries — switch to if-else or an object map if more than two levels deep.

### 3. 🧭 Switch vs Object Mapping

📦 Old-School switch:
```js

switch (role) {
  case 'admin': return 'Full access';
  case 'user': return 'Limited access';
}
```

🚀 Modern Object Mapping:
```js
const permissions = {
  admin: 'Full access',
  user: 'Limited access',
};

const role = 'admin';
const message = permissions[role] ?? 'No access';
```
🧠 Object maps are cleaner, more scalable, and easier to maintain.

### 4. 🔁 Early Returns Instead of Big if-else Blocks

```js
function process(user) {
  if (!user) return 'No user found';
  if (user.isBanned) return 'User banned';

  return 'Welcome!';
}
```

✅ Early returns flatten logic and make code easier to follow.


### 5. ⚡ Immediately Invoked Function Expressions (IIFE)

```js
(function () {
  console.log('I run immediately!');
})();
```
🔐 Useful for isolated scopes, especially in legacy code or modules.


### 6. 🎯 Labelled Loops (Rare but Pro Use)
```js
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === j) continue outer;
    console.log(i, j);
  }
}
```
⚠️ Rarely used, but handy for breaking or continuing outer loops in complex nested logic.

### 7. 🔁 Generators & Iterators (for custom data flow)
```js
function* counter() {
  yield 1;
  yield 2;
  yield 3;
}

const it = counter();
console.log(it.next()); // { value: 1, done: false }
```
### 8. 🛠️ Custom forEach, map, reduce Patterns

🔄 Use .reduce() to Flatten an Array

```js
const nested = [[1], [2], [3]];
const flat = nested.reduce((acc, curr) => acc.concat(curr), []);
```
📊 Grouping Items by Key
```js
const items = [{type: 'fruit'}, {type: 'veg'}, {type: 'fruit'}];

const grouped = items.reduce((acc, item) => {
  acc[item.type] = (acc[item.type] || 0) + 1;
  return acc;
}, {});
```

🧠 Custom reducers unlock powerful data manipulation patterns — use them for flattening, grouping, counting, and more.

## 🏹 Arrow Functions vs Regular Functions

Arrow functions in JavaScript offer a more concise syntax, but they behave differently than regular functions — especially in terms of `this` binding and usage in different contexts.

---

### 🔍 Feature Comparison

| Feature              | Regular Function               | Arrow Function                     |
|----------------------|--------------------------------|-------------------------------------|
| `this` binding       | Dynamic (based on caller)      | Lexical (inherits from outer scope) |
| Constructor usage    | ✅ Yes                          | ❌ No                                |
| `arguments` object   | ✅ Available                    | ❌ Not available                     |

---

### 🧪 Examples

#### 🔁 Regular Function

```js
function regular() {
  console.log(this); // depends on how it's called
}
```

### 🏹 Arrow Function

```js
const arrow = () => {
  console.log(this); // same as outer (lexical) scope
}
```

🧠 Key Difference: Arrow functions do not bind their own this. They're ideal for callbacks or methods where you want to preserve the surrounding context.

⚠️ When to Use Which?
- Use regular functions when:

  + You need dynamic this
  + You’re writing constructors

  + You need the arguments object

- Use arrow functions when:

  + You want concise syntax

  + You don’t want this to be rebound

  + You’re working inside methods or callbacks

## 🔗 Function Binding: `call`, `apply`, `bind`

JavaScript functions have special methods — `call()`, `apply()`, and `bind()` — that allow you to control the value of `this` when the function is executed.

---

### 📌 Example Function

```js
function greet(msg) {
  return `${msg}, ${this.name}`;
}

const user = { name: 'Abubakar' };
```

---
✅ call()
Calls the function immediately with a given this and arguments passed individually.
```js
greet.call(user, 'Hi'); // 'Hi, Abubakar'
```

---
✅ apply()
Similar to call(), but arguments are passed as an array.
```js
greet.apply(user, ['Hello']); // 'Hello, Abubakar'
```
---
✅ bind()
Returns a new function with this permanently set — useful for callbacks, event handlers, etc.
```js
const bound = greet.bind(user);
bound('Welcome'); // 'Welcome, Abubakar'
```
🧠 Pro Tip
+ Use call() and apply() for immediate invocation.

+ Use bind() when you need to defer execution or preserve context for later (e.g., in event handlers or asynchronous logic).

```js
const button = document.querySelector('button');
button.addEventListener('click', greet.bind(user, 'Hey'));
```

## 🔒 Closures (Interview Favorite)

A **closure** is created when a function remembers its **lexical scope**, even when executed outside of that scope. It's one of the most powerful and commonly asked JavaScript concepts in interviews.

---

### ✅ Example: Counter with Closure

```js
function makeCounter() {
  let count = 0;
  return function () {
    return ++count;
  };
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```
🔁 The inner function remembers the count variable from the outer function, even after makeCounter() has finished executing.

🧠 Why It Matters
Closures allow:

- Data encapsulation (private variables)
- Function factories
- Maintaining state in async callbacks (e.g., in loops or timers)

```js
function secretHolder(secret) {
  return function () {
    return secret;
  };
}

const getSecret = secretHolder('🕵️ Hidden');
console.log(getSecret()); // 🕵️ Hidden
```

📌 Closures = Function + its preserved scope

---

## 🔗 Currying (Function Chaining)

**Currying** is a functional programming technique where a function is transformed into a series of functions, each taking a single argument.

---

### ✅ Example: Curried `add` Function

```js
function add(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}

console.log(add(1)(2)(3)); // 6
```

🔁 Each function returns another function until all arguments are provided.

🧠 Why Use Currying?
- Creates flexible and reusable APIs
- Encourages function composition
- Useful in frameworks like React, Redux, and Lodash

⚙️ Real-World Use Case
```js
const multiply = a => b => a * b;

const double = multiply(2);
console.log(double(5)); // 10
```
📌 Currying is all about breaking down a function that takes multiple arguments into a series of unary functions (one argument each).

## ⚡ Memoization (Caching Results)

**Memoization** is an optimization technique used to **cache function results** so expensive computations don’t run multiple times for the same inputs.

---

### ✅ Custom `memoize` Function

```js
function memoize(fn) {
  const cache = {};
  return function (...args) {
    const key = JSON.stringify(args);
    if (key in cache) return cache[key];
    cache[key] = fn(...args);
    return cache[key];
  };
}
```
---
### Example

🧪 Usage Example

```js
const slowSquare = memoize(n => {
  console.log('Calculating...');
  return n * n;
});

console.log(slowSquare(5)); // Calculating... 25
console.log(slowSquare(5)); // Cached: 25
```
🧠 The second call doesn't trigger computation — it retrieves the result from cache.

⚙️ When to Use
- Expensive calculations (e.g. factorial, Fibonacci)
- Recursive algorithms
- Heavy API calls with the same parameters

🔁 Common in Libraries
Memoization is widely used in:

- React (useMemo) for caching component values
- Lodash.memoize
- Redux selectors (reselect)

📌 Key Benefit: Memoization saves time at the cost of memory — perfect for performance-critical logic.

## 🧩 Function Decorators (Add Behavior)

**Function decorators** wrap a function to add behavior like logging, validation, timing, etc., without changing the original function.

---

### ✅ Example: Logging Decorator

```js
function logWrapper(fn) {
  return function (...args) {
    console.log('Calling with', args);
    return fn(...args);
  };
}

function sum(a, b) {
  return a + b;
}

const wrappedSum = logWrapper(sum);
console.log(wrappedSum(2, 3)); // Logs: Calling with [2, 3], then returns 5
```
🧠 The original sum function remains untouched — behavior is added via composition.

🎯 Why Use Decorators?
- Separation of concerns — logic is modular and reusable
- Cleaner logging, profiling, or validation
- Enhances functionality without altering core logic
---
- 🔧 More Use Cases
- ✅ Authentication wrappers
- ⏱ Performance timing
- ⚠ Error handling or retry logic
- 🔒 Access control

### 📌 Bonus Tip
JavaScript decorators (@decorator) are a stage-3 proposal in ECMAScript and already supported in many tools (e.g. Babel, TypeScript).

```js
@log
function process(data) { ... }
```
## 🧠 Functions as First-Class Citizens

In JavaScript, **functions are first-class objects**, meaning you can:

- Assign them to variables
- Pass them as arguments
- Return them from other functions
- Store them in data structures

---

### ✅ Example: Storing & Executing Functions

```js
const operations = {
  add: (a, b) => a + b,
  sub: (a, b) => a - b,
};

function execute(op, a, b) {
  return operations[op](a, b);
}

console.log(execute('add', 5, 3)); // 8
console.log(execute('sub', 5, 3)); // 2
```

🔁 operations is an object where functions are values — just like numbers or strings.

💡 Why It Matters
- Enables higher-order functions
- Forms the basis of patterns like callbacks, event listeners, and functional composition
- Essential for building flexible APIs, utilities, and libraries

📌 Real-World Examples
- Array.prototype.map, filter, reduce
- setTimeout(() => ...)
- Promise.then(callback)

```js
const sayHello = () => console.log("Hello!");
const runLater = cb => setTimeout(cb, 1000);
runLater(sayHello); // Runs after 1 second
```

## 🔍 `this` Keyword Mastery

The `this` keyword refers to the **context** in which a function is executed. Understanding how it behaves in different scenarios is critical for mastering JavaScript.

---

### ✅ Basic Example

```js
const user = {
  name: 'Abu',
  greet() {
    console.log(this.name);
  },
};

user.greet(); // ✅ Abu
```
Here, this refers to the user object because the method was called on it.

❌ Lost Context
```js
const greetFn = user.greet;
greetFn(); // ❌ undefined (in strict mode), or global object in non-strict
```
🔥 Common mistake: assigning methods to variables without binding loses the original context.

✅ Fix with bind()
```js
const bound = user.greet.bind(user);
bound(); // ✅ Abu
```
Use .bind() to permanently bind this to the correct object.

🧠 Why This Matters
- Crucial for working with event handlers, setTimeout, callbacks, and classes
- Prevents bugs caused by this being undefined or referring to the wrong context

---
⚙️ Example in Event Handlers
```js
class Button {
  constructor() {
    this.label = 'Click me';
    document.querySelector('button').addEventListener('click', this.handleClick.bind(this));
  }

  handleClick() {
    console.log(this.label); // ✅ 'Click me'
  }
}
```
📌 Always be cautious with this in class methods, especially when used as callbacks.

🛠 Alternatives to bind()
- Arrow functions (lexical this)
- Class fields (e.g., handleClick = () => {} in React)

## 🏗️ Object Creation Patterns in JavaScript

JavaScript provides several powerful ways to create objects. Each pattern has its use case depending on structure, reusability, and inheritance needs.

---

### ✅ 1. Object Literal

Quick and simple way to define objects.

```js
const user = {
  name: 'Abubakar',
  greet() {
    console.log(`Hi, I'm ${this.name}`);
  },
};

user.greet(); // Hi, I'm Abubakar
```
🧠 Best for static, one-off objects.


### ✅ 2. Factory Function
A function that returns a new object — great for creating multiple instances without using new.
```js
function createUser(name) {
  return {
    name,
    greet() {
      console.log(`Hello from ${name}`);
    },
  };
}

const u1 = createUser('Ali');
u1.greet(); // Hello from Ali
```
🔁 Useful for encapsulating logic and avoiding new.

### ✅ 3. Constructor Function
Used with new to create object instances and leverage prototypes for shared methods.
```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  console.log(`Hey, ${this.name}`);
};

const u = new User('Abu');
u.greet(); // Hey, Abu
```
⚠️ Don’t forget the new keyword — omitting it causes bugs!

### ✅ 4. Object.create() for Prototype Inheritance
Allows manual setup of an object with a specific prototype.

```js
const proto = {
  greet() {
    console.log(`Hi, I'm ${this.name}`);
  },
};

const user = Object.create(proto);
user.name = 'Abubakar';
user.greet(); // Hi, I'm Abubakar
```
🔧 Gives precise control over the prototype chain — powerful for inheritance-heavy designs.


## 🔐 Property Descriptors & Immutability

JavaScript allows fine-grained control over object properties using **property descriptors**. You can define how a property behaves — whether it's writable, enumerable, or configurable.

---

### ✅ Example: Making a Property Immutable

```js
const user = {};

Object.defineProperty(user, 'id', {
  value: 123,
  writable: false, // 🔒 Can't be changed
});

user.id = 456;
console.log(user.id); // still 123
```
🧠 Setting writable: false makes the property read-only — even if reassigned, the value stays unchanged.


🧰 Other Property Descriptor Flags

|Flag        | Default  | Description |
|------------|----------|-------------|
|writable	 | false	| If true, the value can be changed|
|enumerable	 | false	| If true, the property appears in loops|
|configurable| false	| If true, the descriptor can be changed or deleted|

🧪 Inspecting Descriptors
```js
const desc = Object.getOwnPropertyDescriptor(user, 'id');
console.log(desc);
/*
{
  value: 123,
  writable: false,
  enumerable: false,
  configurable: false
}
*/
```

🚫 Enforcing Immutability
- Object.freeze(obj) → Deep freeze all properties
- Object.seal(obj) → Prevent addition/removal of properties
- Object.defineProperty() → Set property-level control

📌 Use Cases
- Locking IDs or constants in config objects
- Protecting internal logic in libraries
- Creating secure API layers

```js
Object.freeze(user); // All properties become read-only and non-configurable
```
🔒 Use property descriptors when you need control and security over how data behaves.

## 💰 Getters & Setters

**Getters** and **Setters** allow you to control how object properties are accessed and mutated — enabling **encapsulation** and **validation** logic.

---

### ✅ Example: Account Balance with Validation

```js
const account = {
  _balance: 0,

  get balance() {
    return this._balance;
  },

  set balance(value) {
    if (value >= 0) this._balance = value;
  },
};

account.balance = 100;
console.log(account.balance); // 100
```
🧠 The actual property _balance is private-like, while balance provides a controlled interface.

🛠 Benefits of Getters & Setters
- Add validation logic
- Trigger side effects (e.g., logging, syncing)
- Create computed properties
- Hide internal state (conventionally using _)

📌 Best Practices
- Use getters/setters for controlled access to internal data
- Prefix internal fields (e.g., _value) to signal private usage
- Avoid heavy computations inside getters to keep performance predictable

### 🧪 Example: Computed Property
```js
const rectangle = {
  width: 10,
  height: 5,

  get area() {
    return this.width * this.height;
  }
};

console.log(rectangle.area); // 50
```
🔍 Getters can act like computed properties without needing explicit method calls.

⚠️ Remember
- Getters must return a value
- Setters must take exactly one argument
- You can define them with Object.defineProperty() too

```js
Object.defineProperty(account, 'info', {
  get() {
    return `Balance: ${this._balance}`;
  }
});
```
🔒 Getters and setters are key tools for building robust, maintainable objects.

## 🔒 Private Fields (ES2022)

**Private class fields** (introduced in ES2022) allow truly private properties using the `#` prefix — inaccessible from outside the class, even via reflection.

---

### ✅ Example: Encapsulating Balance in a Bank Class

```js
class Bank {
  #balance = 0;

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}

const b = new Bank();
b.deposit(100);
console.log(b.getBalance()); // 100
```
🚫 b.#balance is not accessible from outside the class — trying will throw a syntax error.

🧠 Why Use Private Fields?
- True encapsulation (unlike _ prefix which is just a convention)
- Prevents external tampering
- Cleaner and more secure codebase
- Encouraged in modern JS class design

🔐 Key Points
- Always prefixed with #
- Must be declared before usage in the class body
- Not accessible via this['#field'], Object.keys, or JSON.stringify

```js
class Demo {
  #hidden = 42;
}

const d = new Demo();
console.log(d.#hidden); // ❌ SyntaxError: Private field '#hidden' must be declared in an enclosing class
```
📌 Use private fields when you need secure internal state and want to fully encapsulate logic.


### 🌟 Bonus Tip: Combine with Getters/Setters
```js
class Wallet {
  #amount = 0;

  get value() {
    return this.#amount;
  }

  set value(val) {
    if (val >= 0) this.#amount = val;
  }
}
```
🔐 Great for protecting sensitive data like balance, tokens, or internal config.

## 🔄 Dynamic Properties

JavaScript allows you to **dynamically assign property keys** using square brackets `[]` in object literals. This is especially useful when the key is determined at runtime.

---

### ✅ Example: Creating a Dynamic Key

```js
const key = 'name';
const user = {
  [key]: 'Abu',
};

console.log(user.name); // Abu
```
🧠 The property key is computed from the value of key, not hardcoded as 'key'.

💡 Use Cases
- Building objects based on form input or user selection
- Creating configuration objects from variables
- Mapping dynamic field names to values

### 🧪 More Examples
```js
const prefix = 'user_';
const id = 101;

const dynamicObj = {
  [prefix + id]: 'Abubakar',
};

console.log(dynamicObj.user_101); // Abubakar
```
### ⚙️ Computed Property Names in Functions

```js
function createObj(prop, value) {
  return {
    [prop]: value,
  };
}

const obj = createObj('role', 'admin');
console.log(obj.role); // admin
```

📌 Very handy in factory functions, dynamic state updates, and framework internals.

🛠 Bonus: Used in State Management (e.g., React)
```js
const field = 'email';
const formData = {
  [field]: 'abu@example.com',
};
```

🔄 Dynamic properties are a must-know for building flexible and scalable JavaScript objects.

## 🏷️ Class Syntax (ES6)

JavaScript introduced `class` syntax in ES6 to provide a more familiar, cleaner way to create constructor functions and manage inheritance — while still using prototypes under the hood.

---

### ✅ Basic Example: `User` Class

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hi, I'm ${this.name}`);
  }
}

const u = new User('Abubakar');
u.greet(); // Hi, I'm Abubakar
```

🧠 The constructor() is automatically called when a new instance is created with new.

| Feature | Description |
|---------|-----------------------|
| constructor() | Special method to initialize object properties |
| Instance methods | Defined directly in the class body|
| Inheritance | Supported via extends|
| Super calls | Use super() to access parent class methods/constructor|

🧬 Inheritance Example

```js
class Admin extends User {
  constructor(name, role) {
    super(name);
    this.role = role;
  }

  greet() {
    console.log(`Hi, I'm ${this.name} and I'm an ${this.role}`);
  }
}

const admin = new Admin('Ali', 'Admin');
admin.greet(); // Hi, I'm Ali and I'm an Admin
```

🔗 Use extends to inherit and super() to call the parent constructor or method.

⚠️ Notes
- Classes are syntactic sugar over the prototypal inheritance system.
- Class methods are non-enumerable by default.
- Always use new with classes — calling without new throws an error.

💡 Bonus: Class Fields & Private Fields

```js
class Example {
  count = 0;         // Public field
  #secret = 'shh';   // Private field (ES2022)

  show() {
    console.log(this.count, this.#secret);
  }
}
```
🎯 Classes are now more powerful than ever with support for public/private fields and native encapsulation.

## 🧬 Inheritance with `extends` (ES6 Classes)

JavaScript classes support **inheritance** using the `extends` keyword. This allows one class to inherit properties and methods from another, creating a clean and reusable structure for your code.

---

### ✅ Example: Extending a Base Class

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hi, I'm ${this.name}`);
  }
}

class Admin extends User {
  constructor(name, role) {
    super(name); // Call the parent constructor
    this.role = role;
  }

  accessPanel() {
    console.log(`${this.name} has admin access.`);
  }
}

const admin = new Admin('Abu', 'superadmin');
admin.greet();       // Inherited method: Hi, I'm Abu
admin.accessPanel(); // Admin method: Abu has admin access.
```

| Concept | Explanation |
|---------|-------------|
| extends | Used to inherit from another class |
| super() | Calls the constructor of the parent class |
| Method Overriding | You can redefine parent methods in child class |

🔁 Method Overriding Example

```js
class Admin extends User {
  greet() {
    console.log(`Admin ${this.name} says hello!`);
  }
}
```

🔄 Overrides the base greet() method while retaining access to super.greet() if needed.


⚠️ Rules to Remember
- You must call super() in a subclass constructor before accessing this.
- Inherited methods come from the prototype of the parent class.
- Subclasses can add or override any behavior.

🌟 Use Cases
- Create hierarchies (User → Admin, Customer → PremiumCustomer)
- DRY (Don't Repeat Yourself): Share logic across types
- Build scalable, maintainable object structures

🔧 Inheritance is essential for OOP patterns like polymorphism and code reuse.

## 🧩 `super` Keyword (ES6 Inheritance)

The `super` keyword is used to access and call functions on an object's **parent class**. It plays a critical role in **class inheritance** when using the `extends` keyword.

---

### 🔧 What `super` Does

- `super()` → Calls the **parent class constructor**
- `super.method()` → Calls a **method from the parent class**

---

### ✅ Example: Calling Parent Methods

```js
class Parent {
  sayHi() {
    console.log('Hi from parent');
  }
}

class Child extends Parent {
  sayHi() {
    super.sayHi();           // Call parent method
    console.log('Hi from child');
  }
}

const c = new Child();
c.sayHi();
// Output:
// Hi from parent
// Hi from child
```

🧠 super.sayHi() ensures that the parent’s behavior is preserved or extended — useful for logging, validations, chaining, etc.

🔗 Using super() in Constructors

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

class Employee extends Person {
  constructor(name, role) {
    super(name); // Calls Person's constructor
    this.role = role;
  }
}
```

⚠️ In a subclass constructor, super() must be called before this is used.

🛠️ Why Use super?
- To reuse parent logic
- To extend or override behavior without fully replacing it
- To keep your code DRY (Don't Repeat Yourself)

📌 Best Practices
- Always call super() in subclass constructors.
- Use super.method() when you need to enhance base behavior, not override it completely.
- Avoid deep inheritance chains — prefer composition over inheritance when appropriate.

```js
class Logger {
  log(msg) {
    console.log('[LOG]', msg);
  }
}

class AdvancedLogger extends Logger {
  log(msg) {
    super.log(msg); // Call parent
    console.log('[TIMESTAMP]', new Date().toISOString());
  }
}
```
🔍 super is the bridge between child and parent class logic — use it to enhance, not just replace.

## 🧠 Prototype Chain (Behind the Scenes)

In JavaScript, **every object** has a hidden internal property called `[[Prototype]]`, accessible via `. __proto__` (or `Object.getPrototypeOf()`).

This is the foundation of **prototypal inheritance**.

---

### ✅ Example: Function Constructor with Prototype

```js
function Car(name) {
  this.name = name;
}

Car.prototype.drive = function () {
  console.log(`${this.name} is driving`);
};

const c = new Car('Tesla');
c.drive(); // Tesla is driving
```
🔁 The drive() method is not on the object itself, but on its prototype — shared across all instances.

| Concept | Description |
|---------|-------------|
| __proto__ | Links to an object's prototype |
| Car.prototype | Object used as the prototype for instances created via new Car() |
| Shared Methods | Defined on .prototype so they're not duplicated in memory |
| Lookup Chain | If a property is not found on the object, JS looks up the prototype chain |

🧬 The Prototype Chain in Action

```js
console.log(c.__proto__ === Car.prototype); // true
console.log(Car.prototype.__proto__ === Object.prototype); // true
```
🔗 This forms a prototype chain: c → Car.prototype → Object.prototype → null

⚠️ Prototype vs __proto__
- Car.prototype: Used when creating new instances
- c.__proto__: Points to the prototype of an instance (i.e., Car.prototype)

🚀 ES6 Classes = Prototype Under the Hood
```js
class Car {
  drive() {
    console.log('Driving...');
  }
}

const c = new Car();
```
🎭 Classes in JavaScript are just syntactic sugar over prototype-based constructors.

🧪 Custom Prototypes
```js
const animal = {
  eats: true
};

const rabbit = Object.create(animal);
rabbit.hops = true;

console.log(rabbit.eats); // true (inherited)
```

🔍 Object.create() lets you manually set a prototype — very useful in custom inheritance patterns.


🧠 Summary
- All JS objects are linked through prototype chains
- Methods are shared via .prototype
- Understanding this is key to mastering JS inheritance

## 🧷 Static Methods and Properties (ES6 Classes)

**Static methods and properties** are defined on the class itself, not on instances of the class. They're typically used for utility or helper functions that don't require access to instance data.

---

### ✅ Example: Static Method

```js
class MathUtil {
  static add(a, b) {
    return a + b;
  }
}

console.log(MathUtil.add(2, 3)); // 5
```
🧠 You call static methods on the class, not on an object created from the class.

|Feature | Description|
|--------|------------|
|static keyword | Defines a static method or property|
|No this context | Can't access instance variables or methods|
|Class-level scope | Used directly on the class (e.g. ClassName.method())|

⚠️ Not Accessible on Instances
```js
const math = new MathUtil();
math.add(1, 2); // ❌ TypeError: math.add is not a function
```
🔒 Static methods are not copied to instances — they stay on the class itself.

🛠️ Static Properties (Class Fields Proposal)
Modern JavaScript supports static properties as well:

```js
class Config {
  static appName = 'MyApp';
}

console.log(Config.appName); // MyApp
```
📦 Use Cases
- Utility functions (e.g. Math, Date, JSON)
- Shared configuration or constants
- Factory methods

🌟 Bonus Tip: Combine with Inheritance

```js
class Animal {
  static isAnimal(obj) {
    return obj instanceof Animal;
  }
}

class Dog extends Animal {}

console.log(Animal.isAnimal(new Dog())); // true
```
🧩 Static methods are also inherited by child classes unless overridden.

🧠 Summary
- Use static for logic that doesn’t rely on instance state
- Great for utilities, factories, and metadata
- Keeps your instance clean and lean

## 🧠 Instance vs Prototype Members

When defining classes in JavaScript, there are **two types of members**:

1. **Instance Members** → Defined in the constructor, unique per object
2. **Prototype Members** → Defined on the prototype, shared by all instances

---

### ✅ Example

```js
class A {
  constructor() {
    this.x = 10; // 👈 Instance variable
  }

  method() {
    return this.x; // 👈 Prototype method
  }
}

const a1 = new A();
const a2 = new A();

console.log(a1.method()); // 10
console.log(a1.method === a2.method); // true ✅ (shared method)
```

📌 Key Differences


|Feature | Instance Member | Prototype Member |
|--------|-----------------|------------------|
|Defined in | constructor() | Class body (outside constructor)|
|Stored in | Each object instance | Class.prototype|
|Memory use | More (duplicated) | Less (shared)|
|Accessed via | this.prop | this.method()|

🧪 Checking Membership

```js
console.log(a1.hasOwnProperty('x'));       // true (instance)
console.log(a1.hasOwnProperty('method'));  // false (prototype)
console.log('method' in a1);               // true (found in prototype)
```

💡 Why It Matters
- Instance members = each instance has its own copy (more memory)
- Prototype members = shared across instances (memory efficient)

🔍 Best Practices
- Use instance members for state or data
- Use prototype members for methods or behaviors

```js
class Button {
  constructor(label) {
    this.label = label; // instance
  }

  click() {
    console.log(`${this.label} clicked`); // prototype
  }
}
```

🧠 Optimize your class design by understanding where each member lives in memory.


## 🧩 Mixins (Multiple Inheritance Workaround)

JavaScript doesn’t support multiple inheritance directly, but you can simulate it using **mixins** — a pattern that allows you to add behavior from multiple objects to a class.

---

### ✅ Example: Combining Behaviors

```js
let Flyer = {
  fly() {
    console.log(`${this.name} can fly`);
  },
};

let Swimmer = {
  swim() {
    console.log(`${this.name} can swim`);
  },
};

function applyMixins(target, ...sources) {
  Object.assign(target.prototype, ...sources);
}

class Hero {
  constructor(name) {
    this.name = name;
  }
}

applyMixins(Hero, Flyer, Swimmer);

const h = new Hero('Superman');
h.fly();  // Superman can fly
h.swim(); // Superman can swim
```

📌 What’s Happening
- Flyer and Swimmer are plain objects with reusable methods.
- applyMixins() copies these methods to the class prototype using Object.assign.
- The class now “inherits” behaviors from multiple sources.

🔧 Mixin Function
```js
function applyMixins(target, ...sources) {
  Object.assign(target.prototype, ...sources);
}
```
🛠 Adds multiple sets of methods to a class without affecting its original hierarchy.

📦 Use Cases
- Adding reusable functionality (e.g. logging, animation, event handling)
- Sharing behavior across unrelated classes
- Avoiding deep or rigid inheritance chains

⚠️ Things to Watch Out For

| Concern | Tip |
| --------|-----|
|Name conflicts | Avoid mixing objects with the same method names|
|No super support | Mixins can't call super like class inheritance does|
|Pure functions | Keep mixin methods stateless when possible for reusability|

🧠 Summary
- Use mixins to compose multiple capabilities into one class.
- Great for modular and reusable code.
- A clean alternative to traditional inheritance, especially in large apps.

```js
// Example utility mixin for logging
const Logger = {
  log(msg) {
    console.log(`[LOG]: ${msg}`);
  }
};
```

🧩 Mixins are a smart, flexible pattern for sharing behavior without overcomplicating your inheritance model.

## 🧠 Lexical Scope (Static Scope)

**Lexical scope** means a function’s scope is determined by its **physical placement in the code** — where it's declared, not where it’s called. It defines how variable names are resolved in nested functions.

---

### ✅ Example: Outer and Inner Functions

```js
function outer() {
  let name = "Abu";

  function inner() {
    console.log(name); // 'Abu'
  }

  inner();
}

outer();
```
🔍 The inner() function can access name from outer() because it is lexically scoped inside it.

📌 Key Concepts
- Functions remember the scope where they were defined, not where they were called.
- This is the foundation for closures in JavaScript.

🧬 Scope Chain

```js
function a() {
  let x = 10;

  function b() {
    let y = 20;

    function c() {
      console.log(x, y); // Has access to both x and y
    }

    c();
  }

  b();
}

a();
```
🧠 Each inner function has access to its own scope, outer scopes, and global scope.

🔒 Why Lexical Scope Matters
- Predictable: You always know what variables a function can access by looking at the code
- Enables closures (functions that "remember" variables from their outer scope)
- Prevents accidental leakage from other scopes

🧠 Summary

| Term | Description |
|------|-------------|
|Lexical Scope | Scope defined by where code is written (not runtime behavior)|
|Inner Function | Can access outer variables thanks to lexical scope|
|Scope Chain | JavaScript looks up variables from inner to outer scopes|

## 🔐 Closure Defined

A **closure** is a function that **remembers variables from its outer scope**, even after that outer function has finished executing.

This allows for data **encapsulation**, **persistence**, and **powerful patterns** like stateful functions.

---

### ✅ Example: Counter Using Closure

```js
function outer() {
  let count = 0;

  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2
```

🔁 Even though outer() is done executing, inner() remembers count.

📌 Key Characteristics

| Feature | Description |
|---------|-------------|
|Scope Persistence | Remembers the lexical environment|
|Private State | Keeps data hidden from the global scope|
|Function Nesting | Commonly used with inner functions|
|Used After Execution | Outer scope stays alive due to references|

🚀 Real-World Use Cases
- ✅ React Hooks (e.g. useState, useEffect)
- ✅ Memoization (caching results)
- ✅ Throttling/Debouncing
- ✅ Encapsulation (hide data from outside access)

🧠 Visualizing the Closure
```js
const sayHello = () => {
  let name = "Abu";

  return () => console.log(`Hello, ${name}`);
};

const greet = sayHello();
greet(); // Hello, Abu
```

📦 name is kept "alive" by the returned function — that's the closure in action!

🔒 Encapsulation Example

```js
function secretHolder() {
  let secret = '🔐';

  return {
    get: () => secret,
    set: val => (secret = val),
  };
}

const s = secretHolder();
console.log(s.get()); // 🔐
s.set('🔓');
console.log(s.get()); // 🔓
```
🔍 No direct access to secret, only controlled through closure methods.

🧠 Summary
- Closures "close over" their outer lexical scope.
- They allow for persistent, private, and powerful logic.
- Mastering closures is essential for advanced JS and frameworks like React.

💡 If you understand closures, you understand JavaScript.

## 🔐 Use Case: Data Privacy with Closures

JavaScript doesn't have built-in private fields in traditional functions, but closures provide a clean and powerful workaround.

You can **hide variables from the outside world** by enclosing them in a function scope and only exposing controlled accessors.

---

### ✅ Example: Private Data via Closure

```js
function secretHolder() {
  let secret = "🍕";

  return {
    getSecret: () => secret,
    setSecret: (s) => (secret = s),
  };
}

const holder = secretHolder();

console.log(holder.getSecret()); // 🍕
holder.setSecret("🍔");
console.log(holder.getSecret()); // 🍔
```

🔐 secret is not accessible directly — only through getSecret() and setSecret().

📦 Why This Works
- secret is inside the closure and cannot be accessed or modified directly from the outside.
- Only the returned object methods have access to it.
- Perfect for encapsulation, privacy, and controlled data access.

📌 Use Cases in the Wild

| Use Case | Description |
|----------|-------------|
|React Hooks | Encapsulate state logic (e.g. useState)|
|API Tokens | Hide sensitive info like tokens |
|Libraries & SDKs | Prevent external tampering
|Business Logic Rules | Keep internal state rules private|

🚫 What You Can’t Do

```js
console.log(holder.secret);     // undefined ❌
console.log(holder._secret);    // undefined ❌
```

🔒 There is no direct way to access secret, making it truly private via closure.

🧠 Summary
- Closures let you create private variables in plain JavaScript.
- You control access through exposed functions.
- This is a core technique in writing secure, modular, and maintainable JS code.

## 🔁 Loops + Closures (Tricky Case)

Using closures inside loops can lead to **unexpected results**, especially when `var` is involved.

Why? Because `var` is function-scoped — so all loop iterations share the **same variable**.

---

### ❌ Problem Example: Using `var`

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Output after 1 second: 3, 3, 3 ❌
```

All callbacks share the same i, and its final value is 3.

✅ Fix: Use let (Block-Scoped)

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Output after 1 second: 0, 1, 2 ✅
```
let creates a new scope for each iteration, preserving the correct value.

📌 Why It Happens

|Variable | Scope | Behavior in Loop|
|---------|-------|-----------------|
|var | Function | Same instance reused|
|let | Block | New instance per loop|

💡 Manual Fix with IIFE (Before let)

```js
for (var i = 0; i < 3; i++) {
  (function (j) {
    setTimeout(() => console.log(j), 1000);
  })(i);
}
// Output: 0, 1, 2 ✅
```
The IIFE captures i in a new scope each time, simulating let behavior.

🧠 Summary
- Closures inside loops with var can cause bugs due to shared reference.
- Use let or an IIFE to create separate scope for each iteration.
- This is one of the most common JavaScript interview pitfalls — and mastering it shows real understanding of scope.

💡 Rule: Use let in loops unless you really know what you’re doing with var.

## 🔄 Closures in Currying

**Currying** is the process of transforming a function with multiple arguments into a sequence of **nested functions**, each taking a single argument.

Closures make currying possible by preserving the values passed into earlier functions.

---

### ✅ Example: Curried Multiply Function

```js
function multiply(x) {
  return function (y) {
    return x * y;
  };
}

const double = multiply(2);
console.log(double(5)); // 10
```
🔍 double remembers the value 2 via closure, even though multiply() has already returned.

📌 How It Works
- multiply(2) returns a new function.
- This returned function closes over x = 2.
- When you later call double(5), it computes 2 * 5.

🧠 Why Use Currying?

|Benefit | Description|
|--------|------------|
|Partial Application | Reuse functions with fixed values|
|Functional Composition | Combine logic in modular ways|
|Cleaner APIs | Especially useful in React, Redux, Lodash, etc.|

🛠 More Dynamic Example

```js
const greet = (greeting) => (name) => `${greeting}, ${name}!`;

const sayHi = greet("Hi");
console.log(sayHi("Abu")); // Hi, Abu!
```
💬 You can build reusable templates or utilities with less code and more flexibility.

🧠 Summary
- Currying splits function calls into smaller, manageable chunks.
- Closures allow earlier arguments to stay available for later use.
- Common in functional programming, React hooks, and utility libraries like Lodash.

💡 Closures make currying powerful by keeping the original context alive!

## 🧮 Call Stack (Execution Context)

The **Call Stack** is how JavaScript keeps track of what function is currently executing.

It's a **Last In, First Out (LIFO)** stack — functions are **pushed** onto the stack when called, and **popped** off when they finish.

---

### ✅ Example: Function Calls in Action

```js
function one() {
  two();
}
function two() {
  console.log("Two");
}

one(); // one -> two -> console.log
```
🔁 Here's what happens:

- one() is called → pushed onto the stack.
- Inside one(), two() is called → pushed onto the stack.
- console.log("Two") runs.
- two() finishes → popped off the stack.
- one() finishes → popped off the stack.

📦 Visualizing the Stack

```sql
|              |
| console.log  | ← executes first
| two()        |
| one()        | ← called first
```
As each function finishes, it’s removed from the stack.

⚠️ Stack Overflow Example
```js
function recurse() {
  recurse();
}

recurse(); // ❌ Maximum call stack size exceeded
```
💥 The function keeps calling itself infinitely, causing a stack overflow error.

🧠 Why It Matters
- Helps debug issues like infinite recursion or unexpected execution order.
- Important for understanding synchronous vs asynchronous behavior in JavaScript.

📌 Summary

|Term | Description|
|-----|------------|
|Call Stack | Keeps track of function calls|
|LIFO | Last-In-First-Out mechanism|
|Push | Add a function to the stack|
|Pop | Remove function once it returns|

# Event Loop + Concurrency Model

JavaScript is **single-threaded**, but it can handle asynchronous operations using the **Event Loop**.

## 🔑 Key Concepts

- **Call Stack**  
  Executes synchronous code line by line.

- **Web APIs (Browser)**  
  Handles asynchronous operations like `setTimeout`, DOM events, AJAX, etc.

- **Callback Queue (Macrotask Queue)**  
  Stores callbacks from asynchronous operations such as `setTimeout`, `setInterval`, and event handlers.

- **Microtask Queue**  
  Contains tasks like `Promise.then` callbacks and `queueMicrotask`.

## 🔁 Flow Overview

1. **Call Stack** starts executing synchronous code.
2. When the **Call Stack is empty**, the **Event Loop** checks for pending tasks.
3. **Microtasks** are executed first (from the Microtask Queue).
4. Once all microtasks are processed, **macrotasks** (from the Callback Queue) are executed.

## 🧪 Microtasks vs Macrotasks

Let's break down how JavaScript handles asynchronous tasks using microtasks and macrotasks.

### 🔍 Example Code

```js
console.log("Start");

setTimeout(() => {
  console.log("Macrotask - Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask - Promise");
});

console.log("End");
```
🧠 Output
```sql
Start  
End  
Microtask - Promise  
Macrotask - Timeout
```
🤔 Why Does This Happen?
- console.log("Start") and console.log("End") are synchronous and run immediately.
- setTimeout(..., 0) schedules a macrotask (callback goes to the macrotask queue).
- Promise.resolve().then(...) schedules a microtask (callback goes to the microtask queue).
- Once the call stack is empty, the event loop runs all microtasks first, then picks one macrotask to run.

🧠 Understanding the Queues

|Task Type | Queue | Examples | When it runs|
|----------|-------|----------|-------------|
Microtask | Microtask Queue | Promise.then, queueMicrotask | Right after the current script
Macrotask | Callback Queue | setTimeout, setInterval, DOM events | After all microtasks are done

💡 Use Cases
- Microtasks
    - Ideal for fine-grained updates or actions that should happen immediately after the current operation, e.g., chaining Promise logic.
    - Useful in frameworks (e.g., React uses microtasks for state batching).

- Macrotasks
    - Used for timed callbacks, event listeners, and tasks that can wait until the current operation and all microtasks are done.
    - Ideal for animations, UI updates, timers.

🧾 Summary
- JavaScript uses the event loop to manage concurrency in a single-threaded environment.
- Microtasks always run before macrotasks, even if scheduled at the same time.
- Choose the right task type based on urgency and priority of execution.

Tip: Always keep in mind the microtask queue can starve the event loop if it never empties — avoid infinite microtask loops!

| Function | Type | Queue | Description |
|----------|------|-------|-------------|
setTimeout | Macrotask | Callback Queue | Executes once after a specified delay. In this case, after 0ms.
queueMicrotask | Microtask | Microtask Queue | Executes after the current task and before any macrotasks.
Promise.then | Microtask | Microtask Queue | Resolves immediately and queues the .then() callback as a microtask.
setInterval | Macrotask | Callback Queue | Repeatedly executes the callback after the specified interval.

✅ Use Cases & Notes
- setTimeout: Schedule delayed tasks (like animations, async polling).
- setInterval: Repeating actions (e.g., clocks, live updates).
- Promise: Use for chaining async operations in a clean, readable way.
- queueMicrotask: For very fine-grained async behavior, often used in library internals.

🧾 Quick Recap
- Microtasks run before any macrotasks, even if delay is 0ms.
- Microtasks are ideal for short tasks that need to run immediately after the current operation.
- Use macrotasks like setTimeout and setInterval for operations that should happen after all microtasks are done, or on a timer.

💬 You can think of microtasks as "high priority" short tasks, while macrotasks are "scheduled" tasks waiting their turn.

## 🔄 Promises + async/await

Modern JavaScript uses `Promise` and `async/await` to write asynchronous code that reads like synchronous code.

### 🔍 Example Code

```js
const fetchData = () =>
  new Promise((resolve) => setTimeout(() => resolve("🚀"), 1000));

async function getData() {
  const data = await fetchData();
  console.log("Got:", data);
}

getData();
```
🧠 What Happens
- fetchData() returns a Promise that resolves after 1 second (setTimeout).
- The await keyword pauses execution inside getData() until the Promise resolves.
- Once resolved, execution resumes and "Got: 🚀" is logged.

🔁 How it Fits Into the Event Loop
- setTimeout(..., 1000) queues a macrotask to resolve the Promise after 1 second.
- Once the timer expires, the Promise is resolved, and the await resumes.
- The continuation (console.log(...)) is scheduled as a microtask.

🧩 Breakdown: async/await Under the Hood

|Concept | Behind the Scenes | Type|
|--------|-------------------|-----|
async | Wraps function in a Promise | Synchronous until await
await | Pauses function, resumes on resolution | Microtask on resume
setTimeout | Used here to simulate delay | Macrotask

✅ Use Cases
- Clean, readable handling of asynchronous operations.
- Works great for API calls, delays, sequential async flows.
- Replaces the "callback hell" or .then().then() chaining with simpler code.

🧾 Summary
- async/await simplifies working with Promises.
- Awaited code pauses only inside the async function, not the whole program.
- Resuming after await happens via microtask queue.

💡 Async/await doesn't block the thread — it just schedules what happens next and lets other code run while waiting.

## 🧠 Array Methods Mastery

JavaScript arrays come with powerful built-in methods for transforming, filtering, and analyzing data. Here's a quick dive into the most commonly used ones.

### 🔍 Example Code

```js
const nums = [1, 2, 3, 4, 5];

nums.map((n) => n * 2);            // [2, 4, 6, 8, 10]
nums.filter((n) => n % 2 === 0);   // [2, 4]
nums.reduce((acc, n) => acc + n, 0); // 15
nums.find((n) => n > 3);           // 4
nums.some((n) => n > 3);           // true
nums.every((n) => n < 10);         // true
nums.sort((a, b) => b - a);        // [5, 4, 3, 2, 1]
nums.forEach((n) => console.log(n)); // Logs each value
```

📌 Method Breakdown

|Method | Description | Returns | Mutates Original?|
|-------|-------------|---------|------------------|
.map() | Transforms each element and returns a new array | New array | ❌ No
.filter() | Filters elements based on a condition | New array | ❌ No
.reduce() | Reduces array to a single value using an accumulator | Any value | ❌ No
.find() | Finds the first element that matches a condition | First matching value | ❌ No
.some() | Checks if any element matches a condition | Boolean | ❌ No
.every() | Checks if all elements match a condition | Boolean | ❌ No
.sort() | Sorts the array based on a comparison function | Sorted array | ✅ Yes
.forEach() | Executes a function for each element (no return value) | undefined | ❌ No

✅ Use Cases
- .map(): Apply transformations (e.g., double numbers, format strings).
- .filter(): Remove unwanted elements (e.g., odd numbers, invalid data).
- .reduce(): Aggregate data (e.g., total sum, average, object merging).
- .find(): Grab a specific item (e.g., first match in a search).
- .some()/.every(): Validation or condition checks.
- .sort(): Arrange values (e.g., scores, names, timestamps).
- .forEach(): Perform side effects (e.g., logging, DOM updates).


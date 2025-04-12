[Back to Javascript Home Page](./README.md#)

## 🚀 **Intermediate Topics**

These are essential to writing powerful, clean, and modular code:

- [**Function Scope vs Block Scope**](#function-scope-vs-block-scope)
- [**Hoisting**](#hoisting)
- [**Closures**](#closures)
- [**The `this` Keyword**](#the-this-keyword)
- [**Arrow Functions**](#arrow-functions)
- [**Rest and Spread Operators**](#rest-and-spread-operators)
- [**Destructuring Arrays and Objects**](#destructuring-arrays-and-objects)
- [**Template Literals**](#template-literals)
- [**Object Methods & `this` in Objects**](#object-methods--this-in-objects)
- [**Callbacks**](#callbacks)
- **Array Methods**
  - `map`, `filter`, `re duce`, `find`, `some`, `every`, `sort`, `flat`, etc.
- **Object Manipulation**
  - Cloning, Merging, Freezing
- **ES6 Modules**
  - `import` / `export`
- **Strict Mode**
- **Optional Chaining (`?.`)**
- **Nullish Coalescing (`??`)**
- **Default Parameters**
- **Set, Map, WeakSet, WeakMap**
- **Basic DOM Manipulation**
- **Event Handling**
  - `addEventListener`, event types, bubbling, capturing, delegation

---

### **Function Scope vs Block Scope**

Understanding scope is crucial in JavaScript — it determines where variables are accessible in your code. Let's dive into the difference between **function scope** and **block scope**.

#### 🔹 Function Scope 🧭

A variable declared using `var` is **function scoped**, meaning it's only accessible **within the function** where it is defined. If you declare a variable inside a function using `var`, you can't access it from outside that function.

```js
function greet() {
  var message = "Hello!";
  console.log(message); // ✅ Accessible here
}
console.log(message); // ❌ ReferenceError: message is not defined
```

Even if `var` is declared inside a block (e.g., `if`), it still belongs to the enclosing function — **not just the block**.

```js
function test() {
  if (true) {
    var x = 5;
  }
  console.log(x); // ✅ Outputs: 5
}
```

#### 🔹 Block Scope 🚧

Variables declared with `let` and `const` are **block scoped**, meaning they're only accessible **inside the block `{}`** where they’re declared.

```js
if (true) {
  let a = 10;
  const b = 20;
  console.log(a, b); // ✅ Accessible here
}
console.log(a); // ❌ ReferenceError
console.log(b); // ❌ ReferenceError
```

This makes `let` and `const` safer and more predictable than `var`, especially in loops and conditional statements.

#### 🔄 Scope in Loops Example 🔂

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log("var i:", i), 1000); // Prints 3, 3, 3
}

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log("let j:", j), 1000); // Prints 0, 1, 2
}
```

- `var` leaks outside the loop and maintains a single binding.
- `let` creates a **new binding for each iteration**, preserving the value.

#### 🧠 Best Practice Tip

Always use `let` or `const` (preferably `const` by default unless reassignment is needed) to avoid unexpected behavior caused by `var`'s function-scoped nature. 🛡️🧱⚙️

[Back to Top](#)

---

### **Hoisting**

**Hoisting** is a behavior in JavaScript where variable and function declarations are **moved to the top of their scope** during the compilation phase — before code execution. This allows you to use variables and functions *before* they are declared in the code.

#### 🔹 Variable Hoisting

Variables declared with `var` are **hoisted** and initialized with `undefined`.

```js
console.log(name); // undefined (not ReferenceError)
var name = "Vishnu";
```

- Behind the scenes, JavaScript interprets it as:
  ```js
  var name;
  console.log(name);
  name = "Vishnu";
  ```

✅ *Note:* Only the **declaration** is hoisted, not the **initialization**.

#### ❗️`let` and `const` Hoisting

- `let` and `const` **are hoisted**, but they are not initialized.
- Accessing them **before the declaration** results in a **ReferenceError** due to the *Temporal Dead Zone (TDZ)*.

```js
console.log(age); // ❌ ReferenceError
let age = 25;
```

#### 🔹 Function Hoisting

- **Function Declarations** are fully hoisted:
  ```js
  greet(); // ✅ Works
  function greet() {
    console.log("Hello!");
  }
  ```

- **Function Expressions** are *not* hoisted the same way:
  ```js
  sayHi(); // ❌ TypeError: sayHi is not a function
  var sayHi = function () {
    console.log("Hi!");
  };
  ```

#### 🧠 Summary

| Type                | Hoisted | Initialized | Accessible Before Declaration |
|---------------------|---------|-------------|-------------------------------|
| `var`               | ✅ Yes  | ✅ undefined| ✅ (but undefined)             |
| `let`, `const`      | ✅ Yes  | ❌ No       | ❌ (TDZ Error)                |
| Function Declaration| ✅ Yes  | ✅ Yes      | ✅                            |
| Function Expression | ✅ Var  | ❌ No       | ❌                            |

🧠💡 Hoisting can lead to unexpected results if not properly understood — always declare variables and functions at the top of their scope or before using them for clarity and safety. 📚🛡️🔍

[Back to Top](#)

---

### **Closures**

**Closures** are one of JavaScript’s most powerful features. A closure gives you access to an **outer function’s scope** from an **inner function**, even after the outer function has finished executing. 🤯✨🔍

#### 🔹 What is a Closure?

A **closure** is created when:

1. A function is defined **inside another function**, and
2. The inner function **references variables** from the outer function.

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

Even though `outer()` has already returned, the `inner()` function still remembers the variable `count`. That’s the magic of closures. 🪄📦🔁

#### 🔹 Why Use Closures?

- **Data Privacy / Encapsulation**  
  You can simulate private variables:

  ```js
  function createCounter() {
    let count = 0;

    return {
      increment() {
        count++;
        console.log(count);
      },
      reset() {
        count = 0;
      }
    };
  }

  const counter = createCounter();
  counter.increment(); // 1
  counter.increment(); // 2
  ```

- **Maintain state** across function calls.
- **Functional programming** techniques like `currying`.

#### 🔹 Closures in Loops

Closures inside loops often lead to unexpected behavior unless scoped correctly:

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // prints 3, 3, 3
}
```

Fix it using `let` or IIFE:

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // prints 0, 1, 2
}
```

#### 🧠 Summary

Closures are formed every time a function is created. They:

- "Close over" the variables of their outer scope.
- Let functions remember their lexical environment.
- Enable data hiding and functional patterns.

🎯🔐 Closures are a core part of how JavaScript handles **scope** and **functions** — understanding them unlocks new levels of JS mastery. 💪🛠️🚀

[Back to Top](#)

---

### **The `this` Keyword***

In JavaScript, the value of `this` refers to the **execution context** — the object that is currently "calling" the function. It might seem confusing at first, but once you understand the rules, it's very predictable! 🔍📖🔁

#### 🔹 Global Context

In the global scope (`outside any function`), `this` refers to the **global object**:

- In browsers: `window`
- In Node.js: `global`

```js
console.log(this); // window (in browser)
```

#### 🔹 Inside a Function (Non-Strict Mode)

In regular functions (non-arrow), `this` refers to the **global object** (in non-strict mode):

```js
function show() {
  console.log(this); // window (in browser)
}
show();
```

But in **strict mode**, `this` is `undefined`:

```js
'use strict';
function show() {
  console.log(this); // undefined
}
show();
```

#### 🔹 Inside an Object Method

When a function is called as a **method of an object**, `this` refers to that object:

```js
const user = {
  name: 'Alice',
  greet() {
    console.log(`Hi, I am ${this.name}`);
  }
};

user.greet(); // "Hi, I am Alice"
```

#### 🔹 Arrow Functions (No Own `this`)

Arrow functions **do not have their own `this`**. They inherit `this` from the **surrounding lexical scope**:

```js
const person = {
  name: 'Bob',
  greet: () => {
    console.log(this.name); // undefined (refers to global this)
  }
};

person.greet();
```

```js
function outer() {
  const arrow = () => console.log(this);
  arrow();
}
outer(); // 'this' refers to outer()'s this
```

#### 🔹 `this` in Event Handlers

- **Regular function**: `this` refers to the DOM element

  ```js
  button.addEventListener("click", function() {
    console.log(this); // button element
  });
  ```

- **Arrow function**: `this` is inherited from the surrounding context (not the element)

  ```js
  button.addEventListener("click", () => {
    console.log(this); // likely window or enclosing scope
  });
  ```

#### 🔹 Controlling `this`: `call`, `apply`, and `bind`

You can **explicitly set the value of `this`** using:

- `call`: Calls the function with a given `this` and arguments

  ```js
  function greet() {
    console.log(this.name);
  }

  const user = { name: 'Eve' };
  greet.call(user); // Eve
  ```

- `apply`: Same as `call`, but takes arguments as an array

- `bind`: Returns a new function with bound `this`

  ```js
  const boundGreet = greet.bind(user);
  boundGreet(); // Eve
  ```

#### 🧠 Summary

- `this` refers to the **caller** or **owner** of the function.
- Arrow functions inherit `this` from their **lexical scope**.
- You can manually set `this` using `call`, `apply`, or `bind`.

🎯 Learning `this` helps you write more predictable and powerful JavaScript, especially in event handlers, OOP, and async patterns. 🔄💡🎯

[Back to Top](#)

---

### **Arrow Functions**

Arrow functions, introduced in **ES6 (ECMAScript 2015)**, offer a **shorter syntax** for writing functions. They’re not just syntactic sugar — they behave differently than regular functions, especially when it comes to `this`.

#### 🔹 Syntax: Clean & Concise

```js
// Traditional function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;
```

- If only **one parameter**, you can skip the parentheses:
  ```js
  const square = x => x * x;
  ```

- If **no parameters**, you must use empty parentheses:
  ```js
  const greet = () => console.log("Hello!");
  ```

- If you need **multiple lines or logic**, use curly braces and `return`:
  ```js
  const multiply = (a, b) => {
    const result = a * b;
    return result;
  };
  ```

#### 🔹 No Own `this` 🚫

Arrow functions do **not have their own `this`**. They inherit `this` from the **surrounding (lexical) scope**.

```js
const person = {
  name: "Alice",
  greet: function () {
    const arrow = () => {
      console.log(`Hi, I'm ${this.name}`);
    };
    arrow();
  },
};

person.greet(); // "Hi, I'm Alice"
```

If you used a regular function inside `greet()`, `this.name` would be `undefined` unless explicitly bound.

#### 🔹 Cannot Be Used As Constructors 🚫

Arrow functions **cannot** be used with the `new` keyword:

```js
const Person = (name) => {
  this.name = name;
};
const p = new Person("Bob"); // ❌ TypeError
```

#### 🔹 `arguments` Object is Not Available

Arrow functions **do not** have the `arguments` object (use rest parameters instead):

```js
const showArgs = () => {
  console.log(arguments); // ❌ ReferenceError
};

function normalShowArgs() {
  console.log(arguments); // ✅ Works
}
```

Use rest parameters in arrow functions if you need similar behavior:

```js
const showArgs = (...args) => {
  console.log(args);
};
```

#### 🔹 Perfect Use Cases

- Short one-liners and callbacks
- Functional programming (e.g., `map`, `filter`, `reduce`)
- When you want `this` to be preserved

```js
const numbers = [1, 2, 3];
const squared = numbers.map(n => n * n);
```

#### 🧠 Quick Recap

| Feature                     | Arrow Function      | Regular Function     |
|----------------------------|---------------------|----------------------|
| Shorter syntax             | ✅                  | ❌                   |
| Own `this`                 | ❌ (lexical)         | ✅                   |
| Used with `new`            | ❌                  | ✅                   |
| Has `arguments` object     | ❌                  | ✅                   |

[Back to Top](#)

---

### **Rest and Spread Operators**

The `...` syntax in JavaScript can do **two powerful things**, depending on where it’s used:

- **Rest Operator**: **Collects** multiple elements into an array (used in function parameters or destructuring).
- **Spread Operator**: **Spreads** elements out of an array or object into individual parts (used in function calls, array/object literals).

#### 🟣 Rest Operator

✅ **Gathers** values into a single array.

Used when **declaring functions** or doing **destructuring**.

#### 🛠️ In Function Parameters:

```js
function sum(...numbers) {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}

sum(1, 2, 3); // 6
```

- All passed arguments are collected into the `numbers` array.

#### 🛠️ In Destructuring:

```js
const [first, ...rest] = [10, 20, 30, 40];
console.log(first); // 10
console.log(rest);  // [20, 30, 40]
```

#### 🟢 Spread Operator

✅ **Spreads** array or object elements one-by-one.

Used when **calling functions**, creating **arrays/objects**, or copying data.

#### 🛠️ In Function Calls:

```js
const nums = [1, 2, 3];
Math.max(...nums); // 3
```

- Spreads elements as individual arguments: `Math.max(1, 2, 3)`

#### 🛠️ For Array Copying or Merging:

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; 
console.log(arr2); // [1, 2, 3, 4]
```

#### 🛠️ For Object Copying or Merging:

```js
const user = { name: "Alice" };
const updatedUser = { ...user, age: 25 };
console.log(updatedUser); // { name: "Alice", age: 25 }
```

#### 🔍 Summary Table

| Feature              | Rest (`...`)                          | Spread (`...`)                          |
|----------------------|----------------------------------------|------------------------------------------|
| Purpose              | Combine multiple values into one       | Unpack values into individual elements   |
| Use Case             | Function parameters, destructuring     | Function calls, array/object construction |
| Result               | Always an array                        | Individual values                        |

[Back to Top](#)

---

### **Destructuring Arrays and Objects**

**Destructuring** is a concise way to **unpack values** from arrays or **extract properties** from objects into individual variables. It's super useful for cleaner and more readable code! 🧼✨💡

#### 🔹 Array Destructuring

You can unpack values from arrays based on their **index positions**.

```js
const numbers = [10, 20, 30];
const [a, b, c] = numbers;

console.log(a); // 10
console.log(b); // 20
```

#### ✅ Skipping Items:

```js
const [first, , third] = [1, 2, 3];
console.log(third); // 3
```

#### ✅ Default Values:

```js
const [x = 5, y = 10] = [undefined];
console.log(x); // 5
console.log(y); // 10
```

#### 🔸 Object Destructuring

Extract properties by **matching names**:

```js
const user = { name: "Alice", age: 25 };
const { name, age } = user;

console.log(name); // "Alice"
console.log(age);  // 25
```

#### ✅ Renaming Variables:

```js
const { name: userName } = user;
console.log(userName); // "Alice"
```

#### ✅ Default Values:

```js
const { city = "Unknown" } = user;
console.log(city); // "Unknown"
```

#### 🌟 Nested Destructuring

```js
const person = {
  name: "Bob",
  address: {
    city: "New York",
    zip: 10001
  }
};

const {
  address: { city }
} = person;

console.log(city); // "New York"
```

#### 🧠 Why Use Destructuring?

- Makes code more **concise and expressive**
- Reduces boilerplate when working with objects/arrays
- Commonly used with React props, API responses, etc.

[Back to Top](#)

---

### **Template Literals**

Template literals (also known as **template strings**) provide a cleaner, more powerful way to work with strings in JavaScript. Introduced in ES6, they support **multiline strings**, **interpolation**, and **expression embedding**. 🎯📝🔧

#### 🔹 Syntax

Template literals use **backticks** (`` ` ``) instead of single or double quotes.

```js
const name = "Vishnu";
const greeting = `Hello, ${name}!`;
console.log(greeting); // Hello, Vishnu!
```

#### ✨ Features of Template Literals

##### ✅ 1. String Interpolation

You can embed **variables** and **expressions** directly inside `${...}`:

```js
const a = 5;
const b = 10;
console.log(`The sum is ${a + b}`); // The sum is 15
```

##### ✅ 2. Multiline Strings

No need for `\n` or concatenation for multiple lines.

```js
const multi = `This is line 1
This is line 2
This is line 3`;
console.log(multi);
```

##### ✅ 3. Expression Embedding

You can run full JavaScript expressions:

```js
const price = 10;
const quantity = 3;
console.log(`Total: $${price * quantity}`); // Total: $30
```

#### ⚡ Use Cases

- Dynamic HTML generation
- Logging/debugging
- React JSX-style string templates
- Reducing complexity in string operations

#### 🚫 Common Mistake

Don’t use quotes with backticks like this:

```js
// ❌ Incorrect
const str = "`This is wrong`";

// ✅ Correct
const str = `This is right`;
```

[Back to Top](#)

---

### **Object Methods & `this` in Objects**

In JavaScript, functions that are properties of an object are called **methods**. When these methods are called, the special keyword `this` refers to the object the method is called on. 🧩🔍📦

#### 🔹 Defining Object Methods

```js
const user = {
  name: "Vishnu",
  greet: function () {
    return `Hello, my name is ${this.name}`;
  }
};

console.log(user.greet()); // Hello, my name is Vishnu
```

Here, `greet` is a **method**, and `this.name` refers to the `user.name`.

#### 🔹 ES6 Shorthand for Methods

You can define methods without the `function` keyword:

```js
const user = {
  name: "Vishnu",
  greet() {
    return `Hi, I’m ${this.name}`;
  }
};
```

Same result, cleaner syntax! ✅

#### 🔍 Understanding `this` in Object Methods

- `this` inside a method refers to the object the method belongs to.
- It points to the **left of the dot** when the method is called.

```js
const person = {
  name: "Alice",
  sayHi() {
    console.log(this.name);
  }
};

person.sayHi(); // Alice
```

#### ⚠️ Gotcha: `this` with Arrow Functions

Arrow functions don’t bind their own `this`. They inherit it from their **lexical scope**.

```js
const user = {
  name: "Vishnu",
  greet: () => {
    console.log(this.name); // `this` is NOT the user object
  }
};

user.greet(); // undefined
```

Use **regular functions** for object methods if you rely on `this`.

#### 🔁 Method Borrowing

You can use `call`, `apply`, or `bind` to borrow methods:

```js
const user1 = { name: "Vishnu" };
const user2 = { name: "Arjun" };

function sayName() {
  console.log(this.name);
}

sayName.call(user1); // Vishnu
sayName.call(user2); // Arjun
```

#### 🛠️ Real-World Usage

- DOM event handlers in objects
- OOP-style design patterns
- Reusing logic in components/modules

[Back to Top](#)

---

### **Callbacks**

A **callback** is a function passed into another function as an argument, which is then **invoked** (called back) at a later time. They are foundational to handling asynchronous code in JavaScript. 🧠⏳🧩

#### 🔹 Why Use Callbacks?

JavaScript is **non-blocking** and runs code asynchronously. Callbacks allow you to:

- Wait for an operation to complete (like fetching data)
- Define **what to do next** after an action finishes
- Avoid blocking the main thread (UI remains responsive)

#### 🔹 Basic Syntax of a Callback

```js
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

function sayBye() {
  console.log("Goodbye!");
}

greet("Vishnu", sayBye);
```

**Output:**
```
Hello Vishnu
Goodbye!
```

Here, `sayBye` is a **callback function** passed to `greet`.

#### 🔹 Callback in Asynchronous Code

```js
console.log("Start");

setTimeout(() => {
  console.log("I run after 2 seconds");
}, 2000);

console.log("End");
```

Output:
```
Start
End
I run after 2 seconds
```

Even though `setTimeout` is first in appearance, it runs later due to the event loop mechanism. The callback is executed after 2 seconds. ⏱️

#### ⚠️ Callback Hell

Nesting too many callbacks can lead to messy, hard-to-read code (known as **callback hell** or the **pyramid of doom**):

```js
login(user, () => {
  fetchData(() => {
    renderUI(() => {
      console.log("All done!");
    });
  });
});
```

This becomes difficult to maintain. Modern JavaScript uses **Promises** and **async/await** to address this. 🚨

#### ✅ When to Use Callbacks

- In older APIs or libraries (like jQuery)
- For simple async tasks or quick utilities
- When using Node.js-style callbacks (`err, result`)

#### 🛠️ Real-World Examples

- Handling API responses
- Event listeners (`onClick`, `onSubmit`, etc.)
- File reading in Node.js

```js
fs.readFile("file.txt", (err, data) => {
  if (err) throw err;
  console.log(data.toString());
});
```

[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---

### ****



[Back to Top](#)

---
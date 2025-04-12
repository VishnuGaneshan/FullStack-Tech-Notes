
[Back to Javascript Home Page](./README.md#)


## 🧠 **Advanced Topics**

These give deeper understanding of how JavaScript works and are often asked in interviews:

- [**Asynchronous JavaScript**](#asynchronous-javascript)
  - Callbacks
  - Promises
  - `async/await`
- [**JavaScript Event Loop**](#javascript-event-loop)
  - Call Stack
  - Callback Queue
  - Microtask Queue
  - Task Prioritization
- [**Memory Management**](#memory-management)
  - Garbage Collection
  - Memory Leaks
- [**Prototypal Inheritance**](#prototypal-inheritance)
  - `Object.create()`
  - `__proto__`, `prototype`
  - Class Syntax (`class`, `extends`, `super`)
- [**The `new` Keyword**](#the-new-keyword)
- [**`bind`, `call`, `apply`**](#bind-call-apply)
- [**Custom Error Handling**](#custom-error-handling)
  - `try`, `catch`, `finally`, `throw`
- [**IIFE (Immediately Invoked Function Expression)**](#iife-immediately-invoked-function-expression)
- [**Module Bundlers & Tools**](#module-bundlers--tools)
  - Webpack, Babel (Basics)
- [**Event-driven Architecture**](#event-driven-architecture)
- [**Custom Events**](#custom-events)
- [**Throttling & Debouncing**](#throttling--debouncing)
- [**Service Workers & Web APIs**](#service-workers--web-apis)
- [**Security Concepts**](#security-concepts)
  - XSS, CSRF (Basics)
- [**JavaScript Patterns**](#javascript-patterns)
  - Module, Revealing Module, Singleton, Observer, Factory
- [**Functional Programming in JS**](#functional-programming-in-js)
  - Pure Functions, Immutability, Higher-Order Functions
- [**Currying & Partial Application**](#currying--partial-application)
- [**Generators and Iterators**](#generators-and-iterators)
- [**Symbols & Iterables**](#symbols--iterables)
- [**Proxy and Reflect API**](#proxy-and-reflect-api)
- [**Typed Arrays & Buffers**](#typed-arrays--buffers)

---

### **Asynchronous JavaScript**

JavaScript is single-threaded, but it can handle asynchronous operations using **callbacks**, **promises**, and **async/await**. Let’s explore these concepts. 🔄⏳

#### 🔹 Callbacks

A **callback** is a function passed as an argument to another function and executed later.

```js
function fetchData(callback) {
  setTimeout(() => {
    callback("Data fetched!");
  }, 1000);
}

fetchData((data) => {
  console.log(data); // Data fetched!
});
```

- **Use Case**: Handling asynchronous tasks like API calls or timers.

#### 🔹 Promises

A **promise** represents a value that may be available now, in the future, or never. It has three states: **pending**, **fulfilled**, and **rejected**.

```js
const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Data fetched!"), 1000);
});

fetchData
  .then((data) => console.log(data)) // Data fetched!
  .catch((error) => console.error(error));
```

- **Use Case**: Chaining asynchronous operations.

#### 🔹 `async/await`

`async/await` simplifies working with promises by allowing you to write asynchronous code that looks synchronous.

```js
async function fetchData() {
  const data = await new Promise((resolve) => setTimeout(() => resolve("Data fetched!"), 1000));
  console.log(data);
}

fetchData(); // Data fetched!
```

- **Use Case**: Cleaner and more readable asynchronous code.

[Back to Top](#)

---

### **JavaScript Event Loop**

The **event loop** is what allows JavaScript to perform non-blocking operations, even though it’s single-threaded. Let’s break it down. 🔄🕒

#### 🔹 Call Stack

The **call stack** is where JavaScript keeps track of function calls.

```js
function first() {
  console.log("First");
}

function second() {
  console.log("Second");
}

first();
second();
// Output: First, Second
```

#### 🔹 Callback Queue

The **callback queue** holds tasks (e.g., `setTimeout`) that are ready to be executed after the call stack is empty.

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
// Output: Start, End, Timeout
```

#### 🔹 Microtask Queue

The **microtask queue** (e.g., `Promise.then`) has higher priority than the callback queue.

```js
console.log("Start");

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
// Output: Start, End, Promise
```

#### 🔹 Task Prioritization

Tasks in the **microtask queue** are executed before tasks in the **callback queue**.

[Back to Top](#)

---

### **Memory Management**

JavaScript automatically manages memory using **garbage collection**, but understanding how it works can help you avoid memory leaks. 🧠💾

#### 🔹 Garbage Collection

JavaScript uses a **mark-and-sweep** algorithm to remove objects that are no longer reachable.

```js
let obj = { name: "Alice" };
obj = null; // The object is eligible for garbage collection
```

#### 🔹 Memory Leaks

Memory leaks occur when objects are not properly released.

- **Common Causes**:
  - Global variables
  - Event listeners not removed
  - Closures holding references

```js
let leaks = [];
function addLeak() {
  leaks.push(new Array(1000000).fill("leak"));
}
```

- **Solution**: Use tools like Chrome DevTools to monitor memory usage.

[Back to Top](#)

---

### **Prototypal Inheritance**

JavaScript uses **prototypal inheritance**, where objects inherit properties and methods from other objects. 🧬🔗

#### 🔹 `Object.create()`

You can create an object with a specific prototype using `Object.create()`.

```js
const parent = { greet: () => console.log("Hello!") };
const child = Object.create(parent);

child.greet(); // Hello!
```

#### 🔹 `__proto__` and `prototype`

- `__proto__`: Refers to the prototype of an object.
- `prototype`: Refers to the prototype of a constructor function.

```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log(`Hello, I'm ${this.name}`);
};

const alice = new Person("Alice");
alice.greet(); // Hello, I'm Alice
```

#### 🔹 Class Syntax

The `class` syntax is a cleaner way to implement inheritance.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, I'm ${this.name}`);
  }
}

class Student extends Person {
  constructor(name, grade) {
    super(name);
    this.grade = grade;
  }

  study() {
    console.log(`${this.name} is studying.`);
  }
}

const bob = new Student("Bob", "A");
bob.greet(); // Hello, I'm Bob
bob.study(); // Bob is studying.
```

[Back to Top](#)

---

### **The `new` Keyword**

The `new` keyword is used to create an instance of an object from a constructor function. 🛠️🆕

```js
function Person(name) {
  this.name = name;
}

const alice = new Person("Alice");
console.log(alice.name); // Alice
```

- **How it works**:
  1. Creates a new empty object.
  2. Sets the prototype of the object to the constructor’s `prototype`.
  3. Executes the constructor function with `this` bound to the new object.
  4. Returns the new object.

[Back to Top](#)

---

### **`bind`, `call`, `apply`**

These methods allow you to control the value of `this` in a function. 🔗🖇️

#### 🔹 `bind()`

Returns a new function with `this` bound to a specific object.

```js
const person = { name: "Alice" };
function greet() {
  console.log(`Hello, ${this.name}`);
}

const boundGreet = greet.bind(person);
boundGreet(); // Hello, Alice
```

#### 🔹 `call()`

Calls a function with `this` set to a specific object and arguments passed individually.

```js
greet.call(person); // Hello, Alice
```

#### 🔹 `apply()`

Calls a function with `this` set to a specific object and arguments passed as an array.

```js
greet.apply(person); // Hello, Alice
```

[Back to Top](#)

---

### **Custom Error Handling**

JavaScript provides tools for handling errors gracefully. 🛡️⚠️

#### 🔹 `try`, `catch`, `finally`, `throw`

```js
try {
  throw new Error("Something went wrong!");
} catch (error) {
  console.error(error.message); // Something went wrong!
} finally {
  console.log("Cleanup code here.");
}
```

- **Use Case**: Handling runtime errors without crashing the application.

[Back to Top](#)

---

### **IIFE (Immediately Invoked Function Expression)**

An **IIFE** is a function that runs immediately after it is defined. 🔄⚡

```js
(function () {
  console.log("IIFE executed!");
})();
```

- **Use Case**: Creating a private scope to avoid polluting the global namespace.

[Back to Top](#)

---

### **Module Bundlers & Tools**

Modern JavaScript applications often use tools like **module bundlers** and **transpilers** to manage dependencies and ensure compatibility across different environments. Let’s explore two key tools: **Webpack** and **Babel**. 🛠️📦

#### 🔹 Webpack

**Webpack** is a module bundler that takes your JavaScript files (and other assets) and bundles them into a single file (or multiple files) for use in the browser.

##### Key Features:
1. **Code Splitting**: Breaks your code into smaller chunks for better performance.
2. **Loaders**: Allows you to process files like CSS, images, and TypeScript.
3. **Plugins**: Extend Webpack’s functionality (e.g., minification, environment variables).

##### Example Webpack Configuration:
```js
// webpack.config.js
const path = require("path");

module.exports = {
  entry: "./src/index.js", // Entry point
  output: {
    filename: "bundle.js", // Output file
    path: path.resolve(__dirname, "dist"), // Output directory
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Process .js files
        exclude: /node_modules/,
        use: {
          loader: "babel-loader", // Use Babel for transpiling
        },
      },
    ],
  },
};
```

- **Use Case**: Bundling JavaScript files, optimizing assets, and managing dependencies.

#### 🔹 Babel

**Babel** is a JavaScript transpiler that converts modern JavaScript (ES6+) into older versions (ES5) for compatibility with older browsers.

##### Key Features:
1. **Transpilation**: Converts ES6+ syntax to ES5.
2. **Plugins**: Add features like JSX support or experimental syntax.
3. **Presets**: Predefined configurations for specific environments (e.g., `@babel/preset-env`).

##### Example Babel Configuration:
```json
// .babelrc
{
  "presets": ["@babel/preset-env"]
}
```

##### Using Babel with Webpack:
```bash
npm install --save-dev babel-loader @babel/core @babel/preset-env
```

- **Use Case**: Ensuring compatibility with older browsers and environments.

[Back to Top](#)

---

### **Event-driven Architecture**

**Event-driven architecture** is a design pattern where the flow of the program is determined by events such as user actions, sensor outputs, or messages from other programs. It is widely used in JavaScript, especially in the browser and Node.js. 🔄📡

#### 🔹 How It Works

1. **Event Emitters**: Components emit events when something happens.
2. **Event Listeners**: Other components listen for these events and respond accordingly.

##### Example in Node.js:
```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Register an event listener
emitter.on("data", (message) => {
  console.log(`Received: ${message}`);
});

// Emit an event
emitter.emit("data", "Hello, World!");
```

- **Use Case**: Building scalable and decoupled systems.

#### 🔹 Advantages:
1. **Decoupling**: Components don’t need to know about each other.
2. **Scalability**: Easy to add new event listeners or emitters.
3. **Asynchronous**: Handles non-blocking operations efficiently.

#### 🔹 Common Use Cases:
- User interactions in the browser (e.g., clicks, keypresses).
- Server-side events in Node.js (e.g., HTTP requests, file I/O).
- Real-time applications (e.g., chat apps, notifications).

[Back to Top](#)

---

### **Custom Events**

Custom events allow you to define and dispatch your own events in JavaScript, enabling more flexible and modular code. 🔧📢

#### 🔹 Creating and Dispatching Custom Events

You can create custom events using the `CustomEvent` constructor and dispatch them using `dispatchEvent`.

```js
// Create a custom event
const event = new CustomEvent("myEvent", {
  detail: { message: "Hello, World!" }, // Pass custom data
});

// Add an event listener
document.addEventListener("myEvent", (e) => {
  console.log(e.detail.message); // Hello, World!
});

// Dispatch the event
document.dispatchEvent(event);
```

#### 🔹 Use Cases:
1. **Decoupling Components**: Allow different parts of your application to communicate without direct dependencies.
2. **Custom Interactions**: Trigger custom logic based on user actions or application state.

#### 🔹 Example: Custom Events in a Button Click
```js
const button = document.querySelector("#myButton");

// Create and dispatch a custom event
button.addEventListener("click", () => {
  const customEvent = new CustomEvent("buttonClicked", {
    detail: { clickedAt: new Date() },
  });
  button.dispatchEvent(customEvent);
});

// Listen for the custom event
button.addEventListener("buttonClicked", (e) => {
  console.log(`Button clicked at: ${e.detail.clickedAt}`);
});
```

#### 🔹 Advantages:
- **Flexibility**: Define events specific to your application’s needs.
- **Reusability**: Components can emit and listen for events without tight coupling.

[Back to Top](#)

---

### **Throttling & Debouncing**

These techniques optimize performance by controlling how often a function is executed. 🕒⚡

#### 🔹 Throttling

Ensures a function is called at most once in a specified time period.

```js
function throttle(func, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      func(...args);
    }
  };
}
```

#### 🔹 Debouncing

Ensures a function is called only after a specified delay has passed since the last call.

```js
function debounce(func, delay) {
  let timeout;
  return function (...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func(...args), delay);
  };
}
```

[Back to Top](#)

---

### **Service Workers & Web APIs**

Service Workers and Web APIs are essential for building modern, performant, and feature-rich web applications. Let’s explore their roles. 🌐⚙️

#### 🔹 Service Workers

A **Service Worker** is a script that runs in the background, separate from the main browser thread, enabling features like offline support, caching, and push notifications.

##### Key Features:
1. **Offline Support**: Cache assets to make your app work offline.
2. **Push Notifications**: Send notifications even when the app is not open.
3. **Background Sync**: Sync data in the background.

##### Example: Registering a Service Worker
```js
if ("serviceWorker" in navigator) {
  navigator.serviceWorker
    .register("/service-worker.js")
    .then(() => console.log("Service Worker registered"))
    .catch((error) => console.error("Service Worker registration failed:", error));
}
```

##### Example: Caching Files in a Service Worker
```js
self.addEventListener("install", (event) => {
  event.waitUntil(
    caches.open("v1").then((cache) => {
      return cache.addAll(["/index.html", "/styles.css", "/script.js"]);
    })
  );
});

self.addEventListener("fetch", (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
```

- **Use Case**: Progressive Web Apps (PWAs) for offline functionality and better performance.

#### 🔹 Web APIs

**Web APIs** are built into the browser and provide functionality for interacting with the browser and the web.

##### Examples of Web APIs:
1. **Fetch API**: For making HTTP requests.
   ```js
   fetch("https://api.example.com/data")
     .then((response) => response.json())
     .then((data) => console.log(data))
     .catch((error) => console.error(error));
   ```

2. **Geolocation API**: For accessing the user’s location.
   ```js
   navigator.geolocation.getCurrentPosition((position) => {
     console.log(position.coords.latitude, position.coords.longitude);
   });
   ```

3. **Web Storage API**: For storing data in the browser.
   ```js
   localStorage.setItem("key", "value");
   console.log(localStorage.getItem("key")); // value
   ```

4. **WebSockets API**: For real-time communication.
   ```js
   const socket = new WebSocket("wss://example.com/socket");
   socket.onmessage = (event) => console.log(event.data);
   ```

[Back to Top](#)

---

### **Security Concepts**

Security is critical in web development. Let’s explore two common vulnerabilities: **XSS** and **CSRF**. 🛡️🔒

#### 🔹 XSS (Cross-Site Scripting)

**XSS** occurs when an attacker injects malicious scripts into a website, which are then executed in the browser of other users.

##### Example of XSS:
```html
<!-- Vulnerable Code -->
<input type="text" id="input" />
<div id="output"></div>
<script>
  document.getElementById("input").addEventListener("input", (e) => {
    document.getElementById("output").innerHTML = e.target.value; // Vulnerable to XSS
  });
</script>
```

##### Prevention:
1. **Escape User Input**: Use libraries like DOMPurify.
   ```js
   const sanitized = DOMPurify.sanitize(userInput);
   ```
2. **Content Security Policy (CSP)**: Restrict the sources of scripts.
3. **Avoid `innerHTML`**: Use `textContent` instead.

#### 🔹 CSRF (Cross-Site Request Forgery)

**CSRF** tricks a user into performing actions they didn’t intend, such as transferring money or changing account settings.

##### Example of CSRF:
A malicious website sends a request to `https://bank.com/transfer` using the victim’s session.

##### Prevention:
1. **CSRF Tokens**: Include a unique token in forms.
2. **SameSite Cookies**: Restrict cookies to same-site requests.
   ```http
   Set-Cookie: sessionId=abc123; SameSite=Strict
   ```

[Back to Top](#)

---

### **JavaScript Patterns**

Design patterns provide reusable solutions to common problems in software design. Let’s explore some popular JavaScript patterns. 🛠️📐

#### 🔹 Module Pattern

Encapsulates code in a function to create private variables and methods.

```js
const Module = (() => {
  const privateVar = "I am private";

  return {
    publicMethod: () => console.log(privateVar),
  };
})();

Module.publicMethod(); // I am private
```

#### 🔹 Revealing Module Pattern

Exposes only specific methods and properties.

```js
const RevealingModule = (() => {
  let privateVar = "I am private";

  const privateMethod = () => console.log(privateVar);

  return {
    publicMethod: privateMethod,
  };
})();

RevealingModule.publicMethod(); // I am private
```

#### 🔹 Singleton Pattern

Ensures a class has only one instance.

```js
class Singleton {
  constructor() {
    if (Singleton.instance) {
      return Singleton.instance;
    }
    Singleton.instance = this;
  }
}

const instance1 = new Singleton();
const instance2 = new Singleton();
console.log(instance1 === instance2); // true
```

#### 🔹 Observer Pattern

Allows objects to subscribe to and react to events.

```js
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  notify(data) {
    this.observers.forEach((observer) => observer(data));
  }
}

const subject = new Subject();
subject.subscribe((data) => console.log(`Observer 1: ${data}`));
subject.subscribe((data) => console.log(`Observer 2: ${data}`));

subject.notify("Event triggered!");
```

#### 🔹 Factory Pattern

Creates objects without specifying their exact class.

```js
class Car {
  constructor(model) {
    this.model = model;
  }
}

class CarFactory {
  createCar(model) {
    return new Car(model);
  }
}

const factory = new CarFactory();
const car = factory.createCar("Tesla");
console.log(car.model); // Tesla
```

[Back to Top](#)

---

### **Functional Programming in JS**

Functional programming is a paradigm that treats computation as the evaluation of mathematical functions and avoids changing state or mutable data. 🧮🔗

#### 🔹 Pure Functions

A **pure function** always produces the same output for the same input and has no side effects.

```js
const add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```

#### 🔹 Immutability

Avoid modifying existing data; instead, create new data.

```js
const arr = [1, 2, 3];
const newArr = [...arr, 4];
console.log(newArr); // [1, 2, 3, 4]
```

#### 🔹 Higher-Order Functions

A **higher-order function** takes a function as an argument or returns a function.

```js
const multiply = (factor) => (num) => num * factor;
const double = multiply(2);
console.log(double(5)); // 10
```

[Back to Top](#)

---

### **Currying & Partial Application**

Currying and partial application are techniques for transforming functions to make them more reusable and composable. 🔄🛠️

#### 🔹 Currying

Transforms a function with multiple arguments into a sequence of functions, each taking a single argument.

```js
const add = (a) => (b) => a + b;
console.log(add(2)(3)); // 5
```

#### 🔹 Partial Application

Pre-fixes some arguments of a function, creating a new function with fewer arguments.

```js
const multiply = (a, b) => a * b;
const double = multiply.bind(null, 2);
console.log(double(5)); // 10
```

[Back to Top](#)

---

### **Generators and Iterators**

Generators and iterators provide a way to handle sequences of data. 🔄🔗

#### 🔹 Generators

A generator is a function that can pause and resume execution.

```js
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generator();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

#### 🔹 Iterators

An iterator is an object that defines a sequence and a way to access its elements.

```js
const iterable = [1, 2, 3];
const iterator = iterable[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: 3, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

[Back to Top](#)

---

### **Symbols & Iterables**

Symbols are a unique and immutable primitive data type introduced in ES6. They are often used as unique property keys, while iterables provide a way to define custom iteration behavior. 🔑🔄

#### 🔹 Symbols

A `Symbol` is a unique and immutable value.

```js
const sym1 = Symbol("description");
const sym2 = Symbol("description");

console.log(sym1 === sym2); // false
```

- **Use Case**: Creating unique property keys to avoid naming collisions.

```js
const obj = {
  [Symbol("id")]: 1,
  name: "Alice",
};

console.log(Object.keys(obj)); // ["name"]
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(id)]
```

#### 🔹 Iterables

An **iterable** is an object that implements the `Symbol.iterator` method, which returns an iterator.

```js
const iterable = {
  [Symbol.iterator]() {
    let step = 0;
    return {
      next() {
        step++;
        if (step <= 3) {
          return { value: step, done: false };
        }
        return { value: undefined, done: true };
      },
    };
  },
};

for (const value of iterable) {
  console.log(value); // 1, 2, 3
}
```

- **Use Case**: Customizing iteration behavior for objects.

[Back to Top](#)

---

### **Proxy and Reflect API**

The **Proxy** and **Reflect** APIs allow you to intercept and customize operations on objects. 🛡️🔍

#### 🔹 Proxy

A `Proxy` wraps an object and intercepts operations like property access, assignment, and function calls.

```js
const target = { name: "Alice" };

const handler = {
  get(obj, prop) {
    return prop in obj ? obj[prop] : "Property not found";
  },
};

const proxy = new Proxy(target, handler);

console.log(proxy.name); // Alice
console.log(proxy.age); // Property not found
```

- **Use Case**: Validating or logging property access, creating reactive objects.

#### 🔹 Reflect

The `Reflect` API provides methods for performing object operations, similar to those intercepted by `Proxy`.

```js
const obj = { name: "Alice" };

Reflect.set(obj, "age", 25);
console.log(Reflect.get(obj, "age")); // 25
```

- **Use Case**: Simplifying object operations and ensuring consistency with `Proxy`.

#### 🔹 Proxy and Reflect Together

You can use `Proxy` and `Reflect` together to customize and delegate operations.

```js
const target = { name: "Alice" };

const handler = {
  set(obj, prop, value) {
    if (prop === "age" && typeof value !== "number") {
      throw new TypeError("Age must be a number");
    }
    return Reflect.set(obj, prop, value);
  },
};

const proxy = new Proxy(target, handler);

proxy.age = 30; // Works
console.log(proxy.age); // 30

proxy.age = "thirty"; // ❌ Throws TypeError
```

[Back to Top](#)

---

### **Typed Arrays & Buffers**

Typed arrays and buffers provide a way to handle binary data in JavaScript. They are essential for working with raw data, such as files, streams, or Web APIs. 📦💾

#### 🔹 Typed Arrays

Typed arrays are array-like objects that provide a way to read and write binary data.

```js
const buffer = new ArrayBuffer(16); // Create a buffer of 16 bytes
const int32View = new Int32Array(buffer);

int32View[0] = 42;
console.log(int32View[0]); // 42
```

- **Use Case**: Handling binary data efficiently, such as in WebGL or file processing.

#### 🔹 DataView

A `DataView` provides a low-level interface for reading and writing multiple types of data in an `ArrayBuffer`.

```js
const buffer = new ArrayBuffer(16);
const view = new DataView(buffer);

view.setInt8(0, 127);
console.log(view.getInt8(0)); // 127
```

- **Use Case**: Reading and writing data with different types and endianness.

#### 🔹 Buffers in Node.js

In Node.js, `Buffer` is used to handle binary data.

```js
const buffer = Buffer.from("Hello, World!");
console.log(buffer.toString()); // Hello, World!
```

- **Use Case**: Working with file systems, streams, and network protocols.

#### 🧠 Summary

| Feature         | Purpose                          | Use Case                          |
|------------------|----------------------------------|------------------------------------|
| `ArrayBuffer`    | Fixed-length binary data buffer | Base for typed arrays and DataView|
| `Typed Arrays`   | Array-like views of binary data | Efficient binary data manipulation|
| `DataView`       | Flexible binary data access     | Mixed data types in a buffer      |
| `Buffer` (Node)  | Binary data in Node.js          | File systems, streams, networking |

[Back to Top](#)

---

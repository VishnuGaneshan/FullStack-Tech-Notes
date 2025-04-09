## ✅ **Basic Topics**

These are fundamentals every JavaScript developer must know:

- [What is JavaScript?](#what-is-javascript)
- [JS Engine & How it runs in the browser](#javascript-engine--how-it-runs-in-the-browser)
- Code Editors & Setup
- Variables (`var`, `let`, `const`)
- Data Types (Primitive & Non-Primitive)
- Operators
  - Arithmetic
  - Comparison
  - Logical
  - Assignment
  - Bitwise
  - Ternary
- Type Conversion & Coercion
- Conditionals (`if`, `else`, `switch`)
- Loops
  - `for`, `while`, `do...while`
  - `for...in`, `for...of`
- Functions
  - Declaration & Expressions
  - Parameters vs Arguments
  - Return Values
- Arrays
  - Declaration, Access, and Iteration
  - Basic Methods (`push`, `pop`, `shift`, `unshift`, `indexOf`)
- Objects
  - Key-Value Pairs
  - Dot & Bracket Notation
- Basic Debugging using `console.log`

---

> ### What is JavaScript?

JavaScript is a **high-level**, **interpreted**, **lightweight**, and **multi-paradigm** programming language that is one of the **core technologies of the web**, alongside HTML and CSS.  

It allows developers to build **interactive**, **dynamic**, and **responsive** user experiences in the browser, and also power **server-side applications** using environments like **Node.js**. 🚀🖥️💡

#### 📌 Key Characteristics:
- **Interpreted**: Runs directly in the browser (or in Node.js) without the need for compilation.
- **Dynamically typed**: You don’t need to define variable types explicitly.
- **Single-threaded**: Uses one call stack, but handles async tasks via the event loop.
- **Prototype-based**: Inheritance is done using prototypes instead of classical classes (though `class` syntax exists now).
- **Multi-paradigm**: Supports functional, procedural, and object-oriented programming styles.

#### 📜 A Brief History:
- Created in **1995** by **Brendan Eich** in just 10 days at Netscape.
- Originally called *Mocha*, then *LiveScript*, and finally *JavaScript* (for marketing reasons, not related to Java).
- Standardized as **ECMAScript (ES)**, with **ES6 (2015)** being the most influential modern update. 📅📘📈

#### 🌐 Where is JavaScript Used?
- **Client-side (Browser)**: DOM manipulation, form validation, UI interactivity.
- **Server-side**: Backend APIs with Node.js, Express.js, etc.
- **Mobile Apps**: Frameworks like React Native, Ionic.
- **Desktop Apps**: Electron-based apps like VSCode, Slack.
- **Game Development**: 2D/3D games using libraries like Phaser or Three.js.
- **IoT & Robotics**: With platforms like Johnny-Five.

#### 💬 Why Learn JavaScript?
- It’s the **only programming language** that natively runs in browsers.
- Massive **community**, endless **job opportunities**, and powerful **ecosystem**.
- Acts as a **gateway** to learning frontend frameworks (React, Vue, Angular) and full-stack development.

#### 🧪 Simple Example:
```js
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet("Vishnu")); // Output: Hello, Vishnu!
```

---

> ### **JavaScript Engine & How It Runs in the Browser**

JavaScript doesn’t work on its own — it needs a **JavaScript engine** to interpret and execute the code. Every modern browser comes with its own JS engine that runs your code behind the scenes.

Let’s break down how it works, from engine to execution. 🛠️🧩🔍

#### *🧠 What is a JavaScript Engine?*

A **JavaScript Engine** is a program that takes your JS code, parses it, optimizes it, and finally **executes it line by line**.  

Modern JS engines do much more than just interpretation — they **compile**, **optimize**, and **recompile** code to make it fast.

📌 Popular JS Engines:
- **V8** – Chrome, Edge, Node.js
- **SpiderMonkey** – Firefox
- **JavaScriptCore** – Safari
- **Chakra** – (Old) Microsoft Edge

#### 🧩 Main Components of a JS Engine

1. **Parser**: Breaks down your code into a syntax tree (AST – Abstract Syntax Tree).  
2. **Interpreter**: Quickly converts AST to bytecode and starts executing it.  
3. **Compiler (JIT)**: Just-In-Time compiler that takes frequently used code and compiles it into optimized machine code for faster execution.  
4. **Garbage Collector**: Automatically frees memory that's no longer needed.

🧪 Example Flow:  
`Your Code → Parser → AST → Bytecode → Optimized Machine Code`

#### 🌀 How JavaScript Runs in the Browser

JavaScript code runs **inside a browser’s environment**, where the JS engine is part of a bigger system including:

📦 **Web APIs**  
🧵 **Call Stack**  
📤 **Callback Queue**  
⏳ **Event Loop**

#### 📑 Execution Steps in the Browser:

1. **Load HTML → CSS → JS**  
   - The browser loads and parses the HTML.
   - If it hits a `<script>` tag, it pauses rendering and sends JS to the engine.

2. **Parsing & Compilation**  
   - JS engine parses the code into tokens and builds an AST.
   - Bytecode is generated and compiled by the JIT compiler if needed.

3. **Execution via Call Stack**  
   - Synchronous code runs immediately via the **call stack**.
   - Asynchronous operations (setTimeout, fetch) are sent to **Web APIs**.

4. **Asynchronous Handling**  
   - After completing, async tasks move to the **callback queue**.
   - The **event loop** checks if the call stack is empty, and then pushes callback tasks to be executed.

#### 🔁 Visual Simplification:

```text
JavaScript Code
   ↓
JavaScript Engine (V8)
   ↓
Parse → AST → Bytecode → Optimized Code
   ↓
Execution in Browser (Call Stack + Web APIs + Event Loop)
```

#### 💥 Key Takeaways:

- **JS Engine handles execution**, but the **browser provides the environment** (DOM, timers, fetch).
- Modern engines are blazing fast thanks to **JIT compilation** and **smart memory management**.
- The **event loop** enables JavaScript to be asynchronous even though it's single-threaded.

---
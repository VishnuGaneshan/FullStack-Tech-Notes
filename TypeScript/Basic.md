[Back to Typescript Home Page](./README.md#)

## ✅ **Basic Topics** ✨📘🧩

These topics cover the core syntax and features TypeScript adds to JavaScript:

- [What is TypeScript and Why Use It](#what-is-typescript-and-why-use-it)
- [Installing & Setting Up TypeScript](#installing--setting-up-typescript)
- [TypeScript Compiler (`tsc`) & Configuration (`tsconfig.json`)](#typescript-compiler-tsc--configuration-tsconfigjson)
- [Basic Types](#basic-types)
    - [`number`, `string`, `boolean`](#number-string-boolean)
    - [`any`, `unknown`, `void`, `null`, `undefined`, `never`](#any-unknown-void-null-undefined-never)
- [Type Annotations vs Type Inference](#type-annotations-vs-type-inference)
- [Arrays and Tuples](#arrays-and-tuples)
- [Enums](#enums)
- [Type Aliases](#type-aliases)
- [Union and Intersection Types](#union-and-intersection-types)
- [Literal Types](#literal-types)
- [`const` vs `let` with Types](#const-vs-let-with-types)

---

### **What is TypeScript and Why Use It**

**TypeScript** is a superset of JavaScript that adds **static typing** and other features to improve code quality and productivity.

#### 🔹 Why Use TypeScript?
- ✨ **Error Prevention**: Catches bugs during development.
- 📖 **Improved Readability**: Explicit types make code easier to understand.
- 🚀 **Modern Features**: Supports ES6+ features and compiles to older JavaScript.

```ts
function add(a: number, b: number): number {
  return a + b;
}

add(5, "10"); // ❌ Error: Argument of type 'string' is not assignable to parameter of type 'number'.
```

[Back to Top](#)

---

### **Installing & Setting Up TypeScript**

#### 🔹 Installation:
- 🛠️ Install TypeScript globally:
  ```bash
  npm install -g typescript
  ```

#### 🔹 Setting Up a Project:
1. 📂 **Initialize a project**:
   ```bash
   npm init -y
   ```
2. 📦 **Install TypeScript locally**:
   ```bash
   npm install --save-dev typescript
   ```
3. 📝 **Create a `tsconfig.json` file**:
   ```bash
   npx tsc --init
   ```

#### 🔹 Compiling TypeScript:
- 🔄 Compile `.ts` files to `.js`:
  ```bash
  npx tsc index.ts
  ```

[Back to Top](#)

---

### **TypeScript Compiler (`tsc`) & Configuration (`tsconfig.json`)**

The TypeScript compiler (`tsc`) converts TypeScript into JavaScript. The `tsconfig.json` file configures the compiler.

#### 🔹 Example `tsconfig.json`:
```json
{
  "compilerOptions": {
    "target": "ES6", // 🛠️ Specify JavaScript version
    "strict": true, // 🔒 Enable strict type checking
    "outDir": "./dist" // 📂 Output directory
  },
  "include": ["src/**/*"], // 📋 Files to include
  "exclude": ["node_modules"] // 🚫 Files to exclude
}
```

[Back to Top](#)

---

### **Basic Types**

#### 🔹 Common Types:
- 🔢 `number`, 📝 `string`, ✅ `boolean`:
  ```ts
  let age: number = 25;
  let name: string = "Alice";
  let isStudent: boolean = true;
  ```

#### 🔹 Special Types:
- 🌐 **`any`**: Allows any type (use sparingly).
  ```ts
  let value: any = 42;
  value = "Hello";
  ```
- 🔒 **`unknown`**: Safer alternative to `any`.
  ```ts
  let value: unknown = "Hello";
  if (typeof value === "string") console.log(value.toUpperCase());
  ```
- 🚫 **`void`**: For functions that don’t return a value.
  ```ts
  function logMessage(message: string): void {
    console.log(message);
  }
  ```
- ❌ **`never`**: For functions that never return.
  ```ts
  function throwError(message: string): never {
    throw new Error(message);
  }
  ```

[Back to Top](#)

---

### **Type Annotations vs Type Inference**

- 🖊️ **Type Annotations**: Explicitly specify types.
  ```ts
  let age: number = 25;
  ```
- 🔍 **Type Inference**: TypeScript infers the type.
  ```ts
  let age = 25; // Inferred as number
  ```

[Back to Top](#)

---

### **Arrays and Tuples**

- 📋 **Arrays**: Store multiple values of the same type.
  ```ts
  let numbers: number[] = [1, 2, 3];
  ```
- 🔗 **Tuples**: Fixed-length arrays with specific types.
  ```ts
  let person: [string, number] = ["Alice", 25];
  ```

[Back to Top](#)

---

### **Enums**

Enums define a set of named constants.

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

let move: Direction = Direction.Up;
console.log(move); // 0
```

[Back to Top](#)

---

### **Type Aliases**

Type aliases create custom types.

```ts
type Point = {
  x: number;
  y: number;
};

let point: Point = { x: 10, y: 20 };
```

[Back to Top](#)

---

### **Union and Intersection Types**

- 🔀 **Union Types**: A value can be one of several types.
  ```ts
  let value: string | number = "Hello";
  value = 42;
  ```
- 🔗 **Intersection Types**: Combine multiple types.
  ```ts
  type A = { a: number };
  type B = { b: string };
  type C = A & B;

  let obj: C = { a: 1, b: "Hello" };
  ```

[Back to Top](#)

---

### **Literal Types**

Literal types allow specific values as types.

```ts
let direction: "up" | "down" = "up";
```

[Back to Top](#)

---

### **`const` vs `let` with Types**

- 🔒 Use `const` for variables that won’t change:
  ```ts
  const name: string = "Alice";
  ```
- 🔄 Use `let` for variables that may change:
  ```ts
  let age: number = 25;
  age = 26;
  ```

[Back to Top](#)

---
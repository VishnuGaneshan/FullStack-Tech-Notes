[Back to Javascript Home Page](./README.md#)

## 🚀 **Intermediate Topics** 📦⚙️📚

These are essential to build scalable, maintainable, and clean applications:

- [Interfaces](#interfaces)
- [Optional & Readonly Properties](#optional--readonly-properties)
- [Functions](#functions)
  - [Function Types](#function-types)
  - [Optional and Default Parameters](#optional-and-default-parameters)
  - [Rest Parameters](#rest-parameters)
- [Type Assertions](#type-assertions)
- [Working with Objects](#working-with-objects)
- [Narrowing (Type Guards)](#narrowing-type-guards)
- [Type Compatibility](#type-compatibility)
- [Utility Types](#utility-types)
  - `Partial`, `Pick`, `Omit`, `Readonly`, etc.
- [Working with DOM and Event Handling in TS](#working-with-dom-and-event-handling-in-ts)
- [TypeScript with Classes & Inheritance](#typescript-with-classes--inheritance)
- [`this` in TypeScript Context](#this-in-typescript-context)

---

### **Interfaces**

Interfaces define the structure of an object, ensuring type safety.

```ts
interface User {
  name: string;
  age: number;
  isAdmin?: boolean; // Optional property
}

const user: User = { name: "Alice", age: 25 };
```

- **Use Case**: Enforcing consistent object shapes across your application.

[Back to Top](#)

---

### **Optional & Readonly Properties**

#### 🔹 Optional Properties:
Use `?` to mark properties as optional.

```ts
interface User {
  name: string;
  age?: number; // Optional
}

const user: User = { name: "Alice" }; // Valid
```

#### 🔹 Readonly Properties:
Use `readonly` to make properties immutable.

```ts
interface User {
  readonly id: number;
  name: string;
}

const user: User = { id: 1, name: "Alice" };
user.id = 2; // ❌ Error: Cannot assign to 'id' because it is a read-only property.
```

[Back to Top](#)

---

### **Functions**

#### 🔹 Function Types:
Define the shape of a function using types.

```ts
type Add = (a: number, b: number) => number;

const add: Add = (a, b) => a + b;
```

#### 🔹 Optional and Default Parameters:
- Optional parameters use `?`.
- Default parameters provide a fallback value.

```ts
function greet(name: string, age?: number): string {
  return `Hello, ${name}. Age: ${age ?? "unknown"}`;
}

function multiply(a: number, b: number = 2): number {
  return a * b;
}
```

#### 🔹 Rest Parameters:
Use `...` to handle multiple arguments.

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, num) => acc + num, 0);
}

console.log(sum(1, 2, 3)); // 6
```

[Back to Top](#)

---

### **Type Assertions**

Type assertions tell TypeScript to treat a value as a specific type.

```ts
let value: unknown = "Hello";
let strLength: number = (value as string).length;

console.log(strLength); // 5
```

- **Use Case**: When you know more about a value’s type than TypeScript does.

[Back to Top](#)

---

### **Working with Objects**

TypeScript allows you to define object types and access their properties safely.

```ts
type User = {
  name: string;
  age: number;
};

const user: User = { name: "Alice", age: 25 };
console.log(user.name); // Alice
```

- **Index Signatures**: Define dynamic property names.
  ```ts
  interface Dictionary {
    [key: string]: string;
  }

  const dict: Dictionary = { hello: "world" };
  ```

[Back to Top](#)

---

### **Narrowing (Type Guards)**

Type guards help narrow down types at runtime.

```ts
function printId(id: string | number): void {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(2));
  }
}
```

- **`instanceof`**: Check if an object is an instance of a class.
- **`in`**: Check if a property exists in an object.

[Back to Top](#)

---

### **Type Compatibility**

TypeScript uses structural typing, meaning types are compatible if their structures match.

```ts
interface Point {
  x: number;
  y: number;
}

const point: Point = { x: 10, y: 20 }; // Compatible
```

- **Use Case**: Ensures flexibility while maintaining type safety.

[Back to Top](#)

---

### **Utility Types**

Utility types simplify common type transformations.

#### 🔹 `Partial`:
Makes all properties optional.
```ts
type User = { name: string; age: number };
type PartialUser = Partial<User>;
```

#### 🔹 `Pick`:
Select specific properties.
```ts
type User = { name: string; age: number; isAdmin: boolean };
type Admin = Pick<User, "name" | "isAdmin">;
```

#### 🔹 `Omit`:
Exclude specific properties.
```ts
type User = { name: string; age: number; isAdmin: boolean };
type NonAdmin = Omit<User, "isAdmin">;
```

#### 🔹 `Readonly`:
Makes all properties readonly.
```ts
type ReadonlyUser = Readonly<User>;
```

[Back to Top](#)

---

### **Working with DOM and Event Handling in TS**

TypeScript provides type definitions for DOM elements and events.

```ts
const button = document.querySelector<HTMLButtonElement>("#myButton");

button?.addEventListener("click", (event: MouseEvent) => {
  console.log("Button clicked!");
});
```

- **Use Case**: Ensures type safety when interacting with the DOM.

[Back to Top](#)

---

### **TypeScript with Classes & Inheritance**

TypeScript enhances OOP with classes and inheritance.

```ts
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  greet(): void {
    console.log(`Hello, ${this.name}`);
  }
}

class Student extends Person {
  grade: number;

  constructor(name: string, grade: number) {
    super(name);
    this.grade = grade;
  }

  study(): void {
    console.log(`${this.name} is studying.`);
  }
}

const student = new Student("Alice", 10);
student.greet(); // Hello, Alice
student.study(); // Alice is studying.
```

[Back to Top](#)

---

### **`this` in TypeScript Context**

The value of `this` depends on the context in which a function is called.

#### 🔹 In Classes:
`this` refers to the current instance.

```ts
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  greet(): void {
    console.log(`Hello, ${this.name}`);
  }
}
```

#### 🔹 Arrow Functions:
Arrow functions don’t have their own `this`; they inherit it from the surrounding context.

```ts
class Counter {
  count = 0;

  increment = (): void => {
    console.log(this.count++);
  };
}

const counter = new Counter();
counter.increment(); // 0
counter.increment(); // 1
```

[Back to Top](#)

---
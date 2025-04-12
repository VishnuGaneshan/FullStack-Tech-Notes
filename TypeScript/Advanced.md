[Back to Javascript Home Page](./README.md#)

## 🧠 **Advanced Topics** 🧠💡📐

These take you deeper into mastering TypeScript’s type system and writing safe, complex applications:

- [Advanced Types](#advanced-types)
    - [Mapped Types](#🔹-mapped-types)
    - [Conditional Types](#🔹-conditional-types)
    - [Indexed Access Types](#🔹-indexed-access-types)
    - [Template Literal Types](#🔹-template-literal-types)
- [Generics](#generics)
    - [Generic Functions](#🔹-generic-functions)
    - [Generic Interfaces](#🔹-generic-interfaces)
    - [Generic Constraints](#🔹-generic-constraints)
- [Declaration Files (`.d.ts`)](#declaration-files-dts)
- [Modules and Namespaces](#modules-and-namespaces)
- [Type Operators: `keyof`, `typeof`, `in`, `infer`](#type-operators-keyof-typeof-in-infer)
- [Discriminated Unions](#discriminated-unions)
- [Recursive Types](#recursive-types)
- [Handling `this` in Different Contexts](#handling-this-in-different-contexts)
- [TypeScript with React (JSX/TSX & Props Typing)](#typescript-with-react-jsxtsx--props-typing)
- [Working with 3rd Party Libraries (`@types`)](#working-with-3rd-party-libraries-types)
- [Configuring `tsconfig.json` for Real-World Projects](#configuring-tsconfigjson-for-real-world-projects)
- [Type Checking vs Runtime Checking](#type-checking-vs-runtime-checking)
- [Best Practices & Clean Code with TypeScript](#best-practices--clean-code-with-typescript)

---

### **Advanced Types**

#### 🔹 Mapped Types
Mapped types transform existing types into new ones.

```ts
type User = {
  name: string;
  age: number;
};

type ReadonlyUser = {
  readonly [K in keyof User]: User[K];
};
```

- **Use Case**: Creating variations of existing types (e.g., `Readonly`, `Partial`).

#### 🔹 Conditional Types
Conditional types allow type logic based on conditions.

```ts
type IsString<T> = T extends string ? true : false;

type Test1 = IsString<string>; // true
type Test2 = IsString<number>; // false
```

- **Use Case**: Creating types that depend on other types.

#### 🔹 Indexed Access Types
Access a type’s properties using an index.

```ts
type User = { name: string; age: number };
type NameType = User["name"]; // string
```

- **Use Case**: Extracting specific property types.

#### 🔹 Template Literal Types
Combine string literals with types.

```ts
type Route = `/users/${string}`;
const route: Route = "/users/123"; // Valid
```

- **Use Case**: Defining dynamic string patterns.

[Back to Top](#)

---

### **Generics**

Generics provide a way to create reusable, type-safe components.

#### 🔹 Generic Functions
```ts
function identity<T>(value: T): T {
  return value;
}

const num = identity<number>(42);
const str = identity<string>("Hello");
```

- **Use Case**: Writing reusable functions with type safety.

#### 🔹 Generic Interfaces
```ts
interface Box<T> {
  value: T;
}

const box: Box<number> = { value: 42 };
```

- **Use Case**: Creating flexible data structures.

#### 🔹 Generic Constraints
Restrict the types that can be used with generics.

```ts
function getLength<T extends { length: number }>(item: T): number {
  return item.length;
}

getLength("Hello"); // 5
getLength([1, 2, 3]); // 3
```

- **Use Case**: Enforcing specific properties on generic types.

[Back to Top](#)

---

### **Declaration Files (`.d.ts`)**

Declaration files provide type definitions for JavaScript libraries.

#### 🔹 Example:
```ts
// math.d.ts
declare module "math" {
  export function add(a: number, b: number): number;
}
```

- **Use Case**: Adding type definitions for libraries without built-in TypeScript support.

[Back to Top](#)

---

### **Modules and Namespaces**

#### 🔹 Modules
Modules use `import` and `export` to organize code.

```ts
// utils.ts
export function greet(name: string): string {
  return `Hello, ${name}`;
}

// main.ts
import { greet } from "./utils";
console.log(greet("Alice"));
```

#### 🔹 Namespaces
Namespaces group related code under a single name.

```ts
namespace Utils {
  export function greet(name: string): string {
    return `Hello, ${name}`;
  }
}

console.log(Utils.greet("Alice"));
```

- **Use Case**: Namespaces are useful for organizing code in non-modular environments.

[Back to Top](#)

---

### **Type Operators: `keyof`, `typeof`, `in`, `infer`**

#### 🔹 `keyof`
Extracts the keys of a type.

```ts
type User = { name: string; age: number };
type UserKeys = keyof User; // "name" | "age"
```

#### 🔹 `typeof`
Gets the type of a value.

```ts
const user = { name: "Alice", age: 25 };
type UserType = typeof user; // { name: string; age: number }
```

#### 🔹 `in`
Iterates over keys in a type.

```ts
type ReadonlyUser = {
  [K in keyof User]: User[K];
};
```

#### 🔹 `infer`
Infers a type within a conditional type.

```ts
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Test = ReturnType<() => string>; // string
```

[Back to Top](#)

---

### **Discriminated Unions**

Discriminated unions simplify working with multiple object types.

```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number };

function getArea(shape: Shape): number {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
  } else {
    return shape.side ** 2;
  }
}
```

[Back to Top](#)

---

### **Recursive Types**

Recursive types allow types to reference themselves.

```ts
type NestedArray<T> = T | NestedArray<T>[];

const arr: NestedArray<number> = [1, [2, [3]]];
```

- **Use Case**: Defining deeply nested structures.

[Back to Top](#)

---

### **Handling `this` in Different Contexts**

TypeScript provides better control over `this`.

```ts
class Counter {
  count = 0;

  increment(this: Counter): void {
    this.count++;
  }
}

const counter = new Counter();
counter.increment();
```

- **Use Case**: Preventing incorrect `this` usage.

[Back to Top](#)

---

### **TypeScript with React (JSX/TSX & Props Typing)**

TypeScript enhances React development with type safety.

#### 🔹 Typing Props:
```tsx
type ButtonProps = {
  label: string;
  onClick: () => void;
};

const Button: React.FC<ButtonProps> = ({ label, onClick }) => (
  <button onClick={onClick}>{label}</button>
);
```

#### 🔹 Typing State:
```tsx
const [count, setCount] = React.useState<number>(0);
```

[Back to Top](#)

---

### **Working with 3rd Party Libraries (`@types`)**

Use `@types` packages for type definitions.

```bash
npm install --save-dev @types/lodash
```

```ts
import _ from "lodash";
_.chunk([1, 2, 3, 4], 2); // [[1, 2], [3, 4]]
```

[Back to Top](#)

---

### **Configuring `tsconfig.json` for Real-World Projects**

#### 🔹 Example Configuration:
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "strict": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "esModuleInterop": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

[Back to Top](#)

---

### **Type Checking vs Runtime Checking**

TypeScript performs type checking at compile time, but runtime errors can still occur.

#### 🔹 Example:
```ts
function divide(a: number, b: number): number {
  if (b === 0) throw new Error("Division by zero");
  return a / b;
}
```

- **Use Case**: Combine TypeScript with runtime checks for robust applications.

[Back to Top](#)

---

### **Best Practices & Clean Code with TypeScript**

1. **Enable Strict Mode**: Use `"strict": true` in `tsconfig.json`.
2. **Use Type Inference**: Let TypeScript infer types when possible.
3. **Avoid `any`**: Use `unknown` or proper types instead.
4. **Use Utility Types**: Simplify type transformations.
5. **Write Declaration Files**: Add types for external libraries.

[Back to Top](#)

---
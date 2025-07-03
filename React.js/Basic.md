[Back to ReactJs Home Page](./README.md#)

# ✅ Basic Topics 📗🧱✨
These topics are perfect for beginners getting started with React:

- ⚛️ [What is React? Why use React?](#what-is-react-why-use-react)
- 🛠️ Setting Up a React App:
    - 🚀 [Using Create React App (CRA)](#setting-up-a-react-app)
    - ⚡ [Using Vite](#setting-up-a-react-app)
- 📁 [Folder Structure Basics](#folder-structure-basics)
- ✨ [JSX Syntax](#jsx-syntax)
- 🧩 [Functional Components vs Class Components](#functional-components-vs-class-components)
- 🖼️ [Rendering Elements](#rendering-elements)
- 📦 [Props (Properties)](#props-properties)
- 🔄 [State in Functional Components (`useState`)](#state-in-functional-components-usestate)
- 🎯 [Event Handling](#event-handling)
- 🔀 [Conditional Rendering](#conditional-rendering)
- 📝 [Lists and Keys](#lists-and-keys)
- 🎨 [Basic Styling (Inline CSS, CSS Modules)](#basic-styling-inline-css-css-modules)

---

## **What is React? Why use React?**

React is a popular open-source JavaScript library developed by Facebook for building user interfaces, especially single-page applications (SPAs) where you need a fast, interactive user experience.

### What is React?
- 🧩 **Component-Based:** React lets you build encapsulated components that manage their own state, then compose them to make complex UIs.
- 📝 **Declarative:** You describe what you want the UI to look like, and React updates and renders the right components efficiently when your data changes.
- ⚡ **Virtual DOM:** React uses a virtual DOM to optimize updates, making UI changes fast and efficient.
- ➡️ **Unidirectional Data Flow:** Data flows in one direction, making it easier to understand and debug your app.

### Why Use React?
- ♻️ **Reusable Components:** Build small, reusable pieces of UI that can be shared and reused across your app.
- 🌐 **Large Ecosystem:** Huge community, lots of libraries, tools, and resources.
- 🚀 **Strong Performance:** Virtual DOM and efficient diffing algorithms make updates fast.
- 🧠 **Easy to Learn:** Simple API, especially for those familiar with JavaScript.
- 🏢 **Backed by Facebook:** Used in production by Facebook, Instagram, WhatsApp, and many others.
- 🔍 **SEO Friendly:** With tools like Next.js, React can be rendered on the server for better SEO.

### Example: Simple React Component
```jsx
import React from 'react';

function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Welcome;
```

### When Should You Use React?
- 🖥️ When building interactive UIs or SPAs.
- 🧩 When you want to break your UI into reusable components.
- 🌍 When you need a large ecosystem and community support.

[Back to Top](#)

---

## **Folder Structure Basics**

A well-organized folder structure makes your React project easier to scale, maintain, and collaborate on. Here’s a common and beginner-friendly structure for React apps:

```
my-react-app/
├── 📁 public/           # Static files (index.html, favicon, images)
├── 📁 src/              # All React code lives here
│   ├── 📁 components/   # Reusable UI components (Button, Navbar, etc.)
│   ├── 📁 pages/        # Page-level components (Home, About, etc.)
│   ├── 📁 assets/       # Images, fonts, and other static resources
│   ├── 📁 styles/       # CSS or SCSS files
│   ├── App.js          # Main app component
│   ├── index.js        # Entry point (renders App)
│   └── ...other files
├── package.json        # Project metadata & dependencies
└── README.md           # Project documentation
```

### Key Folders & Files
- 📁 **public/**: Contains static files. The main file is `index.html` where your React app is mounted.
- 📁 **src/**: All your JavaScript/JSX code, styles, and assets go here.
  - 📁 **components/**: Store small, reusable UI pieces (e.g., `Button.js`, `Navbar.js`).
  - 📁 **pages/**: Store components that represent full pages or routes (e.g., `Home.js`, `About.js`).
  - 📁 **assets/**: Images, fonts, icons, etc.
  - 📁 **styles/**: CSS, SCSS, or CSS Modules for styling your app.
  - 🗂️ **App.js**: The root component that holds your app’s structure.
  - 🗂️ **index.js**: The entry point that renders `<App />` into the DOM.
- 📦 **package.json**: Lists dependencies and scripts for your project.
- 📄 **README.md**: Project overview and instructions.

### Why Use This Structure?
- 🧩 **Separation of Concerns:** Keeps code modular and easy to find.
- 🔄 **Reusability:** Encourages building reusable components.
- 🛠️ **Scalability:** Makes it easier to add new features as your app grows.
- 👥 **Collaboration:** Team members can quickly understand and navigate the project.

### Example: Adding a New Component
Suppose you want to add a `Header` component:
1. 📝 Create `src/components/Header.js`:
   ```jsx
   import React from 'react';
   
   function Header() {
     return <header>Welcome to My App!</header>;
   }
   
   export default Header;
   ```
2. ➕ Import and use it in `App.js`:
   ```jsx
   import Header from './components/Header';
   
   function App() {
     return (
       <div>
         <Header />
         {/* other components */}
       </div>
     );
   }
   ```

[Back to Top](#)

---

## **JSX Syntax**

JSX (JavaScript XML) is a syntax extension for JavaScript recommended by React. It looks similar to HTML and is used to describe what the UI should look like.

### Why JSX?
- 📝 **Declarative:** Clearly describes the UI structure.
- 💡 **Expressive:** Mixes HTML-like tags with JavaScript, making it powerful and flexible.
- 🛡️ **Prevents Injection Attacks:** Escapes values embedded in JSX, helping to prevent XSS (Cross-Site Scripting) attacks.

### Basic Syntax
- 🏷️ **Elements:** `<div>`, `<span>`, `<h1>` are JSX elements.
- 🧩 **Components:** Custom components start with a capital letter, like `<MyComponent />`.
- 📝 **Attributes:** Use camelCase for attributes (e.g., `className` instead of `class`).
- 👶 **Children:** Elements can have children, which are passed between the opening and closing tags.

### Example
```jsx
const element = <h1 className="greeting">Hello, world!</h1>;
```

### Embedding Expressions
You can embed any JavaScript expression in JSX by wrapping it in curly braces `{}`.

#### Example
```jsx
const name = 'Alice';
const element = <h1>Hello, {name}!</h1>;
```

### JSX is Not HTML
JSX may look like HTML, but there are important differences:
- 🧮 **JavaScript Expressions:** You can use any JavaScript expression inside `{}`.
- 📝 **Attributes:** Use camelCase for attributes (e.g., `className` instead of `class`).
- 🎨 **Styling:** You can’t use CSS styles directly; you need to use `style` attribute with an object.

### Example: JavaScript Expression in JSX
```jsx
const user = { firstName: 'John', lastName: 'Doe' };
const element = <h1>Hello, {user.firstName} {user.lastName}!</h1>;
```

### Practical Tips
- 🧩 **Use Fragments:** Use `<>` and `</>` to group multiple elements without adding extra nodes to the DOM.
- ✂️ **Self-Closing Tags:** Use self-closing tags for elements without children, like `<img />` or `<br />`.

[Back to Top](#)

---

## **Functional Components vs Class Components**

In React, components can be defined as functions or classes. Understanding the difference is key to mastering React.

### Functional Components
- 🧩 **Definition:** JavaScript functions that return JSX.
- ✍️ **Syntax:** Can be written as regular functions or arrow functions.
- 🔄 **State & Lifecycle:** Use React hooks (e.g., `useState`, `useEffect`) for state and lifecycle management.

#### Lifecycle in Functional Components
React functional components use hooks to manage lifecycle events. The most common hook for lifecycle is `useEffect`.

- 🟢 **Mounting:** Code inside `useEffect` with an empty dependency array (`[]`) runs once after the component mounts (like `componentDidMount`).
- 🟡 **Updating:** Code inside `useEffect` with dependencies runs after those dependencies change (like `componentDidUpdate`).
- 🔴 **Unmounting:** Return a cleanup function from `useEffect` to run code when the component unmounts (like `componentWillUnmount`).

#### Example: useEffect Lifecycle
```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);

  // Mounting & Updating
  useEffect(() => {
    const timer = setInterval(() => setCount(c => c + 1), 1000);
    // Unmounting (cleanup)
    return () => clearInterval(timer);
  }, []); // [] = only on mount/unmount

  return <div>Timer: {count}</div>;
}
```

#### Common Hooks for Lifecycle
- 🪝 `useEffect`: Side effects, data fetching, subscriptions, cleanup.
- 🪝 `useLayoutEffect`: Like `useEffect` but fires synchronously after all DOM mutations.
- 🪝 `useRef`: Persist values across renders (like instance variables).

---

### Class Components
- 🏛️ **Definition:** ES6 classes that extend from `React.Component`.
- ✍️ **Syntax:** More boilerplate code, including `render()` method.
- 🔄 **State & Lifecycle:** Manage state and lifecycle methods (e.g., `componentDidMount`) directly.

#### Lifecycle Methods in Class Components
Class components have built-in lifecycle methods that are called at different stages:

- 🟢 **Mounting:**
  - 🏗️ `constructor()`
  - 🔄 `static getDerivedStateFromProps()`
  - 🖼️ `render()`
  - 🚦 `componentDidMount()`
- 🟡 **Updating:**
  - 🔄 `static getDerivedStateFromProps()`
  - 🔁 `shouldComponentUpdate()`
  - 🖼️ `render()`
  - 📝 `getSnapshotBeforeUpdate()`
  - 🔄 `componentDidUpdate()`
- 🔴 **Unmounting:**
  - 🧹 `componentWillUnmount()`
- ⚠️ **Error Handling:**
  - 🛑 `componentDidCatch()`
  - 🛑 `static getDerivedStateFromError()`

#### Example: Lifecycle Methods
```jsx
import React, { Component } from 'react';

class Timer extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    this.timer = setInterval(() => this.setState({ count: this.state.count + 1 }), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timer);
  }

  render() {
    return <div>Timer: {this.state.count}</div>;
  }
}
```

#### Summary Table: Lifecycle Comparison
| Phase         | Class Component Method         | Functional Component Hook         |
|---------------|-------------------------------|-----------------------------------|
| 🟢 Mount         | constructor, componentDidMount| useEffect(() => {...}, [])        |
| 🟡 Update        | componentDidUpdate            | useEffect(() => {...}, [deps])    |
| 🔴 Unmount       | componentWillUnmount          | useEffect(() => {... return ...}, []) |

### Practical Tips
- 🧩 **Prefer Functional Components:** Use hooks for lifecycle logic; they are more concise and flexible.
- 🛠️ **Class Components:** Still useful for legacy code or advanced error boundaries.
- 🔄 **Cleanup:** Always clean up subscriptions, timers, or listeners in `useEffect` or `componentWillUnmount`.

[Back to Top](#)

---

## **Rendering Elements**

Rendering elements is how React displays components on the screen. It’s a crucial concept to understand how your UI is updated and displayed.

### The Render Method
- 🖼️ **Definition:** A method that tells React what to display on the screen.
- 🛠️ **Usage:** Used in class components to return the JSX to be rendered.

#### Example: Render Method in Class Component
```jsx
class MyComponent extends React.Component {
  render() {
    return <h1>Hello, world!</h1>;
  }
}
```

### Rendering in Functional Components
Functional components return JSX directly, without a `render()` method.

#### Example: Rendering in Functional Component
```jsx
function MyComponent() {
  return <h1>Hello, world!</h1>;
}
```

### Updating the Rendered Output
React updates the rendered output when the component’s state or props change. It efficiently updates only the parts of the DOM that have changed.

#### Example: Updating Output
```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### The Virtual DOM
React uses a virtual DOM to optimize rendering. It keeps a lightweight copy of the actual DOM and updates it efficiently.

### Key Points
- 📝 **Declarative:** You describe what the UI should look like, and React takes care of updating the DOM.
- ⚡ **Efficient:** React minimizes direct manipulation of the DOM, leading to better performance.
- 🔄 **Automatic Updates:** The UI automatically updates when the component’s state or props change.

### Practical Tips
- ✂️ **Keep Render Methods Simple:** Don’t put too much logic in the render method; keep it focused on describing the UI.
- 🗝️ **Use Keys in Lists:** When rendering lists of elements, use unique keys to help React identify which items have changed.

[Back to Top](#)

---

## **Props (Properties)**

Props are how you pass data from parent to child components in React. They are essential for building dynamic and interactive UIs.

### What are Props?
- 🏷️ **Definition:** Short for "properties"; they are read-only attributes used to pass data and event handlers down to child components.
- 🚫 **Immutable:** Props are immutable from the child component’s perspective; they cannot be modified by the child.

### Passing Props
Props are passed to components similarly to HTML attributes.

#### Example: Passing Props
```jsx
<Welcome name="Alice" />
```

### Accessing Props
Props are accessible in the component’s `props` object.

#### Example: Accessing Props
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

### Default Props
You can define default values for your props using `defaultProps`.

#### Example: Default Props
```jsx
Welcome.defaultProps = {
  name: 'Guest',
};
```

### Prop Types
You can specify the types of props using `prop-types` package for better validation and documentation.

#### Example: Prop Types
```jsx
import PropTypes from 'prop-types';

Welcome.propTypes = {
  name: PropTypes.string,
};
```

### Practical Tips
- 🧩 **Use Destructuring:** Destructure props in the function parameters for cleaner code.
- 🪝 **Prop-Drilling:** Be aware of prop-drilling; passing props through many layers can make your code harder to maintain.

[Back to Top](#)

---

## **State in Functional Components (`useState`)**

State is a built-in object that allows components to create and manage their own local state. `useState` is a React hook that lets you add state to functional components.

### What is State?
- 🗂️ **Definition:** An object that determines how that component renders & behaves.
- 🏠 **Local:** Each component can have its own state, independent of other components.

### `useState` Hook
The `useState` hook is used to declare state variables in functional components.

#### Syntax
```jsx
const [stateVariable, setStateVariable] = useState(initialValue);
```

#### Example: Using `useState`
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### Updating State
- 🔄 **Functional Updates:** When the new state depends on the old state, use the functional form of the state setter.

#### Example: Functional Updates
```jsx
setCount(prevCount => prevCount + 1);
```

### State and Re-renders
Changing the state with the state setter function causes the component to re-render, reflecting the updated state in the UI.

### Practical Tips
- 🏁 **Initialize State:** Always initialize your state variables.
- 🔄 **Use Functional Updates:** Prefer functional updates when the new state depends on the old state.

[Back to Top](#)

---

## **Event Handling**

Event handling in React is how you manage events triggered by user interactions, like clicks, form submissions, and keyboard input.

### Synthetic Events
- 🧪 React wraps browser events in a synthetic event system to ensure consistency across different browsers.

### Adding Event Handlers
- 🖱️ Event handlers are passed as props to the components and are usually named using camelCase.

#### Example: Adding Event Handlers
```jsx
function MyButton() {
  function handleClick() {
    alert('Button was clicked!');
  }

  return <button onClick={handleClick}>Click me</button>;
}
```

### Event Handler Context
- ⚠️ **`this` Keyword:** In class components, you may need to bind the `this` keyword to the event handler to access the component instance.
- ➡️ **Arrow Functions:** Using arrow functions for event handlers automatically binds the correct `this` value.

#### Example: Binding `this`
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    alert('Button was clicked!');
  }

  render() {
    return <button onClick={this.handleClick}>Click me</button>;
  }
}
```

### Preventing Default Behavior
To prevent the default behavior of an event (like form submission), use the `preventDefault` method of the event object.

#### Example: Preventing Default
```jsx
function MyForm() {
  function handleSubmit(event) {
    event.preventDefault();
    alert('Form submitted!');
  }

  return <form onSubmit={handleSubmit}>...</form>;
}
```

### Practical Tips
- ➡️ **Use Arrow Functions:** Prefer arrow functions for event handlers to avoid binding issues.
- 🧹 **Keep Handlers Simple:** Keep your event handlers simple and delegate complex logic to other functions.

[Back to Top](#)

---

## **Conditional Rendering**

Conditional rendering in React allows you to render different UI elements or components based on certain conditions, like user authentication status or data availability.

### If-Else Conditions
- 🔀 Use JavaScript if-else conditions inside your component to decide what to render.

#### Example: If-Else Conditions
```jsx
function Greeting(props) {
  if (props.isLoggedIn) {
    return <h1>Welcome back!</h1>;
  } else {
    return <h1>Please sign in.</h1>;
  }
}
```

### Ternary Operator
- ⚖️ The ternary operator is a shorthand for if-else and is often used for conditional rendering.

#### Syntax
```jsx
condition ? <TrueComponent /> : <FalseComponent />;
```

#### Example: Ternary Operator
```jsx
function Greeting(props) {
  return props.isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign in.</h1>;
}
```

### Logical AND (`&&`) Operator
- ➕ The logical AND operator can be used to conditionally render a component if the condition is true.

#### Example: Logical AND Operator
```jsx
function LogoutButton(props) {
  return (
    <div>
      {props.isLoggedIn && <button onClick={props.onLogout}>Logout</button>}
    </div>
  );
}
```

### Practical Tips
- 🧹 **Keep It Simple:** Don’t overuse conditional rendering; keep your components simple and focused.
- ⚖️ **Use Ternary for Simple Conditions:** Use the ternary operator for simple if-else conditions to keep your code concise.

[Back to Top](#)

---

## **Lists and Keys**

Rendering lists of data and managing them with keys is a crucial part of building dynamic React applications.

### Rendering Lists
- 📝 You can render lists of elements by mapping over an array and returning a JSX element for each item.

#### Example: Rendering Lists
```jsx
const items = ['Apple', 'Banana', 'Cherry'];

function FruitList() {
  return (
    <ul>
      {items.map(item => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
}
```

### Keys
- 🗝️ Keys are special attributes you need to include when rendering lists of elements. They help React identify which items have changed, are added, or are removed.

#### Key Rules
- 🆔 **Unique:** Keys must be unique among siblings.
- 🔒 **Stable:** Keys should not change between renders.

#### Example: Using Keys
```jsx
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}
```

### Practical Tips
- 🗝️ **Always Use Keys in Lists:** Forgetting to use keys or using them incorrectly can lead to performance issues and bugs.
- 🆔 **Use Unique Identifiers:** Use unique and stable identifiers from your data as keys.

[Back to Top](#)

---

## **Basic Styling (Inline CSS, CSS Modules)**

Styling in React can be done in various ways, including inline CSS, CSS modules, and styled-components. This section covers the basics of inline CSS and CSS modules.

### Inline CSS
- 🎨 You can apply styles directly to elements using the `style` attribute. The value is a JavaScript object with camelCased properties.

#### Example: Inline CSS
```jsx
function MyComponent() {
  const divStyle = {
    color: 'blue',
    backgroundColor: 'lightgray',
    padding: '10px',
  };

  return <div style={divStyle}>Hello, world!</div>;
}
```

### CSS Modules
- 🗂️ CSS modules are a way to scope your CSS to a specific component, preventing clashes with other styles. Class names are locally scoped by default.

#### Example: CSS Modules
1. 📝 **Create a CSS Module:** `MyComponent.module.css`
   ```css
   .container {
     color: blue;
     background-color: lightgray;
     padding: 10px;
   }
   ```
2. ➕ **Import and Use It:**
   ```jsx
   import styles from './MyComponent.module.css';

   function MyComponent() {
     return <div className={styles.container}>Hello, world!</div>;
   }
   ```

### Practical Tips
- 🗂️ **Choose the Right Styling Method:** Choose a styling method that fits your project and team preferences.
- 🧩 **Keep Styles Organized:** Keep your styles organized and modular to avoid conflicts and make maintenance easier.

[Back to Top](#)

---
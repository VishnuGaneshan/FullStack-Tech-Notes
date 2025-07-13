[Back to ReactJs Home Page](./README.md#)

# 🚀 Intermediate Topics 📘🛠️🔁

Here you'll get into state management, component composition, and more real-world usage:

- 🛠️ [React Developer Tools](#react-developer-tools)
- 🔄 [useEffect Hook (side effects)](#useeffect-hook-side-effects)
- 🧲 [useRef Hook](#useref-hook)
- 🧮 [useMemo and useCallback](#usememo-and-usecallback)
- 🎛️ [Controlled vs Uncontrolled Components](#controlled-vs-uncontrolled-components)
- 📝 [Form Handling in React](#form-handling-in-react)
- ⬆️ [Lifting State Up](#lifting-state-up)
- 🧱 [Component Composition](#component-composition)
- 🛣️ [React Router Basics](#react-router-basics)
- 🛠️ [Custom Hooks](#custom-hooks)
- 🛡️ [Error Boundaries](#error-boundaries)
- 🌐 [Basic Context API](#basic-context-api)
- 🔗 [Working with APIs (Fetch/Axios)](#working-with-apis-fetchaxios)
- 🎬 [Basic Animations (Framer-motion-react-transition-group)](#basic-animations-framer-motion-react-transition-group)
- 🚀 [Deployment (Netlify, Vercel, etc.)](#deployment-netlify-vercel-etc)
---

## React Developer Tools
React Developer Tools is a browser extension for inspecting React component hierarchies, props, state, and hooks. It helps debug and optimize React apps.
- 🔍 Inspect components, props, and state in real time.
- 🧩 View component tree and relationships.
- 🪝 See hooks and their values.
- 🚦 Profile performance and detect unnecessary renders.

**Tip:** 💡 Install from Chrome/Firefox extension store and use the "⚛️ Components" and "Profiler" tabs.

---

## useEffect Hook (side effects)

The `useEffect` hook lets you perform side effects in functional components, such as data fetching, subscriptions, timers, and DOM updates. It is one of the most important hooks for managing component lifecycle in React.

### How useEffect Works
- 🟢 By default, `useEffect` runs after every render (mount and update).
- 🟡 You can control when it runs using the dependency array.
- 🔴 You can clean up effects to avoid memory leaks.

### Dependency Array Explained
The second argument to `useEffect` is the dependency array (`[dep1, dep2, ...]`). It determines when the effect runs:
- 🗂️ `[]` (empty array): Runs only once after the initial render (emulates `componentDidMount`).
- 🔁 `[dep1, dep2]`: Runs after initial render and whenever any dependency changes (emulates `componentDidUpdate`).
- ♻️ No array: Runs after every render (mount and update).

**Example: Different Dependency Patterns**
```jsx
// 🟢 Runs once on mount
useEffect(() => {
  console.log('Mounted!');
}, []);

// 🔁 Runs when 'count' changes
useEffect(() => {
  console.log('Count changed:', count);
}, [count]);

// ♻️ Runs after every render
useEffect(() => {
  console.log('Rendered!');
});
```

### Cleanup Function
Return a function from `useEffect` to clean up resources (emulates `componentWillUnmount`).

**Example: Timer Cleanup**
```jsx
useEffect(() => {
  const timer = setInterval(() => setCount(c => c + 1), 1000);
  return () => clearInterval(timer); // 🧹 Cleanup on unmount
}, []);
```

### Common useEffect Patterns
- 🛠️ Data fetching (API calls)
- 🧹 Subscriptions (WebSocket, event listeners)
- ⏰ Timers and intervals
- 🎨 DOM manipulation (focus, scroll)

### Best Practices
- ✅ Always specify dependencies to avoid bugs.
- 🧹 Always clean up subscriptions/timers.
- ⚠️ Avoid putting non-stable values (like objects/functions) in the dependency array unless memoized.
- 🧩 Use multiple `useEffect` hooks for unrelated side effects.

### Full Example: Data Fetching with useEffect
```jsx
import React, { useEffect, useState } from 'react';

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      });
  }, []); // 🟢 Only runs once on mount
  return (
    <div>
      {loading ? '⏳ Loading...' : (
        <ul>
          {users.map(user => <li key={user.id}>👤 {user.name}</li>)}
        </ul>
      )}
    </div>
  );
}
```

### Summary Table: useEffect Lifecycle Emulation
| Lifecycle Phase         | useEffect Pattern                |
|------------------------|----------------------------------|
| 🟢 Mount                  | `useEffect(() => {...}, [])`     |
| 🔁 Update (on deps)       | `useEffect(() => {...}, [deps])` |
| 🧹 Unmount                | `return () => {...}` in useEffect|

**Tip:** 💡 If you see unexpected behavior, check your dependency array!

[Back to Top](#)

---

## useRef Hook
`useRef` creates a mutable reference that persists across renders. Useful for accessing DOM nodes or storing values that don’t trigger re-renders.
- 🔗 Store values without causing re-renders.
- 🖱️ Access DOM elements directly.

**Example:**
```jsx
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(); // 🔗 Reference to input
  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>🖱️ Focus</button>
    </>
  );
}
```

---

## useMemo and useCallback
Optimize performance by memoizing values/functions so they don’t get recalculated/recreated on every render.
- 🧮 `useMemo`: Memoizes expensive calculations.
- 🪝 `useCallback`: Memoizes functions.

**Example:**
```jsx
import React, { useState, useMemo, useCallback } from 'react';

function ExpensiveComponent({ num }) {
  const squared = useMemo(() => num * num, [num]); // 🧮 Memoized value
  const handleClick = useCallback(() => alert(squared), [squared]); // 🪝 Memoized function
  return <button onClick={handleClick}>Show Square</button>;
}
```

[Back to Top](#)

---

## Controlled vs Uncontrolled Components
- 🎛️ **Controlled:** Form data managed by React state.
- 🗄️ **Uncontrolled:** Form data managed by the DOM (via refs).

**Controlled Example:**
```jsx
function ControlledInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={e => setValue(e.target.value)} />; // 🎛️ Controlled
}
```
**Uncontrolled Example:**
```jsx
function UncontrolledInput() {
  const inputRef = useRef();
  return <input ref={inputRef} />; // 🗄️ Uncontrolled
}
```

[Back to Top](#)

---

## Form Handling in React
React handles forms using state and event handlers.
- 🖊️ Use controlled components for form fields.
- 🧹 Validate and process input on submit.

**Example:**
```jsx
function SimpleForm() {
  const [name, setName] = useState('');
  const handleSubmit = e => {
    e.preventDefault();
    alert(`👋 Hello, ${name}!`);
  };
  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={e => setName(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

[Back to Top](#)

---

## Lifting State Up
Move state to a common ancestor to share data between components.
- 🔄 Enables sibling communication.
- 🧩 Keeps data consistent.

### Why Lift State Up?
- 📦 When two or more components need to share or synchronize data.
- 🔄 When you want to keep business logic in one place and pass data down as props.
- 🧹 To avoid prop-drilling through many layers.

### Common Use Cases
- ✅ Synchronizing form inputs (e.g., multiple fields updating a summary)
- ✅ Managing selected items in a list (e.g., highlight selected card)
- ✅ Parent-child communication (e.g., modal open/close state)
- ✅ Sibling communication (e.g., updating a counter from two buttons)

### Example: Sibling Communication
```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <ChildA count={count} />
      <ChildB increment={() => setCount(count + 1)} />
    </>
  );
}
function ChildA({ count }) {
  return <div>🔢 Count: {count}</div>;
}
function ChildB({ increment }) {
  return <button onClick={increment}>➕ Increment</button>;
}
```

[Back to Top](#)

---

## Component Composition
Build complex UIs by combining simple components.
- 🏗️ Use children props for flexible layouts.
- 🧱 Compose reusable building blocks.

**Example:**
```jsx
function Card({ children }) {
  return <div className="card">🧱 {children}</div>;
}
function App() {
  return (
    <Card>
      <h2>📝 Title</h2>
      <p>📦 Content goes here.</p>
    </Card>
  );
}
```

[Back to Top](#)

---

## React Router Basics
React Router enables navigation between pages in single-page apps.
- 🛣️ Define routes for different components.
- 🔗 Use `<Link>` for navigation.

### Key Components Explained
- **`<BrowserRouter>`**: 🗺️ The top-level component that enables routing in your app. It listens to URL changes and renders the correct components. Wrap your app with it to use React Router features.
  ```jsx
  <BrowserRouter>
    {/* All routing logic goes here */}
  </BrowserRouter>
  ```
- **`<Link>`**: 🔗 Used for navigation between routes. It renders an anchor tag (`<a>`) but prevents full page reloads, enabling client-side navigation.
  ```jsx
  <Link to="/about">Go to About</Link>
  ```
- **`<Routes>`**: 📦 A container for all your route definitions. It matches the current URL to a `<Route>` and renders the corresponding component.
  ```jsx
  <Routes>
    {/* Route definitions go here */}
  </Routes>
  ```
- **`<Route>`**: 🛤️ Defines a mapping between a URL path and a component. When the path matches the current URL, the component is rendered.
  ```jsx
  <Route path="/about" element={<About />} />
  ```

### Example: Putting It All Together
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';
function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">🏠 Home</Link>
        <Link to="/about">ℹ️ About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

[Back to Top](#)

---

## Custom Hooks
Create reusable logic by writing your own hooks.
- 🔄 Encapsulate stateful logic.
- 🧩 Share logic across components.

### Key Details About Custom Hooks
- 📝 **Naming Convention:** Custom hooks must start with "use" (e.g., `useCounter`, `useFetch`). This tells React to treat them as hooks and apply hook rules.
- 🧑‍💻 **Rules of Hooks:** Custom hooks can use other hooks (like `useState`, `useEffect`), but must only be called at the top level of a function component or another hook.
- 🧩 **Reusability:** Custom hooks let you extract and reuse logic across multiple components, keeping your code DRY and organized.
- 🛡️ **Isolation:** State and effects inside a custom hook are isolated to each component that uses it.
- 📦 **No JSX:** Custom hooks do not return JSX—they return values, functions, or objects.

### Best Practices
- ✅ Always start the name with "use".
- 🧩 Use custom hooks to share logic, not UI.
- 🧑‍💻 Keep hooks pure—avoid side effects outside of hooks.
- 🧹 Document what your hook does and what it returns.

**Example:**
```jsx
// 🔄 Custom hook for a counter
function useCounter(initial = 0) {
  const [count, setCount] = useState(initial);
  const increment = () => setCount(c => c + 1);
  return { count, increment };
}
function Counter() {
  const { count, increment } = useCounter();
  return <button onClick={increment}>Count: {count}</button>;
}
```

[Back to Top](#)

---

## Error Boundaries
Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the whole app.

### Why Use Error Boundaries?
- 🛡️ Prevent the entire app from crashing due to errors in part of the UI.
- 📝 Log errors for debugging and monitoring.
- 🎨 Show a user-friendly error message or recovery option.

### Limitations
- ❌ Error boundaries only catch errors in rendering, lifecycle methods, and constructors of child components.
- ❌ They do NOT catch errors in event handlers, async code, or server-side rendering.

### How to Use
1. 🏗️ Create a class component that implements `componentDidCatch` and `getDerivedStateFromError`.
2. 🧩 Wrap parts of your app with the error boundary.

### Annotated Example
```jsx
import React, { Component } from 'react';

// 🏗️ 1. Create the ErrorBoundary class
class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  // 🧩 2. Update state so the next render shows the fallback UI
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  // 📝 3. Log error details (optional)
  componentDidCatch(error, info) {
    console.error('Error caught by boundary:', error, info);
    // 🛠️ You can also send error info to a logging service here
  }

  render() {
    if (this.state.hasError) {
      // 🎨 4. Render fallback UI
      return <h1>❗ Something went wrong.</h1>;
    }
    // 5. Render children if no error
    return this.props.children;
  }
}

// Usage: 🧩 Wrap components that may throw errors
function App() {
  return (
    <ErrorBoundary>
      <ProblematicComponent />
    </ErrorBoundary>
  );
}
```

### Best Practices
- 🧩 Use error boundaries around parts of your app that may fail (e.g., widgets, third-party components).
- 📝 Customize the fallback UI for a better user experience.
- 🛠️ Log errors for monitoring and debugging.

### More Info
- ⚠️ Error boundaries do NOT catch errors in event handlers. Use try/catch in those cases.
- 🧩 You can nest multiple error boundaries for granular control.

[Back to Top](#)

---

## Basic Context API
The Context API is a React feature that allows you to share data (state, functions, etc.) across your component tree without passing props manually at every level (avoiding "prop drilling").

### Why Use Context?
- 🌍 Share global state (theme, user, language, etc.)
- 🔄 Avoid prop drilling through many layers
- 🧩 Make code more maintainable and readable

### How Context Works
1. 🏗️ **Create a Context:**
   ```jsx
   const MyContext = React.createContext(defaultValue);
   ```
2. 🧩 **Provide Context Value:** Wrap your component tree with a Provider and pass the value.
   ```jsx
   <MyContext.Provider value={value}>
     <ChildComponent />
   </MyContext.Provider>
   ```
3. 🧑‍💻 **Consume Context Value:** Use `useContext` (in functional components) or `MyContext.Consumer` (in class components).
   ```jsx
   const value = React.useContext(MyContext);
   ```

### Annotated Example: Theme Context
```jsx
// 🏗️ 1. Create the context
const ThemeContext = React.createContext('light');

// 🧩 2. Provide the context value
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return <ThemeButton />;
}

// 🧑‍💻 3. Consume the context value
function ThemeButton() {
  const theme = React.useContext(ThemeContext);
  return <button>Current theme: {theme}</button>;
}
```

### Common Use Cases
- 🌍 Theme switching (light/dark mode)
- 👤 User authentication state
- 🌐 Language/i18n settings
- 🛒 Shopping cart state

### Limitations
- ⚠️ Context is best for global state. For frequent updates or large apps, consider state management libraries (Redux, Zustand, etc.).
- ⚠️ Changing context value re-renders all consumers—use wisely for performance.

### Best Practices
- ✅ Use context for truly global data.
- 🧩 Split context into smaller pieces for different concerns (e.g., ThemeContext, UserContext).
- 🛠️ Memoize context value if it changes often.

[Back to Top](#)

---

## Working with APIs (Fetch/Axios)
Fetch data from APIs using `fetch` or `axios`.
- 🔄 Use `useEffect` for data fetching.
- 🧩 Store data in state.

### Example: Fetch API
```jsx
import React, { useEffect, useState } from 'react';
function UserList() {
  const [users, setUsers] = useState([]);
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(setUsers);
  }, []);
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>👤 {user.name}</li>
      ))}
    </ul>
  );
}
```

### Example: Axios
```jsx
import React, { useEffect, useState } from 'react';
import axios from 'axios';
function UserList() {
  const [users, setUsers] = useState([]);
  useEffect(() => {
    axios.get('https://jsonplaceholder.typicode.com/users')
      .then(res => setUsers(res.data));
  }, []);
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>👤 {user.name}</li>
      ))}
    </ul>
  );
}
```

### Fetch vs Axios
| Feature                | Fetch                         | Axios                       |
|------------------------|-------------------------------|-----------------------------|
| 📝 Syntax                 | Native JS, Promise-based      | Library, Promise-based      |
| 🗂️ JSON Parsing           | Manual (`res.json()`)         | Automatic (`res.data`)      |
| ⚠️ Error Handling         | Only network errors           | Handles HTTP errors         |
| 🔄 Request/Response Interceptors | No built-in support         | Built-in support           |
| 🌐 Browser Support        | Modern browsers               | Modern browsers & Node.js   |
| 📦 Upload/Download Progress| No built-in support           | Built-in support            |
| ❌ Cancel Requests        | Manual (AbortController)      | Built-in (CancelToken)      |
| 🛠️ Extra Features         | Minimal                       | Many (timeout, transform)   |

**Tip:** 💡 Use `fetch` for simple requests and when you want zero dependencies. Use `axios` for advanced features, better error handling, or Node.js support.

[Back to Top](#)

---

## Basic Animations (Framer Motion, React Transition Group)
Add animations for transitions and UI effects.
- 🎥 Use Framer Motion for declarative animations.
- 🔄 Use React Transition Group for managing component transitions.

**Framer Motion Example: Fade In**
```jsx
import { motion } from 'framer-motion';
function FadeIn() {
  return <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }}>🎬 Hello!</motion.div>;
}
```

**Framer Motion Example: Slide In**
```jsx
import { motion } from 'framer-motion';
function SlideIn() {
  return (
    <motion.div initial={{ x: -100 }} animate={{ x: 0 }} transition={{ duration: 0.5 }}>
      🚗 Slide In Animation
    </motion.div>
  );
}
```

**React Transition Group Example: Fade**
```jsx
import { CSSTransition } from 'react-transition-group';
import './fade.css';
function FadeComponent({ show }) {
  return (
    <CSSTransition in={show} timeout={300} classNames="fade" unmountOnExit>
      <div className="fade">🌫️ Fade Animation</div>
    </CSSTransition>
  );
}
```

**Tips:**
- 📚 Always refer to the official documentation for advanced usage and best practices:
  - Framer Motion: [https://www.framer.com/motion/](https://www.framer.com/motion/)
  - React Transition Group: [https://reactcommunity.org/react-transition-group/](https://reactcommunity.org/react-transition-group/)
- 🧩 Keep animations simple for performance and accessibility.
- 🛠️ Use CSS for basic transitions, and libraries for complex or interactive animations.

[Back to Top](#)

---

## Deployment (Netlify, Vercel, etc.)
Deploy React apps easily to cloud platforms.
- 🌍 Netlify, Vercel, GitHub Pages, etc.
- 🛠️ Push code to GitHub and connect to deployment platform.
- 🔄 Automatic builds and previews.

**Official Documentation Links:**
- 🌍 Netlify: [https://docs.netlify.com/configure-builds/get-started/](https://docs.netlify.com/configure-builds/get-started/)
- 🚀 Vercel: [https://vercel.com/docs/deployments/quickstart](https://vercel.com/docs/deployments/quickstart)
- 🗂️ GitHub Pages: [https://docs.github.com/en/pages/getting-started-with-github-pages](https://docs.github.com/en/pages/getting-started-with-github-pages)

**Tip:** 💡 Check platform docs for setup steps. Most platforms support drag-and-drop or Git integration for fast deployment.

[Back to Top](#)

---
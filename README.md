## 1. What is React?

React is an open-source JavaScript library developed by Meta (formerly Facebook) for building user interfaces, particularly single-page applications (SPAs).

React follows a component-based architecture, which means we divide an application into small, reusable pieces called components.

### Why do we use React?

- Component-based architecture.
- Reusability of UI components.
- Efficient UI updates.
- Declarative programming approach.
- Large ecosystem and community support.
- Easy integration with APIs and other libraries.

### Example

```jsx
function App() {
  return (
    <div>
      <h1>Welcome to React!</h1>
      <p>Let's learn React fundamentals.</p>
    </div>
  );
}

export default App;
```

## 2. What are JSX, Components, and Props?

### 2.1 What is JSX?

JSX stands for JavaScript XML. It is a syntax extension for JavaScript that allows us to write HTML-like code inside JavaScript.

**Without JSX:**

```jsx
const heading = React.createElement(
  "h1",
  null,
  "Hello React"
);
```

**With JSX:**

```jsx
const heading = <h1>Hello React</h1>;
```

Both approaches create a React element.

### Important JSX Rules

1. Every JSX element must have a closing tag.
2. Multiple elements must be wrapped inside a parent element or Fragment (`<> </>`).
3. Use `className` instead of `class`.
4. JavaScript expressions must be written inside curly braces `{}`.
5. Inline styles are passed as JavaScript objects.

**Example:**

```jsx
function App() {
  const name = "Prateek";

  return (
    <>
      <h1>Hello, {name}</h1>
      <p className="description">
        Learning React
      </p>
    </>
  );
}
```

### 2.2 What is a Component?

A component is an independent and reusable piece of UI.

React components are generally written as JavaScript functions.

**Example:**

```jsx
function Navbar() {
  return (
    <nav>
      <h2>My Website</h2>
    </nav>
  );
}

export default Navbar;
```

We can reuse this component inside another component:

```jsx
import Navbar from "./Navbar";

function App() {
  return (
    <div>
      <Navbar />
      <h1>Welcome to my website</h1>
    </div>
  );
}

export default App;
```

### 2.3 What are Props?

Props stands for properties. Props are used to pass data from a parent component to a child component.

**Parent Component:**

```jsx
function App() {
  return (
    <div>
      <JobCard
        title="Frontend Developer"
        company="Google"
      />

      <JobCard
        title="Backend Developer"
        company="Microsoft"
      />
    </div>
  );
}
```

**Child Component:**

```jsx
function JobCard({ title, company }) {
  return (
    <div>
      <h2>{title}</h2>
      <p>{company}</p>
    </div>
  );
}

export default JobCard;
```

**Important Points:**

- Props are passed from parent to child.
- Props are read-only.
- A child component should not directly modify its props.
- Props can contain strings, numbers, arrays, objects, functions, and React elements.

## 3. What is Babel, and what role does it play in React?

Babel is a JavaScript compiler that converts modern JavaScript syntax and JSX into JavaScript that browsers can understand.

Browsers do not directly understand JSX.

**Example JSX:**

```jsx
const element = <h1>Hello React</h1>;
```

**Transformed JavaScript (conceptual):**

```jsx
import { jsx } from "react/jsx-runtime";

const element = jsx("h1", {
  children: "Hello React"
});
```

### How Babel works

1. We write JSX inside React components.
2. Babel processes the JSX.
3. JSX is transformed into JavaScript function calls.
4. The browser executes the resulting JavaScript.

**Does Vite use Babel?**

Not necessarily. Vite commonly uses esbuild for fast JSX/TypeScript transformation and can use Babel through configured plugins. Babel is not required in every Vite React project.

## 4. What is the difference between Virtual DOM and Real DOM?

### 4.1 What is DOM?

DOM stands for Document Object Model.

It is a programming interface that represents an HTML document as a tree of objects.

**Example:**

```html
<html>
  <body>
    <h1>Hello</h1>
    <p>Welcome to React</p>
  </body>
</html>
```

JavaScript can interact with the DOM to modify HTML elements, attributes, and content.

```javascript
document.getElementById("heading").innerText =
  "Hello World";
```

### 4.2 What is Virtual DOM?

Virtual DOM is a lightweight, in-memory representation of the UI.

React uses its element tree and reconciliation process to determine what needs to change in the actual DOM.

Whenever state or props change:

1. React renders the component again to calculate the next UI description.
2. React compares the new result with the previous one.
3. React determines which changes are required.
4. React commits the necessary updates to the real DOM.

This process is known as reconciliation.

### Virtual DOM vs Real DOM

| Real DOM | Virtual DOM |
|---|---|
| Represents the actual document structure. | Represents the UI in memory. |
| Managed by the browser. | Managed by React's rendering system. |
| Direct DOM updates can trigger layout and rendering work. | Helps React calculate necessary DOM updates. |
| Contains actual DOM nodes. | Contains React element descriptions and related internal structures. |

**Important:** Virtual DOM does not mean every DOM update is automatically faster. Performance also depends on component structure, rendering work, and browser operations.

## 5. What is a Bundler?

A bundler is a development tool that combines multiple JavaScript files, CSS files, images, and other assets into optimized files that browsers can load efficiently.

### Responsibilities of a Bundler

1. Resolves module imports and dependencies.
2. Transforms JSX and modern JavaScript.
3. Processes CSS and other assets.
4. Optimizes code for production.
5. Minifies JavaScript and CSS.
6. Supports code splitting and hot module replacement.

### Popular Build Tools

- Vite
- Webpack
- Parcel
- Rollup
- Rsbuild

**Example:**

```javascript
// Navbar.js
export function Navbar() {
  return "Navbar";
}
```

```javascript
// Footer.js
export function Footer() {
  return "Footer";
}
```

```javascript
// App.js
import { Navbar } from "./Navbar";
import { Footer } from "./Footer";

console.log(Navbar(), Footer());
```

The build tool follows the imports, identifies dependencies, and prepares the application for the browser.

## 6. Why are we using Vite instead of Create React App?

Earlier, developers commonly used Create React App (CRA) to set up React projects.

However, Create React App was deprecated for new applications in February 2025.

### What is Vite?

Vite is a modern frontend build tool that provides a fast development environment and an optimized production build.

It provides two major capabilities:

- Development server: Starts the application and supports Hot Module Replacement (HMR).
- Production build: Bundles and optimizes the application for deployment.

### Vite vs Create React App

| Create React App | Vite |
|---|---|
| Uses Webpack internally. | Uses a modern development and build pipeline. |
| Generally slower startup for larger projects. | Fast development server startup. |
| Uses Webpack-based build tooling. | Uses Rolldown for production bundling in the current Vite toolchain. |
| Deprecated for new projects. | Actively developed. |
| Uses `npm start`. | Uses `npm run dev`. |

### What is Hot Module Replacement (HMR)?

HMR allows developers to update a module in the browser without refreshing the entire webpage.

For example, if we change the heading inside our Navbar component, Vite updates the affected module in the browser.

### Creating a React Project Using Vite

```bash
npm create vite@latest my-react-app
```

Select:

```text
Framework: React
Variant: JavaScript
```

Then execute:

```bash
cd my-react-app
npm install
npm run dev
```

The application usually starts at:

```text
http://localhost:5173
```

## 7. Understanding the React Project Folder Structure

When we create a React application using Vite, it generates a default folder structure.

### Folder Structure

```text
my-react-app/
│
├── node_modules/
│
├── public/
│   └── vite.svg
│
├── src/
│   ├── assets/
│   │   └── react.svg
│   │
│   ├── components/
│   │   └── Navbar.jsx
│   │
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
│
├── .gitignore
├── eslint.config.js
├── index.html
├── package.json
├── package-lock.json
└── vite.config.js
```

### 7.1 node_modules

This directory contains all installed dependencies and packages required by the application.

Examples:

- React
- React DOM
- Vite
- Axios
- React Router DOM
- Ant Design

We install dependencies using:

```bash
npm install
```

### 7.2 public

The public directory stores static assets that need to be served directly.

Examples:

- Images
- Favicon
- Static files
- Robots.txt

Example:

```text
public/
├── logo.png
└── favicon.ico
```

Access these files using:

```jsx
<img src="/logo.png" alt="Logo" />
```

### 7.3 src

The src directory contains most of our React application code.

It includes:

- Components
- Pages
- CSS files
- Hooks
- Context
- API-related logic
- Application state

### 7.4 App.jsx

This is usually the root application component.

It is where we compose other components and define the main UI structure.

```jsx
import Navbar from "./components/Navbar";

function App() {
  return (
    <div>
      <Navbar />
      <h1>Welcome to my application</h1>
    </div>
  );
}

export default App;
```

### 7.5 main.jsx

This is the entry point of the React application.

It connects the React application to the actual HTML document.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

import App from "./App";
import "./index.css";

ReactDOM.createRoot(
  document.getElementById("root")
).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

**How does it work?**

1. We import React and ReactDOM.
2. We import the root App component.
3. `document.getElementById("root")` selects the HTML element.
4. `createRoot()` creates a React root.
5. `.render()` renders the application inside that root.

### 7.6 index.html

This is the main HTML file of a Vite application.

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My React App</title>
  </head>

  <body>
    <div id="root"></div>

    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

React renders the application inside the `div` with the ID `root`.

### 7.7 package.json

This file contains project metadata, dependencies, and scripts.

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^19.0.0",
    "react-dom": "^19.0.0"
  },
  "devDependencies": {
    "vite": "^7.0.0"
  }
}
```

The versions above are illustrative.

| Command | Purpose |
|---|---|
| `npm run dev` | Starts development server |
| `npm run build` | Creates production build |
| `npm run preview` | Previews production build locally |
| `npm install` | Installs project dependencies |

### 7.8 vite.config.js

This file is used to configure Vite and its plugins.

```javascript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()]
});
```

## 8. Difference Between Class Components and Functional Components

React components can be written using two approaches:

1. Class Components
2. Functional Components

### 8.1 Class Components

Class components are JavaScript classes that extend `React.Component`.

They use a `render()` method to return JSX.

```jsx
import React from "react";

class Counter extends React.Component {

  constructor(props) {
    super(props);

    this.state = {
      count: 0
    };
  }

  increment = () => {
    this.setState({
      count: this.state.count + 1
    });
  };

  render() {
    return (
      <div>
        <h2>Count: {this.state.count}</h2>

        <button onClick={this.increment}>
          Increment
        </button>
      </div>
    );
  }
}

export default Counter;
```

### 8.2 Functional Components

Functional components are JavaScript functions that return JSX.

```jsx
import { useState } from "react";

function Counter() {

  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>

      <button
        onClick={() => setCount(count + 1)}
      >
        Increment
      </button>
    </div>
  );
}

export default Counter;
```

### Class Components vs Functional Components

| Class Components | Functional Components |
|---|---|
| Defined using JavaScript classes. | Defined using JavaScript functions. |
| Use `this.state` for state. | Use Hooks such as `useState`. |
| Use `this.setState()` to update state. | Use state setter functions. |
| Use lifecycle methods. | Use Hooks such as `useEffect`. |
| Require handling of `this` in certain situations. | No component-level `this` keyword. |
| More verbose. | Generally simpler and shorter. |

**Which approach should we use?**

Today, functional components with Hooks are the recommended approach for modern React applications.

Class components are still supported and may be encountered in older projects.

## 9. What are Hooks in React?

Hooks are special functions provided by React that allow functional components to use React features such as state, lifecycle-related behavior, context, and references.

Before Hooks were introduced in React 16.8, developers primarily used class components to manage state and lifecycle methods.

### Why do we use Hooks?

- To manage component state.
- To perform side effects.
- To access and manipulate DOM elements.
- To share reusable stateful logic.
- To manage context.

### Rules of Hooks

1. Only call Hooks at the top level of a React component or custom Hook.
2. Do not call Hooks inside loops, conditions, or nested functions.

**Correct:**

```jsx
function App() {
  const [count, setCount] = useState(0);

  return <h1>{count}</h1>;
}
```

**Incorrect:**

```jsx
function App() {

  if (true) {
    const [count, setCount] = useState(0);
  }

  return <h1>Hello</h1>;
}
```

## 10. useState Hook

`useState` is a React Hook used to create and manage state inside functional components.

State is data that can change over time and influence what the component displays.

### Syntax

```jsx
const [state, setState] = useState(initialValue);
```

It returns two things:

1. Current state value.
2. A function to update that state.

### Example: Counter Application

```jsx
import { useState } from "react";

function Counter() {

  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  const decrement = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h2>Count: {count}</h2>

      <button onClick={increment}>
        Increment
      </button>

      <button onClick={decrement}>
        Decrement
      </button>
    </div>
  );
}

export default Counter;
```

### How does it work?

1. Initially, `count` is set to `0`.
2. When we click Increment, `setCount()` requests a state update.
3. React renders the component again with the updated value.
4. The updated count is displayed on the screen.

### Updating State Using a Callback Function

Sometimes, the new state depends on the previous state.

In such situations, use the functional updater form.

```jsx
setCount((prevCount) => prevCount + 1);
```

### Updating Object State

```jsx
const [user, setUser] = useState({
  name: "Prateek",
  age: 22
});

function updateAge() {
  setUser((prevUser) => ({
    ...prevUser,
    age: prevUser.age + 1
  }));
}
```

We use the spread operator to preserve existing properties while updating the age.

**Important:** React state should be treated as immutable. Instead of directly modifying existing arrays or objects, create new ones.

## 11. useEffect Hook

`useEffect` is a React Hook used to synchronize a component with external systems.

Examples include:

- Fetching data from APIs.
- Adding event listeners.
- Setting up subscriptions.
- Working with timers.
- Synchronizing with browser APIs.

### Syntax

```jsx
useEffect(() => {
  // Side effect logic

  return () => {
    // Cleanup logic
  };
}, [dependencies]);
```

### Case 1: No Dependency Array

```jsx
useEffect(() => {
  console.log("Effect executed");
});
```

The Effect runs after every commit where the component renders.

### Case 2: Empty Dependency Array

```jsx
useEffect(() => {
  console.log("Component mounted");
}, []);
```

The Effect runs after the initial commit in production.

### Case 3: Dependency Array with Values

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

The Effect runs after the initial commit and again when `count` changes.

### Practical Example: Fetching API Data

```jsx
import { useEffect, useState } from "react";

function Users() {

  const [users, setUsers] = useState([]);

  useEffect(() => {

    const fetchUsers = async () => {

      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );

        const data = await response.json();

        setUsers(data);

      } catch (error) {
        console.error("Error:", error);
      }
    };

    fetchUsers();

  }, []);

  return (
    <div>
      <h2>Users</h2>

      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default Users;
```

### Cleanup Function in useEffect

Sometimes we create resources that must be cleaned up when a component is removed or before an Effect re-synchronizes.

**Example: Timer**

```jsx
import { useEffect, useState } from "react";

function Timer() {

  const [seconds, setSeconds] = useState(0);

  useEffect(() => {

    const intervalId = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => {
      clearInterval(intervalId);
    };

  }, []);

  return <h2>Timer: {seconds}</h2>;
}

export default Timer;
```

The cleanup function clears the interval and prevents it from continuing after the component is removed.

**Important:** `useEffect` is not required for every operation. Responding to a button click should generally be handled directly in the event handler.

## 12. useRef Hook

`useRef` is a React Hook that allows us to store a mutable value that persists between renders without triggering a re-render when its value changes.

It is commonly used for:

1. Accessing DOM elements directly.
2. Storing values that should persist between renders.
3. Storing timer IDs.
4. Keeping track of previous values.

### Syntax

```jsx
const ref = useRef(initialValue);
```

A ref returns an object containing a `current` property.

```javascript
ref.current
```

### Example 1: Accessing DOM Elements

Suppose we want to automatically focus an input field when a user clicks a button.

```jsx
import { useRef } from "react";

function InputFocus() {

  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input
        ref={inputRef}
        type="text"
        placeholder="Enter your name"
      />

      <button onClick={handleFocus}>
        Focus Input
      </button>
    </div>
  );
}

export default InputFocus;
```

**How does it work?**

1. `useRef(null)` creates a reference.
2. We attach that reference to the input using `ref={inputRef}`.
3. React assigns the actual DOM input element to `inputRef.current`.
4. When the button is clicked, `inputRef.current.focus()` focuses the input.

### Example 2: Storing a Value Without Re-rendering

```jsx
import { useRef, useState } from "react";

function Counter() {

  const [count, setCount] = useState(0);

  const renderCount = useRef(0);

  renderCount.current += 1;

  return (
    <div>
      <h2>Count: {count}</h2>

      <h3>Render Count: {renderCount.current}</h3>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

Changing `renderCount.current` does not trigger a re-render. Changing `count` does trigger a re-render.

### useState vs useRef

| useState | useRef |
|---|---|
| Stores component state. | Stores a mutable reference. |
| Updating it triggers a re-render. | Updating `.current` does not trigger a re-render. |
| Used for data displayed in UI. | Used for DOM access and values that don't need to trigger rendering. |

**Remember:** Do not use `useRef` as a replacement for `useState` when the changed value needs to update the UI.

## 13. How to Pass Data from One Component to Another?

React applications consist of multiple components, and these components often need to communicate with each other.

The most common ways to share data include:

1. Parent to Child – Props.
2. Child to Parent – Callback functions passed through props.
3. Between siblings – Lifting state up.
4. Across deeply nested components – Context API.

### 13.1 Parent to Child Communication

We use props to pass data from a parent component to a child component.

**Parent.jsx**

```jsx
import Child from "./Child";

function Parent() {

  const username = "Prateek";

  return (
    <div>
      <Child name={username} />
    </div>
  );
}

export default Parent;
```

**Child.jsx**

```jsx
function Child({ name }) {

  return (
    <h2>Welcome, {name}</h2>
  );
}

export default Child;
```

**Output:**

```text
Welcome, Prateek
```

### 13.2 Child to Parent Communication

We pass a function from the parent to the child. The child calls that function and sends data as an argument.

**Parent.jsx**

```jsx
import Child from "./Child";

function Parent() {

  const handleMessage = (message) => {
    console.log(message);
  };

  return (
    <Child sendMessage={handleMessage} />
  );
}

export default Parent;
```

**Child.jsx**

```jsx
function Child({ sendMessage }) {

  const handleClick = () => {
    sendMessage("Hello from Child!");
  };

  return (
    <button onClick={handleClick}>
      Send Message
    </button>
  );
}

export default Child;
```

This is commonly called callback-based communication.

### 13.3 Sibling Component Communication

Suppose we have two sibling components:

- Component A
- Component B

Both need access to the same data.

A common solution is to store the shared state in their common parent and pass the necessary values and functions through props.

## 14. What is Lifting State Up?

Lifting state up means moving state from a child component to its nearest common parent component so that multiple child components can share and update the same data.

Suppose we have two components:

- InputComponent – Accepts a username.
- DisplayComponent – Displays the username.

Instead of maintaining separate state in both components, we maintain the state in their common parent.

### Example

**App.jsx (Parent Component)**

```jsx
import { useState } from "react";
import InputComponent from "./InputComponent";
import DisplayComponent from "./DisplayComponent";

function App() {

  const [name, setName] = useState("");

  return (
    <div>
      <InputComponent
        name={name}
        setName={setName}
      />

      <DisplayComponent name={name} />
    </div>
  );
}

export default App;
```

**InputComponent.jsx**

```jsx
function InputComponent({ name, setName }) {

  return (
    <input
      type="text"
      value={name}
      onChange={(e) => setName(e.target.value)}
      placeholder="Enter your name"
    />
  );
}

export default InputComponent;
```

**DisplayComponent.jsx**

```jsx
function DisplayComponent({ name }) {

  return (
    <h2>Welcome, {name}</h2>
  );
}

export default DisplayComponent;
```

### How Does It Work?

1. The parent component creates the state using `useState`.
2. The parent passes `name` and `setName` to InputComponent.
3. When the user enters text, InputComponent calls `setName`.
4. The parent state gets updated.
5. React re-renders the parent and its relevant child components.
6. DisplayComponent receives the updated name through props.

### Why is Lifting State Up Important?

- Maintains a single source of truth.
- Avoids duplicate state.
- Keeps sibling components synchronized.
- Makes data flow predictable.

## 15. How to Use Event Listeners in React Components?

Event listeners allow us to respond to user interactions such as:

- Clicking a button.
- Typing in an input field.
- Submitting a form.
- Hovering over an element.
- Pressing keyboard keys.

React provides event props that let us handle these interactions directly in JSX.

### 15.1 Click Event

In React, we use `onClick` instead of traditional HTML `onclick`.

```jsx
function App() {

  const handleClick = () => {
    alert("Button clicked!");
  };

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}

export default App;
```

We pass the function reference instead of calling the function immediately.

**Incorrect:**

```jsx
<button onClick={handleClick()}>
  Click Me
</button>
```

### 15.2 Input Event

We can use `onChange` to handle input changes.

```jsx
import { useState } from "react";

function App() {

  const [name, setName] = useState("");

  const handleChange = (event) => {
    setName(event.target.value);
  };

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={handleChange}
        placeholder="Enter your name"
      />

      <h2>{name}</h2>
    </div>
  );
}

export default App;
```

Here:

- `event` represents the React event.
- `event.target` refers to the input element.
- `event.target.value` gives us the current input value.

### 15.3 Form Submission Event

```jsx
function LoginForm() {

  const handleSubmit = (event) => {

    event.preventDefault();

    console.log("Form submitted!");
  };

  return (
    <form onSubmit={handleSubmit}>

      <input
        type="email"
        placeholder="Enter email"
      />

      <button type="submit">
        Submit
      </button>

    </form>
  );
}

export default LoginForm;
```

**What is preventDefault()?**

By default, submitting an HTML form can trigger browser navigation or a page reload.

`event.preventDefault()` prevents that default browser behavior, allowing us to handle submission using React.

### 15.4 Keyboard Event

We can use `onKeyDown` to detect keyboard interactions.

```jsx
function App() {

  const handleKeyDown = (event) => {

    if (event.key === "Enter") {
      console.log("Enter key pressed!");
    }
  };

  return (
    <input
      type="text"
      onKeyDown={handleKeyDown}
      placeholder="Press Enter"
    />
  );
}

export default App;
```

### 15.5 Adding Event Listeners Using useEffect

Sometimes we need to attach native browser event listeners to the window or document.

For example, detecting when a user presses a key anywhere on the webpage.

We can use `useEffect` to add and remove the listener.

```jsx
import { useEffect } from "react";

function App() {

  useEffect(() => {

    const handleKeyDown = (event) => {
      console.log("Key pressed:", event.key);
    };

    window.addEventListener(
      "keydown",
      handleKeyDown
    );

    return () => {
      window.removeEventListener(
        "keydown",
        handleKeyDown
      );
    };

  }, []);

  return <h1>Press any key</h1>;
}

export default App;
```

**Why do we use cleanup here?**

Whenever we attach a native event listener, we should remove it when it is no longer needed.

Otherwise, we may end up with unnecessary listeners or duplicate event handling.

### React Event Handlers vs Native Event Listeners

| React Event Handlers | Native Event Listeners |
|---|---|
| Written directly in JSX. | Added using `addEventListener()`. |
| Example: `onClick`. | Example: `window.addEventListener()`. |
| React manages their lifecycle. | Developer manages attachment and cleanup. |
| Suitable for normal UI interactions. | Suitable for global or external DOM events. |

For normal button clicks, input changes, and form submissions, prefer React event handlers.

## Conclusion

React is built around a few fundamental ideas: components, props, state, and one-way data flow.

Understanding these concepts will help you develop a strong foundation before moving towards more advanced topics such as:

- React Router and nested routing.
- Context API.
- Custom Hooks.
- State management libraries.
- API integration using Axios.
- Performance optimization.
- React application architecture.

The most important thing is to understand how data flows between components and how state updates affect the UI. Once these concepts become clear, building larger applications becomes much easier.


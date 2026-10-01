ReactJS(React) is an open-source JavaScript library used for building user interfaces, especially for web application. React was created by **Jordan Walke**, a Facebook software engineer and is primarily used for building the frontend of modern web applications.

The main idea behind React is to build a UI by combining small, reusable pieces called components. React was developed to make UI development more **declarative, component-based, and easier to manage**.

**The main ideas behind React were:**

1. **Component-based development**
    - Break the UI into small, reusable components.
2. **Declarative UI**
    - Describe what the UI should look like for a given state.
    - React handles the necessary DOM updates.
3. **Efficient UI updates**
    - React uses a reconciliation process to determine what needs to change in the UI.
4. **Reusable code**
    - Components can be reused throughout an application.
5. **Better management of complex UIs**
    - Keep UI logic organized as applications grow.
    

### **Why is Component-Based UI Important?**

A large UI can become difficult to manage when everything is written in one place.

Components break the UI into **small, independent, reusable pieces**, making the code easier to understand and maintain.

They also reduce **code duplication** and make debugging and teamwork easier.

For example, instead of repeating a product UI 100 times, we create one `ProductCard` component and reuse it.

### **What do we need before creating a React project?**

**Requirement:**

- Node.js (allows us to run JS outside the browser)
- Node Package Manager (npm) — allows us to install packages, manage dependencies, run proect scripts, execute development/build tools

Now, React need a **build tool** which helps us to develop and prepare a web application. Popularbuild tools are Vite, Parcel, Rsbuild.

We normally write React like this:

function App() {
  return <h1>Hello React</h1>;
}

This is **JSX**. JSX needs to be transformed into JavaScript that the browser can execute.

A build setup handles transformations like this as part of the development/build process.

A build tool can also provide a development server. 

Instead of opening: file:///C:/project/index.html

we run : npm run dev and get something like http://localhost:5173

The development server watches our files and server the application while we work.

One of the useful features provided by Vite is **Hot Module Replacement (HMR)**.

Suppose we have:

<h1>Hello React</h1>

We change it to:

<h1>Hello World</h1>

and save the file.

Vite can update the relevant part of the application without requiring a full manual page reload. Vite describes this as one of its core development features.

### **Why Vite?**

**Vite** is a frontend build tool designed to provide a fast development experience.

It provides:

- Development server
- Fast HMR
- Dependency handling
- JSX/React integration
- Production builds
- Plugin support
- Sensible defaults

Vite's current architecture uses **Rolldown** for production builds.

## Methods to create React Project

### Method 1 — create React App with Vite

**Step 1** : Create the project using cmd “npm create vite@latest”. Vite will ask questions like project name, framework, variant  or directly use cmd “npm create vite@latest my-react-app — —template react”

**Step 2** : cd my-react-app

**Step 3** : Install Dependencies using cmd “npm install”

**Step 4** : Start the Development Server

### **Method 2 — using Vite and Typescript**

use cmd “npm create vite@latest my-react-app — —template react-ts”

then cd my-react-app —> npm install —> npm run dev

### **Method 3 — Use a React Framework**

if Next.js : “npx create-next-app@latest”

if React Router : “npx create-react-router@latest”

### **Method 4 — Try React without Installing Anything**

If you only want to experiment with React, you don't necessarily need to create a local project.

React's documentation provides online sandboxes, and platforms such as CodeSandbox and StackBlitz can run React projects in the browser.

### **Method 5 — Manual React Setup**

You can also create a React application from scratch manually.

For example, you could install Vite yourself : “npm install -D vite”. Then configure the project yourself.

This teaches you what the tooling is doing, but it requires more configuration.React's documentation explicitly describes this as a "build a React app from scratch" approach and lists Vite, Parcel, and Rsbuild as possible build tools.

## **React ES6**

**Definition:**

ES6 (ECMAScript 2015) is a modern version of JavaScript that provides features commonly used in React, such as classes, arrow functions, **`let`**, **`const`**, destructuring, spread operators, modules, and template strings.

**Syntax:**

```jsx
const variable = value;
```

**Example:**

```jsx
const name = "John";

function App() {
  return <h1>Hello {name}</h1>;
}
```

## **ES6 Classes**

**Definition:**

Classes are templates for creating objects and defining their properties and methods.

**Syntax:**

```jsx
class ClassName {
  constructor() {
    // properties
  }

  method() {
    // code
  }
}
```

**Example:**

```jsx
class Person {
  constructor(name) {
    this.name= name;
  }

  greet() {
    return `Hello${this.name}`;
  }
}

const person = new Person("John");
console.log(person.greet());
```

## **ES6 Arrow Function**

**Definition:**

Arrow functions provide a shorter syntax for writing functions.

**Syntax:**

```jsx
const functionName = (parameters)=> {
  // code
};
```

**Example:**

```jsx
const add = (a, b)=> {
  return a+ b;
};

console.log(add(2, 3));
```

## **ES6 Variables**

**Definition:**

ES6 provides **`let`** and **`const`** for declaring variables.

**Syntax:**

```jsx
let variableName= value;
const variableName = value;
```

**Example:**

```jsx
let age= 20;
age= 21;

const name = "John";
```

## **ES6 Array `map()`**

**Definition:**

**`map()`** creates a new array by applying a function to every element of an array.

**Syntax:**

```jsx
array.map((element)=> {
  return newValue;
});
```

**Example:**

```jsx
const numbers = [1, 2, 3];

const doubled = numbers.map((number)=> {
  return number* 2;
});

console.log(doubled);
// [2, 4, 6]
```

## **ES6 Destructuring**

**Definition:**

Destructuring extracts values from arrays or properties from objects into variables.

**Syntax:**

```jsx
const {property1, property2 }= object;

const [value1, value2]= array;
```

**Example:**

```jsx
const person = {
  name: "John",
  age: 25
};

const {name, age }= person;

console.log(name);
console.log(age);
```

## **ES6 Spread Operator**

**Definition:**

The spread operator **`...`** expands the elements of an array or the properties of an object.

**Syntax:**

```jsx
const newArray = [...oldArray];

const newObject = {...oldObject };
```

**Example:**

```jsx
const numbers = [1, 2, 3];

const newNumbers = [...numbers, 4, 5];

console.log(newNumbers);
// [1, 2, 3, 4, 5]
```

## **ES6 Modules**

**Definition:**

Modules allow JavaScript code to be separated into different files and reused using **`export`** and **`import`**.

**Syntax:**

```jsx
// Export
export default value;

// Import
import valuefrom "./file";
```

**Example:**

```jsx
// App.js
export default function App() {
  return <h1>Hello React</h1>;
}
```

```jsx
// main.js
import Appfrom "./App";
```

## **ES6 Ternary Operator**

**Definition:**

The ternary operator is a short way to write an **`if...else`** condition.

**Syntax:**

```jsx
condition? valueIfTrue: valueIfFalse;
```

**Example:**

```jsx
const age = 20;

const result = age>= 18 ? "Adult" : "Minor";

console.log(result);
// Adult
```

## **ES6 Template String**

**Definition:**

Template strings allow strings to contain variables and expressions using backticks **```** and **`${}`**.

**Syntax:**

```jsx
`Text${expression}`
```

**Example:**

```jsx
const name = "John";
const age = 25;

const message = `My name is${name} and I am${age} years old.`;

console.log(message);
```

## **React JSX Intro**

**Definition:**

JSX is a syntax extension that allows HTML-like code to be written inside JavaScript.

**Syntax:**

```jsx
const element = <h1>Hello World</h1>;
```

**Example:**

```jsx
function App() {
  return <h1>Hello React</h1>;
}
```

---

## **2. React JSX Expressions**

**Definition:**

JSX expressions allow JavaScript values, variables, and expressions to be written inside **`{}`**.

**Syntax:**

```jsx
{expression}
```

**Example:**

```jsx
function App() {
  const name = "John";
  const age = 20;

  return (
    <div>
      <h1>Hello {name}</h1>
      <p>Age: {age}</p>
      <p>{age >= 18 ? "Adult" : "Minor"}</p>
    </div>
  );
}
```

---

## **3. React JSX Attributes**

**Definition:**

JSX attributes are used to provide properties or values to HTML elements and React components.

### **Types**

### **A. String Attribute**

**Syntax:**

```jsx
<element attribute="value" />
```

**Example:**

```jsx
<img src="image.jpg" alt="Profile" />
```

### **B. JavaScript Expression Attribute**

**Syntax:**

```jsx
<element attribute={expression} />
```

**Example:**

```jsx
const image = "profile.jpg";

<img src={image} alt="Profile" />
```

### **C. `className`**

**Syntax:**

```jsx
<element className="class-name" />
```

**Example:**

```jsx
<div className="container">Hello</div>
```

### **D. `style`**

**Syntax:**

```jsx
<element style={{ property: "value" }} />
```

**Example:**

```jsx
<h1 style={{ color: "blue", fontSize: "24px" }}>
  Hello
</h1>
```

### **E. Boolean Attribute**

**Syntax:**

```jsx
<element attribute />
```

**Example:**

```jsx
<button disabled>Submit</button>
```

---

# **4. React JSX If Statements**

**Definition:**

**`if`** statements are used to execute different code based on a condition.

**Syntax:**

```jsx
if (condition) {
  // code
}
```

**Example:**

```jsx
function App() {
  const isLoggedIn = true;

  if (isLoggedIn) {
    return <h1>Welcome User</h1>;
  }

  return <h1>Please Login</h1>;
}
```

---

# **5. React Components**

**Definition:**

Components are reusable building blocks of a React application.

### **Types**

### **A. Function Component**

**Definition:**

A JavaScript function that returns JSX.

**Syntax:**

```jsx
function ComponentName() {
  return <JSX />;
}
```

**Example:**

```jsx
function Welcome() {
  return <h1>Welcome to React</h1>;
}
```

### **B. Class Component**

**Definition:**

A component created using an ES6 class that extends **`React.Component`**.

**Syntax:**

```jsx
class ComponentName extends React.Component {
  render() {
    return <JSX />;
  }
}
```

**Example:**

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Welcome to React</h1>;
  }
}
```

### **C. Nested Component**

**Definition:**

A component rendered inside another component.

**Example:**

```jsx
function Header() {
  return <h1>Header</h1>;
}

function App() {
  return (
    <div>
      <Header />
      <p>Content</p>
    </div>
  );
}
```

---

# **6. React Class**

**Definition:**

A React class component is an ES6 class that extends **`React.Component`** and contains a **`render()`** method.

**Syntax:**

```jsx
class ComponentName extends React.Component {
  render() {
    return <h1>Hello</h1>;
  }
}
```

**Example:**

```jsx
import React from "react";

class App extends React.Component {
  render() {
    return <h1>Hello React</h1>;
  }
}

export default App;
```

### **Class Component with State**

**Syntax:**

```jsx
class ComponentName extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      value: data
    };
  }
}
```

**Example:**

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      count: 0
    };
  }

  render() {
    return <h1>{this.state.count}</h1>;
  }
}
```

---

# **7. React Props**

**Definition:**

Props are data passed from a parent component to a child component.

**Syntax:**

```jsx
<ComponentName propName={value} />
```

**Example:**

```jsx
function Welcome(props) {
  return <h1>Hello {props.name}</h1>;
}

function App() {
  return <Welcome name="John" />;
}
```

### **Types of Props**

### **A. String Props**

```jsx
<Welcome name="John" />
```

### **B. Number Props**

```jsx
<Welcome age={25} />
```

### **C. Boolean Props**

```jsx
<Welcome isAdmin={true} />
```

### **D. Array Props**

```jsx
<Welcome items={["Apple", "Mango"]} />
```

### **E. Object Props**

```jsx
<Welcome user={{ name: "John", age: 25 }} />
```

### **F. Function Props**

```jsx
function Child({ handleClick }) {
  return <button onClick={handleClick}>Click</button>;
}

function App() {
  const showMessage = () => {
    alert("Hello");
  };

  return <Child handleClick={showMessage} />;
}
```

---

# **8. React Props Destructuring**

**Definition:**

Props destructuring extracts prop values directly into variables.

### **A. Destructuring in Function Parameter**

**Syntax:**

```jsx
function Component({ prop1, prop2 }) {
  return <JSX />;
}
```

**Example:**

```jsx
function User({ name, age }) {
  return (
    <h1>
      {name} - {age}
    </h1>
  );
}
```

### **B. Destructuring Inside Function**

**Syntax:**

```jsx
function Component(props) {
  const { prop1, prop2 } = props;
}
```

**Example:**

```jsx
function User(props) {
  const { name, age } = props;

  return <h1>{name} - {age}</h1>;
}
```

---

# **9. React Props Children**

**Definition:**

**`children`** is a special prop that contains the content placed between a component's opening and closing tags.

**Syntax:**

```jsx
<Component>
  Content
</Component>
```

**Example:**

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

function App() {
  return (
    <Card>
      <h1>Hello React</h1>
      <p>This is card content.</p>
    </Card>
  );
}
```

---

# **10. React Events**

**Definition:**

React events are used to respond to user actions such as clicks, typing, submitting forms, and mouse actions.

### **A. `onClick`**

**Syntax:**

```jsx
<button onClick={functionName}>Click</button>
```

**Example:**

```jsx
function App() {
  const handleClick = () => {
    alert("Button clicked");
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```

### **B. `onChange`**

**Syntax:**

```jsx
<input onChange={functionName} />
```

**Example:**

```jsx
function App() {
  const handleChange = (event) => {
    console.log(event.target.value);
  };

  return <input onChange={handleChange} />;
}
```

### **C. `onSubmit`**

**Syntax:**

```jsx
<form onSubmit={functionName}>
```

**Example:**

```jsx
function App() {
  const handleSubmit = (event) => {
    event.preventDefault();
    alert("Form submitted");
  };

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```

### **D. `onMouseEnter`**

**Syntax:**

```jsx
<div onMouseEnter={functionName}>
```

**Example:**

```jsx
function App() {
  const handleMouseEnter = () => {
    console.log("Mouse entered");
  };

  return <div onMouseEnter={handleMouseEnter}>Hover Me</div>;
}
```

### **E. `onKeyDown`**

**Syntax:**

```jsx
<input onKeyDown={functionName} />
```

**Example:**

```jsx
function App() {
  const handleKeyDown = (event) => {
    console.log(event.key);
  };

  return <input onKeyDown={handleKeyDown} />;
}
```

---

# **11. React Conditionals**

**Definition:**

Conditional rendering displays different JSX based on a condition.

### **A. `if` Statement**

**Example:**

```jsx
function App() {
  const isLoggedIn = true;

  if (isLoggedIn) {
    return <h1>Welcome</h1>;
  }

  return <h1>Login</h1>;
}
```

### **B. Ternary Operator**

**Syntax:**

```jsx
condition ? trueValue : falseValue
```

**Example:**

```jsx
function App() {
  const isLoggedIn = true;

  return (
    <h1>
      {isLoggedIn ? "Welcome" : "Please Login"}
    </h1>
  );
}
```

### **C. Logical AND `&&`**

**Syntax:**

```jsx
condition && JSX
```

**Example:**

```jsx
function App() {
  const isAdmin = true;

  return (
    <div>
      {isAdmin && <button>Admin Panel</button>}
    </div>
  );
}
```

### **D. Logical OR `||`**

**Syntax:**

```jsx
value || defaultValue
```

**Example:**

```jsx
function App() {
  const name = "";

  return <h1>{name || "Guest"}</h1>;
}
```

---

# **12. React Lists**

**Definition:**

Lists are used to render multiple elements from an array.

### **A. Rendering Array with `map()`**

**Syntax:**

```jsx
array.map((item) => (
  <Element>{item}</Element>
))
```

**Example:**

```jsx
function App() {
  const fruits = ["Apple", "Mango", "Banana"];

  return (
    <ul>
      {fruits.map((fruit) => (
        <li key={fruit}>{fruit}</li>
      ))}
    </ul>
  );
}
```

### **B. List with Objects**

**Syntax:**

```jsx
array.map((item) => (
  <Element key={item.id}>
    {item.property}
  </Element>
))
```

**Example:**

```jsx
function App() {
  const users = [
    { id: 1, name: "John" },
    { id: 2, name: "Alice" }
  ];

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

### **C. List with Components**

**Syntax:**

```jsx
array.map((item) => (
  <Component key={item.id} {...item} />
))
```

**Example:**

```jsx
function User({ name }) {
  return <li>{name}</li>;
}

function App() {
  const users = [
    { id: 1, name: "John" },
    { id: 2, name: "Alice" }
  ];

  return (
    <ul>
      {users.map((user) => (
        <User key={user.id} name={user.name} />
      ))}
    </ul>
  );
}
```

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

A **form** in React is used to collect user input. React generally handles form values through **state**, making the form a **controlled component**.

### **Types**

1. **Controlled Forms**
2. **Uncontrolled Forms**

### **Sub-types of form inputs**

- Text input
- Password
- Email
- Number
- Textarea
- Select
- Checkbox
- Radio
- File input

### **Syntax — Controlled Form**

```jsx
import { useState } from "react";

function Form() {
  const [name, setName] = useState("");

  return (
    <form>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />

      <p>Name: {name}</p>
    </form>
  );
}
```

### **Example**

```jsx
function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  return (
    <form>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />

      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
    </form>
  );
}
```

### **Controlled vs Uncontrolled**

| **Controlled** | **Uncontrolled** |
| --- | --- |
| Value stored in React state | Value stored in DOM |
| Uses **`value`** | Uses **`defaultValue`** |
| Uses **`onChange`** | Usually uses **`ref`** |
| Easier validation | Simpler for some cases |
| React controls input | DOM controls input |

### **Important**

```jsx
value={state}
```

makes an input controlled.

```jsx
defaultValue="John"
```

provides an initial value without controlling it through state.

---

# **React Forms Submit**

Form submission is handled using the form's **`onSubmit`** event.

### **Syntax**

```jsx
<form onSubmit={handleSubmit}>
```

```jsx
function handleSubmit(e) {
  e.preventDefault();
}
```

### **Example**

```jsx
function Login() {
  const [email, setEmail] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();

    console.log(email);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />

      <button type="submit">
        Login
      </button>
    </form>
  );
}
```

### **Types of submission**

1. **Normal browser submission**
2. **React-controlled submission**
3. **Async submission**

### **Async example**

```jsx
const handleSubmit = async (e) => {
  e.preventDefault();

  const response = await fetch("/api/login", {
    method: "POST",
    body: JSON.stringify({ email })
  });

  const data = await response.json();
};
```

### **Important**

Always use:

```jsx
e.preventDefault();
```

when you don't want the browser to reload/navigate away.

---

# **React Textarea**

### **Definition**

**`textarea`** is used for multi-line text.

Unlike HTML, React normally controls it using **`value`**.

### **Syntax**

```jsx
<textarea
  value={text}
  onChange={(e) => setText(e.target.value)}
/>
```

### **Example**

```jsx
function Message() {
  const [message, setMessage] = useState("");

  return (
    <textarea
      value={message}
      onChange={(e) => setMessage(e.target.value)}
      placeholder="Enter message"
    />
  );
}
```

### **Types**

1. Controlled textarea
2. Uncontrolled textarea

### **Controlled**

```jsx
<textarea value={message} onChange={handleChange} />
```

### **Uncontrolled**

```jsx
<textarea defaultValue="Hello" ref={textRef} />
```

### **Important**

Don't use:

```jsx
<textarea>
  {message}
</textarea>
```

for a controlled React textarea.

Use:

```jsx
<textarea value={message} />
```

---

# **React Select**

### **Definition**

**`select`** creates a dropdown menu.

### **Syntax**

```jsx
<select value={country} onChange={handleChange}>
  <option value="india">India</option>
  <option value="usa">USA</option>
</select>
```

### **Example**

```jsx
function Country() {
  const [country, setCountry] = useState("");

  return (
    <>
      <select
        value={country}
        onChange={(e) => setCountry(e.target.value)}
      >
        <option value="">Select Country</option>
        <option value="india">India</option>
        <option value="usa">USA</option>
      </select>

      <p>Selected: {country}</p>
    </>
  );
}
```

### **Types**

- Single select
- Multiple select

### **Multiple select**

```jsx
<select
  multiple
  value={countries}
  onChange={(e) => {
    const values = [...e.target.selectedOptions]
      .map(option => option.value);

    setCountries(values);
  }}
>
```

---

# **React Multiple Inputs**

### **Definition**

A form may contain multiple inputs. Instead of creating separate handlers, we can use **one generic handler**.

### **Syntax**

```jsx
const handleChange = (e) => {
  const { name, value } = e.target;

  setForm({
    ...form,
    [name]: value
  });
};
```

### **Example**

```jsx
function Register() {
  const [form, setForm] = useState({
    name: "",
    email: "",
    age: ""
  });

  const handleChange = (e) => {
    const { name, value } = e.target;

    setForm(prev => ({
      ...prev,
      [name]: value
    }));
  };

  return (
    <form>
      <input
        name="name"
        value={form.name}
        onChange={handleChange}
      />

      <input
        name="email"
        value={form.email}
        onChange={handleChange}
      />

      <input
        name="age"
        value={form.age}
        onChange={handleChange}
      />
    </form>
  );
}
```

### **Types**

1. Separate state for each input
2. Single object state
3. Generic change handler

### **Key concept**

```jsx
[name]: value
```

is a **computed property name**.

---

# **React Checkbox**

### **Definition**

Checkbox allows the user to select/deselect a boolean value.

### **Syntax**

```jsx
<input
  type="checkbox"
  checked={isChecked}
  onChange={(e) => setIsChecked(e.target.checked)}
/>
```

### **Example**

```jsx
function Terms() {
  const [accepted, setAccepted] = useState(false);

  return (
    <label>
      <input
        type="checkbox"
        checked={accepted}
        onChange={(e) => setAccepted(e.target.checked)}
      />

      Accept Terms
    </label>
  );
}
```

### **Types**

1. Single checkbox
2. Multiple checkboxes
3. Checkbox group
4. Select all / deselect all

### **Multiple checkboxes**

```jsx
const [skills, setSkills] = useState([]);

const handleSkill = (e) => {
  const { value, checked } = e.target;

  setSkills(prev =>
    checked
      ? [...prev, value]
      : prev.filter(skill => skill !== value)
  );
};
```

### **Important**

Checkbox uses:

```jsx
checked
```

not:

```jsx
value
```

to represent its selected state.

---

# **React Radio**

### **Definition**

Radio buttons allow selecting **one option from a group**.

### **Syntax**

```jsx
<input
  type="radio"
  name="gender"
  value="male"
  checked={gender === "male"}
  onChange={(e) => setGender(e.target.value)}
/>
```

### **Example**

```jsx
function Gender() {
  const [gender, setGender] = useState("");

  return (
    <>
      <label>
        <input
          type="radio"
          name="gender"
          value="male"
          checked={gender === "male"}
          onChange={(e) => setGender(e.target.value)}
        />
        Male
      </label>

      <label>
        <input
          type="radio"
          name="gender"
          value="female"
          checked={gender === "female"}
          onChange={(e) => setGender(e.target.value)}
        />
        Female
      </label>
    </>
  );
}
```

### **Types**

- Single radio group
- Dynamic radio group

### **Important**

Radio buttons in the same group should have the same:

```jsx
name
```

---

# **14. React Portals**

### **Definition**

A **Portal** allows a React component to render its UI into a different DOM node outside its normal parent DOM hierarchy.

Useful for:

- Modals
- Dialogs
- Tooltips
- Dropdowns
- Notifications

### **Syntax**

Modern React:

```jsx
import { createPortal } from "react-dom";

createPortal(
  <Component />,
  document.getElementById("portal-root")
);
```

### **Example**

**`index.html`**

```html
<div id="root"></div>
<div id="modal-root"></div>
```

Component:

```jsx
import { createPortal } from "react-dom";

function Modal() {
  return createPortal(
    <div className="modal">
      <h2>Hello Modal</h2>
    </div>,
    document.getElementById("modal-root")
  );
}
```

### **Types**

1. Modal Portal
2. Tooltip Portal
3. Notification Portal
4. Overlay Portal

### **Important concept**

A portal changes the **DOM location**, but the component remains part of the same **React tree**.

Therefore, React context and event propagation still work according to the React tree.

---

# **15. React Suspense**

### **Definition**

**`Suspense`** allows React to display a fallback UI while some child content is not ready.

Commonly used with:

- Lazy-loaded components
- Code splitting
- Suspense-enabled data sources

### **Syntax**

```jsx
<Suspense fallback={<Loading />}>
  <Component />
</Suspense>
```

### **Example — Lazy Loading**

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

### **Types**

1. Component lazy loading
2. Code splitting
3. Suspense boundaries
4. Suspense-enabled data loading

### **Nested Suspense**

```jsx
<Suspense fallback={<PageLoading />}>
  <Header />

  <Suspense fallback={<ContentLoading />}>
    <Content />
  </Suspense>
</Suspense>
```

### **Important**

**`Suspense`** is not simply an alternative to:

```jsx
isLoading ? <Loading /> : <Component />
```

It works with React features that can **suspend rendering**.

---

# **16. React CSS Styling**

### **Definition**

React supports multiple approaches to styling components.

### **Types**

1. Inline CSS
2. External CSS
3. CSS Modules
4. CSS-in-JS
5. Sass/SCSS
6. Utility CSS frameworks

---

## **10.1 Inline CSS**

### **Syntax**

```jsx
<div style={{ color: "red", fontSize: "20px" }}>
  Hello
</div>
```

### **Example**

```jsx
const style = {
  color: "blue",
  backgroundColor: "lightgray"
};

function App() {
  return <h1 style={style}>Hello React</h1>;
}
```

### **Important**

CSS property names become camelCase:

```css
background-color
```

becomes:

```jsx
backgroundColor
```

### **Best for**

- Dynamic styles
- Small component-specific styles

---

# **React CSS Modules**

### **Definition**

CSS Modules scope CSS class names locally to a component.

### **File**

```
Button.module.css
```

### **CSS**

```css
.button {
  background: blue;
  color: white;
}
```

### **Component**

```jsx
import styles from "./Button.module.css";

function Button() {
  return (
    <button className={styles.button}>
      Click
    </button>
  );
}
```

### **Types**

1. Local classes
2. Local animations
3. Conditional classes
4. Composed classes

### **Conditional class**

```jsx
<div className={`${styles.card} ${active ? styles.active : ""}`}>
```

### **Advantage**

Normal CSS:

```css
.button
```

can potentially conflict with another **`.button`**.

CSS Modules generate scoped class names.

---

# **React CSS-in-JS**

### **Definition**

CSS-in-JS means writing CSS using JavaScript or JavaScript-based APIs.

Popular approaches/libraries include:

- styled-components
- Emotion
- other CSS-in-JS solutions

### **Example concept**

```jsx
const Button = styled.button`
  background: blue;
  color: white;
`;
```

### **Dynamic styling**

```jsx
const Button = styled.button`
  background: ${(props) =>
    props.primary ? "blue" : "gray"};
`;
```

Usage:

```jsx
<Button primary>
  Submit
</Button>
```

### **Types**

1. Styled components
2. Dynamic styles
3. Theme-based styling
4. Component-scoped styling

### **Advantages**

- Dynamic styles
- Component-level styling
- Theme support

### **Disadvantages**

- Additional abstraction
- Runtime/build considerations depending on library
- Can increase complexity in large projects

---

# **17. React Router**

### **Definition**

React Router is used for **client-side routing** in React applications.

It allows different URLs to render different components without a full page reload.

### **Main concepts**

- Router
- Routes
- Route
- Link
- Navigate
- Nested routes
- URL parameters
- Query parameters
- Layout routes
- Protected routes

### **Basic syntax**

```jsx
import {
  BrowserRouter,
  Routes,
  Route
} from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

### **Navigation**

```jsx
import { Link } from "react-router-dom";

<Link to="/about">
  About
</Link>
```

### **Dynamic route**

```jsx
<Route path="/users/:id" element={<User />} />
```

Access parameter:

```jsx
import { useParams } from "react-router-dom";

function User() {
  const { id } = useParams();

  return <h1>User: {id}</h1>;
}
```

### **Programmatic navigation**

```jsx
const navigate = useNavigate();

navigate("/dashboard");
```

### **Nested routes**

```jsx
<Route path="/dashboard" element={<Dashboard />}>
  <Route path="profile" element={<Profile />} />
  <Route path="settings" element={<Settings />} />
</Route>
```

### **Types**

1. Static routes
2. Dynamic routes
3. Nested routes
4. Layout routes
5. Protected routes
6. Error routes
7. Catch-all routes

### **Important**

Understand these separately:

```
Link
↓
User navigation

useNavigate()
↓
Programmatic navigation

useParams()
↓
URL parameters

useLocation()
↓
Current location

Outlet
↓
Render child route
```

---

This topic can refer to **React UI transitions** and the React **Transition APIs**.

## **A. CSS Transitions**

### **Example**

```css
.button {
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: blue;
}
```

---

## **B. `useTransition`**

### **Definition**

**`useTransition`** allows React to mark an update as **non-urgent**, so urgent UI updates can remain responsive.

### **Syntax**

```jsx
const [isPending, startTransition] = useTransition();
```

### **Example**

```jsx
function Search() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);

  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    setQuery(e.target.value);

    startTransition(() => {
      setResults(searchData(e.target.value));
    });
  };

  return (
    <>
      <input
        value={query}
        onChange={handleChange}
      />

      {isPending && <p>Updating...</p>}

      <Results data={results} />
    </>
  );
}
```

### **Types**

1. Urgent update
2. Transition/non-urgent update

### **Important**

**`useTransition`** is about **update priority**, not CSS animation.

---

## **C. `startTransition`**

Can also be used directly:

```jsx
import { startTransition } from "react";

startTransition(() => {
  setState(value);
});
```

---

# **18. React Forward Ref**

### **Definition**

**`forwardRef`** historically allowed a parent component to pass a **`ref`** through a component to a child DOM element.

### **Traditional syntax**

```jsx
const Input = forwardRef(function Input(props, ref) {
  return (
    <input ref={ref} {...props} />
  );
});
```

Parent:

```jsx
function App() {
  const inputRef = useRef(null);

  return (
    <>
      <Input ref={inputRef} />

      <button onClick={() => inputRef.current.focus()}>
        Focus
      </button>
    </>
  );
}
```

### **Types**

1. DOM ref forwarding
2. Component ref forwarding
3. Ref + custom methods

### **Important modern React note**

In **React 19**, **`ref`** can be passed as a prop to function components, so **`forwardRef`** is no longer required for this common use case.

Conceptually:

```jsx
function Input({ ref, ...props }) {
  return <input ref={ref} {...props} />;
}
```

For intermediate-level notes, know **both the traditional `forwardRef` pattern and the newer React approach**.

---

# **19. React HOC — Higher Order Component**

### **Definition**

A **Higher Order Component (HOC)** is a function that takes a component and returns an enhanced component.

### **Basic formula**

```
HOC(Component) → EnhancedComponent
```

### **Syntax**

```jsx
function withAuth(Component) {
  return function ProtectedComponent(props) {
    if (!isLoggedIn) {
      return <Login />;
    }

    return <Component {...props} />;
  };
}
```

Usage:

```jsx
const ProtectedDashboard = withAuth(Dashboard);
```

### **Example**

```jsx
function withLoading(Component) {
  return function WithLoading({ loading, ...props }) {
    if (loading) {
      return <p>Loading...</p>;
    }

    return <Component {...props} />;
  };
}
```

Usage:

```jsx
const UserListWithLoading = withLoading(UserList);
```

### **Types**

Common HOCs:

1. Authentication HOC
2. Authorization HOC
3. Loading HOC
4. Logging HOC
5. Data-fetching HOC
6. Feature/permission HOC

### **Important rules**

Don't mutate the original component:

```jsx
// Avoid
Component.someProperty = ...
```

Instead:

```jsx
return function EnhancedComponent(props) {
  return <Component {...props} />;
};
```

### **HOC vs Custom Hook**

| **HOC** | **Custom Hook** |
| --- | --- |
| Enhances component | Shares logic |
| Returns component | Returns values/functions |
| Component composition | Logic composition |
| Older/common pattern | Preferred for many modern use cases |

---

# **20. React Sass**

### **Definition**

**Sass/SCSS** is a CSS preprocessor that provides features such as:

- Variables
- Nesting
- Mixins
- Functions
- Partials
- Operators

React can use Sass by compiling **`.scss`** files.

### **Installation**

```bash
npm install sass
```

### **File**

```
App.scss
```

### **SCSS**

```scss
$primary: blue;

.button {
  background: $primary;
  color: white;

  &:hover {
    background: darkblue;
  }
}
```

### **React**

```jsx
import "./App.scss";

function App() {
  return (
    <button className="button">
      Submit
    </button>
  );
}
```

### **Types**

1. Variables
2. Nesting
3. Mixins
4. Functions
5. Partials
6. Modules
7. Operators

### **Variables**

```scss
$primary-color: blue;

.title {
  color: $primary-color;
}
```

### **Nesting**

```scss
.card {
  padding: 20px;

  .title {
    font-size: 20px;
  }

  &:hover {
    transform: scale(1.02);
  }
}
```

### **Mixin**

```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  @include flex-center;
}
```

### **Sass + CSS Modules**

```
Button.module.scss
```

```scss
.button {
  background: blue;
}
```

```jsx
import styles from "./Button.module.scss";

<button className={styles.button}>
  Click
</button>
```

This is a very useful combination in React projects.

---

# **21. REACT HOOKS**

Hooks are one of the most important areas for intermediate React.

---

# **i. What are Hooks?**

### **Definition**

**Hooks** are functions that allow functional components to use React features such as:

- State
- Effects
- Context
- Refs
- Performance optimizations

Hooks were introduced in React 16.8.

### **Syntax**

```jsx
const [state, setState] = useState(initialValue);
```

### **Types of Hooks**

### **Built-in Hooks**

#### **State Hooks**

```
useState
useReducer
```

#### **Context Hook**

```
useContext
```

#### **Ref Hooks**

```
useRef
useImperativeHandle
```

#### **Effect Hooks**

```
useEffect
useLayoutEffect
useInsertionEffect
```

#### **Performance Hooks**

```
useMemo
useCallback
useTransition
useDeferredValue
```

#### **Other Hooks**

```
useId
useSyncExternalStore
useDebugValue
```

### **Custom Hooks**

Developer-created hooks:

```jsx
function useSomething() {
  // logic
}
```

---

# **ii. React `useState`**

### **Definition**

**`useState`** adds state to a functional component.

### **Syntax**

```jsx
const [state, setState] = useState(initialValue);
```

### **Example**

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>{count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </>
  );
}
```

### **Types**

State can contain:

1. Primitive
2. Object
3. Array
4. Boolean
5. Function/lazy initial state

### **Object state**

```jsx
const [user, setUser] = useState({
  name: "",
  age: 20
});
```

Update:

```jsx
setUser(prev => ({
  ...prev,
  name: "John"
}));
```

### **Array state**

```jsx
const [items, setItems] = useState([]);

setItems(prev => [...prev, newItem]);
```

### **Functional update**

Use when new state depends on previous state:

```jsx
setCount(prev => prev + 1);
```

### **Lazy initialization**

```jsx
const [data, setData] = useState(() => expensiveCalculation());
```

### **Important**

Never mutate state directly:

```jsx
// Wrong
user.name = "John";
```

Instead:

```jsx
setUser(prev => ({
  ...prev,
  name: "John"
}));
```

---

# **iii. React `useEffect`**

### **Definition**

**`useEffect`** allows a component to synchronize with **external systems** after rendering.

Common uses:

- API calls
- Event listeners
- Timers
- Subscriptions
- DOM APIs
- Third-party libraries

### **Syntax**

```jsx
useEffect(() => {
  // effect

  return () => {
    // cleanup
  };
}, [dependencies]);
```

### **Example**

```jsx
function User() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch("/api/user")
      .then(res => res.json())
      .then(data => setUser(data));
  }, []);

  return <div>{user?.name}</div>;
}
```

### **Dependency types**

### **1. No dependency array**

```jsx
useEffect(() => {
  console.log("after every render");
});
```

Runs after every render.

### **2. Empty dependency array**

```jsx
useEffect(() => {
  console.log("effect");
}, []);
```

Runs after initial mount.

### **3. Dependency array**

```jsx
useEffect(() => {
  console.log(userId);
}, [userId]);
```

Runs when **`userId`** changes.

### **Cleanup**

```jsx
useEffect(() => {
  const id = setInterval(() => {
    console.log("tick");
  }, 1000);

  return () => {
    clearInterval(id);
  };
}, []);
```

### **Types**

1. Data fetching
2. Subscription
3. Event listener
4. Timer
5. Synchronization
6. Cleanup effect

### **Important intermediate concept**

Don't use **`useEffect`** just to calculate derived values.

Avoid:

```jsx
const [fullName, setFullName] = useState("");

useEffect(() => {
  setFullName(firstName + " " + lastName);
}, [firstName, lastName]);
```

Prefer:

```jsx
const fullName = `${firstName} ${lastName}`;
```

---

# **iv. React `useContext`**

### **Definition**

**`useContext`** allows a component to read values from React Context without manually passing props through every level.

Useful for:

- Theme
- Authentication
- Language
- User settings
- Global-ish application state

### **Syntax**

Create context:

```jsx
const ThemeContext = createContext();
```

Provider:

```jsx
<ThemeContext value="dark">
  <App />
</ThemeContext>
```

Consume:

```jsx
const theme = useContext(ThemeContext);
```

### **Example**

```jsx
const ThemeContext = createContext("light");

function App() {
  return (
    <ThemeContext value="dark">
      <Page />
    </ThemeContext>
  );
}

function Page() {
  const theme = useContext(ThemeContext);

  return <div>Theme: {theme}</div>;
}
```

### **Types**

1. Theme Context
2. Auth Context
3. User Context
4. Language Context
5. Application settings

### **Important**

Context is not automatically a replacement for every state-management library.

Use it mainly when many components need access to the same value.

---

# **v. React `useRef`**

### **Definition**

**`useRef`** stores a mutable value that persists across renders **without causing a re-render when changed**.

### **Syntax**

```jsx
const ref = useRef(initialValue);
```

### **Type 1 — DOM reference**

```jsx
const inputRef = useRef(null);

<input ref={inputRef} />
```

Then:

```jsx
inputRef.current.focus();
```

### **Example**

```jsx
function Input() {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} />

      <button onClick={() => inputRef.current.focus()}>
        Focus
      </button>
    </>
  );
}
```

### **Type 2 — Store mutable value**

```jsx
const countRef = useRef(0);

countRef.current++;
```

### **Types**

1. DOM reference
2. Mutable value
3. Previous value storage
4. Timer/interval ID
5. Third-party library instance

### **Previous value example**

```jsx
const previousValue = useRef(value);

useEffect(() => {
  previousValue.current = value;
}, [value]);
```

### **Important**

Changing:

```jsx
ref.current
```

does **not** trigger a render.

---

# **vi. React `useReducer`**

### **Definition**

**`useReducer`** manages state using a **reducer function** and **actions**.

Useful when state logic becomes complex.

### **Syntax**

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

Reducer:

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };

    default:
      return state;
  }
}
```

### **Example**

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return {
        count: state.count + 1
      };

    case "decrement":
      return {
        count: state.count - 1
      };

    case "reset":
      return {
        count: 0
      };

    default:
      throw new Error("Unknown action");
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, {
    count: 0
  });

  return (
    <>
      <p>{state.count}</p>

      <button onClick={() => dispatch({ type: "increment" })}>
        +
      </button>

      <button onClick={() => dispatch({ type: "decrement" })}>
        -
      </button>
    </>
  );
}
```

### **Types**

1. Simple reducer
2. Object state reducer
3. Multiple-action reducer
4. Reducer + Context

### **Reducer pattern**

```
UI
 ↓
dispatch(action)
 ↓
Reducer
 ↓
New State
 ↓
UI
```

### **Important**

A reducer should be **pure**.

Don't do API calls or mutate external state inside the reducer.

---

# **vii. React `useCallback`**

### **Definition**

**`useCallback`** memoizes a **function reference** between renders.

### **Syntax**

```jsx
const memoizedFunction = useCallback(
  () => {
    // logic
  },
  [dependencies]
);
```

### **Example**

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

### **Practical example**

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Hello");
  }, []);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        {count}
      </button>

      <Child onClick={handleClick} />
    </>
  );
}
```

If **`Child`** is memoized:

```jsx
const Child = memo(function Child({ onClick }) {
  return <button onClick={onClick}>Child</button>;
});
```

**`useCallback`** can help maintain the same function reference.

### **Types**

1. Stable callback
2. Callback passed to memoized child
3. Callback used in dependency arrays
4. Event handler optimization

### **Important**

Don't use **`useCallback`** everywhere.

It is a **performance optimization**, not something required for normal event handlers.

---

# **viii. React `useMemo`**

### **Definition**

**`useMemo`** memoizes the **result of a calculation**.

### **Syntax**

```jsx
const result = useMemo(
  () => expensiveCalculation(data),
  [data]
);
```

### **Example**

```jsx
function ProductList({ products, search }) {
  const filteredProducts = useMemo(() => {
    return products.filter(product =>
      product.name
        .toLowerCase()
        .includes(search.toLowerCase())
    );
  }, [products, search]);

  return (
    <ul>
      {filteredProducts.map(product => (
        <li key={product.id}>
          {product.name}
        </li>
      ))}
    </ul>
  );
}
```

### **Types**

1. Expensive calculation
2. Derived data
3. Stable object reference
4. Stable array reference

### **`useMemo` vs `useCallback`**

| **`useMemo`** | **`useCallback`** |
| --- | --- |
| Memoizes a value | Memoizes a function |
| Returns calculated result | Returns function |
| **`useMemo(() => value, [])`** | **`useCallback(fn, [])`** |

Conceptually:

```jsx
useCallback(fn, deps)
```

is similar to:

```jsx
useMemo(() => fn, deps)
```

### **Important**

Don't memoize everything. Measure/understand the performance problem first.

---

# **ix. React Custom Hooks**

### **Definition**

A **Custom Hook** is a JavaScript function whose name starts with **`use`** and which can use other Hooks.

It is used to **reuse stateful logic**, not UI.

### **Syntax**

```jsx
function useSomething() {
  // hooks
  return value;
}
```

### **Example — `useCounter`**

```jsx
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => {
    setCount(prev => prev + 1);
  };

  const decrement = () => {
    setCount(prev => prev - 1);
  };

  return {
    count,
    increment,
    decrement
  };
}
```

Use it:

```jsx
function Counter() {
  const {
    count,
    increment,
    decrement
  } = useCounter(10);

  return (
    <>
      <p>{count}</p>

      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </>
  );
}
```

### **Types**

Common custom hooks:

1. **`useFetch`**
2. **`useForm`**
3. **`useLocalStorage`**
4. **`useDebounce`**
5. **`useToggle`**
6. **`usePrevious`**
7. **`useOnlineStatus`**
8. **`useWindowSize`**
9. **`useClickOutside`**

### **Example — `useToggle`**

```jsx
function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);

  const toggle = () => {
    setValue(prev => !prev);
  };

  return [value, toggle];
}
```

Usage:

```jsx
const [isOpen, toggleOpen] = useToggle();

<button onClick={toggleOpen}>
  Toggle
</button>
```

### **Important distinction**

Custom Hooks reuse:

> **logic**
> 

They do not reuse the actual component UI.

---

# **React Hooks — Quick Classification**

This is worth memorizing for interviews and practical development:

| **Hook** | **Main Purpose** | **Category** |
| --- | --- | --- |
| **`useState`** | Local state | State |
| **`useReducer`** | Complex state | State |
| **`useEffect`** | External synchronization | Effect |
| **`useContext`** | Consume context | Context |
| **`useRef`** | Persistent mutable value / DOM | Ref |
| **`useMemo`** | Memoize value | Performance |
| **`useCallback`** | Memoize function | Performance |
| **`useTransition`** | Non-urgent updates | Performance/Concurrency |
| **`useDeferredValue`** | Defer a value | Performance/Concurrency |
| **`useId`** | Stable unique IDs | Utility |
| Custom Hook | Reuse logic | Custom |

---

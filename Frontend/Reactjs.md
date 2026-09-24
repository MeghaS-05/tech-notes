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

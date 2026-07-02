# Introduction
Modern web applications consist of two major parts:

- Frontend —> What users see
- Backend —> Handles business logics, database, APIs and server-side operations

JavaScript was originally designed to run only inside the web browser. With the introduction of Node.js, JavaScript can also run on server, allowing developer to use a single language for both frontend and backend development.

Express.js is a lightweight framework built on top of Node.js that simplifies server and API development by providing features such as routing, middleware and request handling.

In these notes, we will learn:

- Node.js Fundamentals
- Express.js Fundamentals
- Routes & Middleware
- REST APIs
- Building a Mini Project

The objective is to understand both the theoretical concepts and practical implementation of backend development using Node.js and Express.



# Part 1 : Node.js Fundamental
JS was originally designed to run only inside web browsers. This meant developers could create interactive web pages, but they couldn’t use JS to build server or backend applications. 
Node.js solved this problem by providing a runtime environment that allows JS to run outside the browser.

With Node.js, JavaScript can be used to:
- Build web servers
- Create REST APIs
- Handle databases
- Build real-time applications
- Create command-line tools

Ultimately, Node.js is an open source, cross-platform JS environment built on Google’s V8 JavaScript Engine that allows JS to run outside the browser.

Advantage of Node.js :
1. Fast Execution :- Node.js uses Google’s V8 Engine which converts JS code into machine readable code which makes JS execution faster than traditional interpreter approaches.
2. Non-Blocking I/O :- Node.js does not wait for one operation to finish before handling another. This improves performance when handling many users.
3. Event-Driven Architecture :- Node.js listen to the users event and responds accordingly.
4. Huge Package Ecosystem :- Node.js contains and NPM packages that has thousands of reusable packages. Instead of writing code from scratch developers can use this packages.

## Real-Life Example
Imagine a restaurant.

### Traditional Waiting Model
Customer 1 Order
Wait
Finish

Customer 2 Order
Wait
Finish

Slow.

### Node.js Model
Take Customer 1 Order
Kitchen Starts Cooking

Take Customer 2 Order
Kitchen Starts Cooking

Take Customer 3 Order
Kitchen Starts Cooking


The server remains free to handle new work while waiting for long operations to finish.


Node.js Architecture : (Refer from W3School)
**1. Client Request Phase**
- Clients send requests to the Node.js server
- Each request is added to the **Event Queue**

**2. Event Loop Phase**
- The Event Loop continuously checks the **Event Queue**
- Picks up requests one by one in a loop

**3. Request Processing**
- Simple (non-blocking) tasks are handled immediately by the main thread
- Complex/blocking tasks are offloaded to the Thread Pool

**4. Response Phase**
- When blocking tasks complete, their callbacks are placed in the **Callback Queue**
- Event Loop processes callbacks and sends responses
  

Installation & Setup :
1. Install Node.js from official website:
2. Verify Installation using cmd node -v and also check for npm -v
3. Create your first project and inititalize node project using cmd npm init -y
4. Create first file like app.js that’s must be a main file

Few points:
- For installing packages use cmd — npm i package-name
- Always initialize your project using cmd as npm init -y
- Install Nodemon package which automatically restarts your application whenever file changes are detected in your project.



## Event Loop + Sync vs Aysnc :
Synchronous code mean **instructions are executed one after another in order.** Each operation must complete before the next one starts. whereas Asynchronous code means **tasks are initiated but do not block the execution of other code**. The result is handled later once the task is completed.

#### Why Asynchronous Programming Exists :
Node.js handles many users at the same time.
If it waited for each task, performance would drop.
So instead: Node continues execution and handles results later.


______________________________________________________________________________________________________________________________________________________________________


## Event Loop (Core Concept)
The Event Loop is a mechanism that **controls execution of asynchronous operations**.

#### Simple Definition:
> It decides when async callbacks should be executed.

## How Event Loop Works (Concept Flow)
1. Synchronous code goes to execution first.
2. Async tasks are sent to background.
3. Once completed, they enter a waiting queue.
4. Event Loop moves them back to execution.

### Flow Diagram (for notes):
Call Stack → Background → Callback Queue → Event Loop → Call Stack


## Key Components Inside Event Loop System
1. Call Stack
Executes synchronous code line by line.

2. Background APIs
Handles async tasks like timers, file operations.

3. Callback Queue
Stores completed async tasks waiting for execution.

4. Event Loop
Moves tasks from queue to call stack.


## Important Concept
> Asynchronous does NOT mean parallel execution.
> It means deferred execution.\



Node.js Core Modules:
Module is a self-contained block of code that performs a specific task and can be reused in other files. Module help in code reusability, better organization, easier maintenance etc.

There are 3 types of modules :
1. Built-In Modules (modules provided by node.js itself like fs, http, path, os, url)
2. User-Defined / Custom Module (created by developers)
3. Third-Party Modules (external modules installed using npm like express, nodemon, mongoose etc)

## How Modules Work in Node.js
Node.js uses:

- `require()` → to import modules
- `module.exports` → to export modules

### Concept Flow:
File A (Module) → exports code
File B → imports and uses it





# Part 2 : Express.js, Routing & Middleware
Express.js is a lightweight web framework built on top of Node.js which simplifies creating web servers and APIs by providing different features like routing, middleware, request handling and other useful features.
Node.js and Express.js are related to each other like Node.js is the engine which runs JS code and Express.js is a framework that makes building web application with Node.js easier.

- Installing express using CMD : npm i express

Example of implementing express.js :
const express = require("express");   //Import Expres
const app = express();  //Create Application

//Define Routes
app.get("/", (req, res) => {
res.send("Welcome to Express");
});

//Sart Server
app.listen(3000, () => {
console.log("Server running on port 3000");
});

Note: Here req is the incoming request and res is the outgoing request.
3000 is the port number (communication endpoint through which clients connect to the server)
here the response is get using a http status code.



## Understanding Request & Response Objects :
Whenever a client (browser, Postman, frontend application, mobile app, etc.) sends a request to an Express server, Express creates two important objects:
- **Request Object (`req`)** → Contains information about the incoming request.
- **Response Object (`res`)** → Used to send a response back to the client.
  
These two objects are available inside every route handler.


### Understanding the Request Object (`req`) :
The request object contains all information sent by the client.

Examples:
- URL
- Route parameters
- Query parameters
- Request body
- Headers
- Cookies

---

### Commonly Used Request Properties

| Property | Description | Syntax / Example |
| --- | --- | --- |
| `req.params` | Route parameters | app.get(”/user/:id”)
here : rep. route para. |
| `req.query` | Query parameters are values passed after the ? symbol in the url | `app.get("/search", (req, res) => { res.json(req.query);});`
Request`/search?name=Rahul&age=22` |
| `req.body` | Data sent in request body | app.post("/user", (req, res) => { res.json(req.body);}); |
| `req.headers` | Request headers |  |
| `req.method` | HTTP method | app.get(), app.post() |
| `req.url` | Requested URL | app.get(”/about” ,()⇒{}); |



### Understanding the Response Object (`res`) :
The response object is used to send data back to the client.

#### Common Response Methods

| Method | Purpose | Syntax / Example |
| --- | --- | --- |
| `res.send()` | Send text/HTML | res.send(”Welcome”) |
| `res.json()` | Send JSON | res.json({data in json}) |
| `res.status()` | Set status code | res.status(code).send(data) |
| `res.sendFile()` | Send file | res.sendFile(path.join(__dirname, "index.html")); |
| `res.redirect()` | Redirect request | res.redirect("/"); |



## Routing in Express :
Routing is the process of determining how an application responds to a client request for a specific URL and Http method.
A route consist of : Http method, URL Path and Route Handler.

Syntax :- app.METHOD(PATH, HANDLER)

Example :- 
app.get(”/”, (req, res)⇒{
    res.send(”Hello World”);
});


A route handler is a function that executes when a route is matched.


### HTTP Methods in Express:
Express supports all major HTTP methods.

| Method | Purpose | Syntax |
| --- | --- | --- |
| GET | Retrieve data | app.get(path, handler) |
| POST | Create data | app.post(path, handler) |
| PUT | Replace existing data | `app.put("/users/:id", (req, res) => { res.send(`User ${req.params.id} Updated`);});` |
| PATCH | Update existing data | app.patch("/users/:id", (req, res) => { res.send(`User ${req.params.id} Partially Updated`);}); |
| DELETE | Remove data | app.delete("/users/:id", (req, res) => { res.send(`User ${req.params.id} Deleted`);}); |


**Route chaining** in express allows multiple methods for the same route using `route().`

for example:
app.route("/users")
.get((req, res) => {
res.send("Get Users");
})
.post((req, res) => {
res.send("Create User");
})
.delete((req, res) => {
res.send("Delete User");
});


## Express Router:
As applications grow, writing all routes inside a single file makes the code difficult to read and maintain. Express provides **Router** to group related routes into separate files.
A Router acts like a mini Express application that can manage its own routes and middleware. Instead of defining all routes in `server.js`, we can create separate route files such as `userRoutes.js`, `productRoutes.js`, and `noteRoutes.js`.
This makes the application modular, organized, and easier to scale.

Syntax :

Step 1 : Create Router 
              const express = require(”express”);
              const router = express.Router();

Step 2 : Define Routes
router.get("/", (req, res) => {
res.send("All Users");
});

Step 3 : Export Router 
module.exports = router;

Step 4 : Import and Mount Router
const userRoutes = require(”./routes/userRoutes”);
app.use(”/users”, userRoutes);


### Nested Routes :
Nested routes are routes inside another resource. They represent relationships between resources.

### Middleware :
Middleware is a function that runs between request and response and can modify, end or forward the request.

## Key Points
- Middleware runs before the final route handler.
- It has access to `req`, `res`, and `next()`.
- It must call `next()` to move forward (unless response is sent). `next()` passes control to the next middleware or route handler.
- Middleware executes in order (top to bottom).
- Can be global, route-specific, or router-level.

Syntax :
app.use((req,res,next)⇒{next();});

Types of middleware :
1. Application - List Middleware  — Entire app
2. Route-Level Middleware — Specific route
3. Router-Level Middleware — Specific router
4. Built-in Middleware — Express feature
5. Third-party Middleware — External packages
6. Error Middleware — Handles error

## Note Point 📌
- Middleware runs between request and response.
- It can modify request/response objects.
- Must call `next()` to continue flow.
- Middleware executes in order.
- Without `next()`, request stops.
- `app.use()` is used for middleware.
- Middleware is the core concept of Express architecture.

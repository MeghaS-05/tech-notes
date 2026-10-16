~ created by Vercel in the year 2016, initial creator included Guillermo Rauch and other engineers. 

Next.js is a React framework for building full-stack web applications. Next.js makes easier to create production-ready web applications. It handles things like page rendering, routing, and performance automatically, so developers can focus on building features. Think of it like : React helps build the UI. Next.js helps you build the application around that UI.

**Next.js Features**

- **File-based Routing** → Create routes using folders and files.
- **Server Components** → Render components on the server by default.
- **Client Components** → Add interactivity using **`"use client"`**.
- **Server-Side Rendering (SSR)** → Generate pages dynamically on the server.
- **Static Rendering** → Pre-generate pages for faster loading.
- **Data Fetching** → Fetch API/database data directly in server-side code.
- **API Routes / Route Handlers** → Build backend APIs inside the Next.js project.
- **SEO & Metadata** → Easily manage page titles, descriptions, and metadata.
- **Image Optimization** → Optimize images using **`next/image`**.
- **Font Optimization** → Optimize fonts using **`next/font`**.
- **Layouts** → Share UI like Navbar/Footer across multiple pages.
- **Loading & Error UI** → Built-in **`loading.js`** and **`error.js`** conventions.
- **Dynamic Routes** → Create routes like **`/products/[id]`**.
- **Middleware** → Run logic before a request reaches a route.
- **Environment Variables** → Safely manage configuration/secrets.
- **TypeScript Support** → First-class TypeScript support.
- **Full-Stack Development** → Build frontend + backend functionality in one project.
- **Production Optimization** → Next.js optimizes the application for production builds.

Keywords : Static Server Rendering(SSR), Static Site Generation(SSG), Incremental Site Regeneration(ISR)

## Getting started with nextjs :

**Step 1** : Install Nodejs

**Step 2** : create nextjs project : npx create-next-app project-name  // you can also use npx create-next-app@latest . (here . means in the current folder).

**Step 3** : answer the questions asked

**To install tailwind to nextjs using cmd : “npm install - - save-dev typescript @types/react @types/node”**

Project Folder :

!image.png

- **public/** – Stores static assets like images and icons.
- **src/** – Contains the main application source code.
- **assets/** – Holds reusable static files (images, fonts, etc.).
- **components/** – Reusable UI components.
- **hooks/** – Custom React hooks.
- **layouts/** – Common layout components for pages.
- **lib/** – Helper libraries or third-party integrations.
- **app/** - Recommended routing directory for new Next.js projects using the App Router.
- **pages/** – Used with the Pages Router and contains routing files and API routes.
- **services/** – API calls and service logic.
- **styles/** – Global styles and CSS modules.
- **utils/** – Utility and helper functions.

## **Nextjs Router :**

### i)Routing in Nextjs

Routing means deciding which UI/pages should be displayed for a particular URL. Next.js uses file-system based routing.

Example

app/
├── page.js
├── about/
│   └── page.js
└── contact/
    └── page.js

Routes:

```
/          → app/page.js
/about     → app/about/page.js
/contact   → app/contact/page.js
```

### ii)Next.js Nested Routes

A nested routes is a route created by putting folders inside other folder. Remember nested folder = nested URL.

**examples**

app/
├── page.js
├── products/
│   ├── page.js
│   ├── mobile/
│   │   └── page.js
│   └── laptop/
│       └── page.js

Routes:

```
/                   → Home
/products           → Products
/products/mobile    → Mobile
/products/laptop    → Laptop
```

### iii)Next.js Pages

In the app router, a page.js file defines the UI for a route and makes that route publicly accessible.

for example page.js can be accessed using “/” url.

### iv)Next.js layout component

A layout is UI that is shared between multiple pages. Typical examples include nevbar, sidebar, footer etc.

### v)Navigate Between pages

There are two main ways we’ll use:

Type 1 : <Link> — for normal navigation between pages

Type 2 : useRouter() — for programmatic navigation, usually after an action such as clicking a button.

Example of Link : 

import Link from "next/link";

export default function Home() {
return (
<div>
<h1>Home</h1>

  <Link href="/about">
    Go to About
  </Link>
</div>

);
}

### vi)Linking between pages

Suppose:

app/
├── page.js
├── about/
│   └── page.js
└── contact/
    └── page.js

Your home page can contain:

import Link from "next/link";

export default function Home() {
  return (
    <>
      <h1>Home</h1>

      <Link href="/about">
        About
      </Link>

      <br />

      <Link href="/contact">
        Contact
      </Link>
    </>
  );
}

**Dynamic Link**

Later, when working with dynamic routes:

<Link href={`/products/${id}`}>
  View Product
</Link>

For example:

```
/products/101
```

### vii)Navigate Programmatically — useRouter()

useRouter() allows you to change routes using javascript. It is used in a client components.

**Syntax**

"use client";

import { useRouter } from "next/navigation";

const router = useRouter();

router.push("/about");

**Example**

"use client";

import { useRouter } from "next/navigation";

export default function Home() {
  const router = useRouter();

  function handleClick() {
    router.push("/about");
  }

  return (
    <button onClick={handleClick}>
      Go to About
    </button>
  );
}

**Important router methods**

| **Method** | **Meaning** |
| --- | --- |
| **`router.push()`** | Go to another page and add history entry |
| **`router.replace()`** | Go to another page without adding history entry |
| **`router.back()`** | Go back |
| **`router.forward()`** | Go forward |
| **`router.refresh()`** | Refresh current route |
| **`router.prefetch()`** | Prefetch a route |

### viii)Next.js Redirects

A redirect automatically sends the user from one URL to another. There are several ways to redirect in the App Router:

Type 1 : redirect() 

import { redirect } from "next/navigation";

export default function Dashboard() {
const isLoggedIn = false;

if (!isLoggedIn) {
redirect("/login");
}

return <h1>Dashboard</h1>;
}

Type 2 : permanentRedirect()  

Used when the URL has permanently changed.

import { permanentRedirect } from "next/navigation";

permanentRedirect("/new-url");

Type 3 : next.config.mjs

Useful when you have predefined redirects

const nextConfig = {
  async redirects() {
    return [
      {
        source: "/old",
        destination: "/new",
        permanent: true,
      },
    ];
  },
};

export default nextConfig;

Now:

```
/old → /new
```

### ix)Redirect with useRouter()

For a button/event in a Client Component:

For a button/event in a Client Component:

"use client";

import { useRouter } from "next/navigation";

export default function Page() {
  const router = useRouter();

  return (
    <button onClick={() => router.push("/login")}>
      Login
    </button>
  );
}

**Remember**

```
redirect()              → server-side/rendering logic
permanentRedirect()     → permanent redirect
next.config.mjs         → predefined redirects
router.push()           → event-based client navigation
```

### x)Dynamic Route Segments

a dynamic route is a route where part of the url can changes

For example:

/products/101
/products/102
/products/103

Type 1 : Single Dynamic Segment

**Syntax**

[parameter]

**Example**

app/
└── products/
    └── [id]/
        └── page.js

This matches:

/products/1
/products/2
/products/100

**`page.js`**:

export default async function Product({ params }) {
  const { id } = await params;

  return <h1>Product ID: {id}</h1>;
}

So:

/products/101

outputs:

```
Product ID: 101
```

### xi)Catch-all Dynamic Routes

A catch-all routes captures multiple URL segments.

**Syntax**

[...slug]

**Example**

app/
└── docs/
    └── [...slug]/
        └── page.js

Can match:

/docs/react
/docs/react/hooks
/docs/react/hooks/useState

Example:

export default async function Docs({ params }) {
  const { slug } = await params;

  return <h1>{slug.join(" / ")}</h1>;
}

For:

/docs/react/hooks

**`slug`** becomes:

```jsx
["react", "hooks"]
```

### xii)Optional Catch-all Routes

An optional catch-all route can match the route with or without additional segments.

**Syntax**

[[...slug]]

**Example**

app/
└── docs/
    └── [[...slug]]/
        └── page.js

Can match:

/docs
/docs/react
/docs/react/hooks

…slug means to catch everything that comes after docs. so from the above example slug=[”react”,”hooks”]

Remeber […slug] & [[…slug]] are both same but [] catches one or more whereas [[]] catches zero or more

### xiii)Middleware in Next.js

Middleware is also called as Proxy(from version 16 or above). Proxy allows you to run code before a request is completed. It can redirect, rewrite, modify request/responses headers, check conditions or handle certain authentication/locale routing logic

**Basic Syntax**

Create:

nextjslearning/
├── app/
├── public/
└── proxy.js

import { NextResponse }from "next/server";

export function proxy(request) {
  return NextResponse.next();
}

**`NextResponse.next()`** means:

Continue to the requested route.

**Matcher**

You normally don't want Proxy logic to run unnecessarily everywhere.

export const config = {
  matcher: "/dashboard/:path*",
};

This means the Proxy applies to:

/dashboard
/dashboard/settings
/dashboard/profile
/dashboard/anything

**Remember**

proxy.js
   ↓
runs before route completion
   ↓
check condition
   ↓
redirect / rewrite / continue

Also, current Next.js documentation recommends using Proxy only when simpler routing APIs aren't enough

### xiv)Internationalization (i8n)

It is used for building an application that supports multiple language/locales.

For example:

/en/products
/fr/products
/de/products

Where:

en → English
fr → French
de → German

Next.js supports the routing patterns needed for internationalized applications, but with the App Router you typically implement locale routing using a **dynamic route segment + Proxy**, rather than relying on the old Pages Router **`i18n`** configuration

### xv)Locale Detection with Proxy

You can use the user’s browser language to decide which locale to use.

For example:

Browser language = French

User visits:
example.com/products

        ↓

Proxy checks language

        ↓

Redirect

/fr/products

A simplified example:

import { NextResponse }from "next/server";

const locales = ["en", "fr", "de"];
const defaultLocale = "en";

export function proxy(request) {
  const {pathname }= request.nextUrl;

  const hasLocale = locales.some(
    (locale)=>
      pathname.startsWith(`/${locale}/`)||
      pathname=== `/${locale}`
  );

  if (hasLocale) {
    return NextResponse.next();
  }

  const url = request.nextUrl.clone();

  url.pathname= `/${defaultLocale}${pathname}`;

  return NextResponse.redirect(url);
}

export const config = {
  matcher: ["/((?!_next).*)"],
};

This is the basic idea behind locale-based routing. The official guide also demonstrates using the **`Accept-Language`** header and locale-matching libraries to select the preferred locale.

## Next.js Data Fetching

### i)Data Fetching in Next.js

Data fetching means getting data from a source such as API, Database, File, External Service etc.

Working : Next.js → API → JSON data → Display in UI

In the app router, Server Components can fetch data directly on the server.

### **Example**

```jsx
export default async function Products() {
  const response = await fetch(
    "https://api.example.com/products"
  );

  const products = await response.json();

  return (
    <ul>
      {products.map((product) => (
        <li key={product.id}>{product.name}</li>
      ))}
    </ul>
  );
}
```

Note : a server component must be async

### ii)Fetching Data from an API

An API allows your Next.js application to communicate with another service.

### **Example API response**

Suppose an API returns:

```json
[
  {
    "id": 1,
    "name": "iPhone"
  },
  {
    "id": 2,
    "name": "Samsung"
  }
]
```

You can fetch it:

```jsx
export default async function Products() {
  const res = await fetch(
    "https://api.example.com/products"
  );

  const products = await res.json();

  return (
    <div>
      {products.map((product) => (
        <h2 key={product.id}>
          {product.name}
        </h2>
      ))}
    </div>
  );
}
```

### **Error handling**

```jsx
export default async function Products() {
  const res = await fetch(
    "https://api.example.com/products"
  );

  if (!res.ok) {
    throw new Error("Failed to fetch products");
  }

  const products = await res.json();

  return (
    <div>
      {products.map((product) => (
        <h2 key={product.id}>{product.name}</h2>
      ))}
    </div>
  );
}
```

### **iii)Server Actions in Next.js**

A Server Action is an asynchronous server-side function that can be called from your application to perform server-side operations. They’re especially useful for mutation like CRUD operations.

### **iv)Data Fetching using SSG and SSR**

Two important rendering strategies you’ll hear about are SSG and SSR.

#### **Static Site Generation**

**SSG** generates a page as static HTML that can be reused for requests.

Conceptually:

```
Build time
    ↓
Generate HTML
    ↓
User requests page
    ↓
Serve generated page
```

Good for content that doesn't change frequently.

Examples:

- Blog
- Documentation
- Marketing pages

### **Example**

A page that uses static data:

```jsx
export default async function Page() {
  const res = await fetch(
    "https://api.example.com/products",
    {
      cache: "force-cache",
    }
  );

  const products = await res.json();

  return <div>{products.length} products</div>;
}
```

**`force-cache`** tells Next.js to cache the result.

#### **Static Site Regeneration**

**SSR** means generating the page on the server when a request is made.

Conceptually:

```
User request
     ↓
Server fetches latest data
     ↓
Server generates HTML
     ↓
Response
```

Good for data that needs to be fresh.

### **Example**

```jsx
export default async function Page() {
  const res = await fetch(
    "https://api.example.com/products",
    {
      cache: "no-store",
    }
  );

  const products = await res.json();

  return <div>{products.length} products</div>;
}
```

The important idea is:

```
cache: "no-store"
        ↓
Don't reuse cached response
        ↓
Fetch fresh data
```

## **Next.js Rendering**

Rendering means turning your React components into UI that can be displayed to the user.

Rendering is of two types : Server Rendering & Client Rendering 

Static Rendering — The result can be reused because the data doesn’t need to be generated for every request.

Dynamic Rendering — The result depends on request-specific or frequently changing information.

### **Server Rendering :**

They execute on the server and can be used to fetch data and access server-side resources without sending their component code to the browser in the same way a Client Component does.

### **Example**

```jsx
export default async function Products() {
  const res = await fetch(
    "https://api.example.com/products"
  );

  const products = await res.json();

  return (
    <div>
      {products.map((product) => (
        <p key={product.id}>
          {product.name}
        </p>
      ))}
    </div>
  );
}
```

Notice:

```
No "use client"
```

So this is a Server Component.

### **What can Server Components do?**

They are suitable for:

- Fetching data
- Accessing databases through server-side code
- Keeping secrets on the server
- Reducing client-side JavaScript

### **What can't they directly do?**

You can't use browser-only APIs such as:

```jsx
window
document
localStorage
```

And interactive React hooks such as:

```jsx
useState()
useEffect()
```

are Client Component features.

### **Client Component :**

Although your topic is Server Components, you need to understand their counterpart.

### **Definition**

A **Client Component** is a component that needs to run in the browser.

Add:

```jsx
"use client";
```

at the top.

### **Example**

```jsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

Why Client Component?

Because it uses:

```
useState
onClick
```

which require client-side JavaScript.

### **Remember**

```
Server Component
     ↓
Default
     ↓
Data fetching / server logic

Client Component
     ↓
"use client"
     ↓
State / events / browser APIs
```

## Edge Functions

An **Edge Function** is server-side code designed to execute close to the user geographically, depending on the hosting platform/runtime.

Conceptually:

```
User in India
     ↓
Nearby edge location
     ↓
Function
```

This can reduce network latency for suitable workloads.

### **Important**

Edge runtime has different API/runtime capabilities than Node.js, so not every Node.js package or API is available.

## **Reset Next.js Development Cache**

Sometimes Next.js behaves strangely during development:

- Old page appears
- Changes aren't reflected
- Build/cache problems
- Unexpected errors after configuration changes

You can remove the **`.next`** folder.

### **Windows**

In PowerShell:

```powershell
Remove-Item -Recurse -Force .next
```

Or simply delete the **`.next`** folder manually.

Then restart:

```bash
npm run dev
```

### **Why?**

**`.next`** contains generated Next.js build/development files.

```
.next/
   ↓
Generated cache/build output
```

Deleting it forces Next.js to regenerate those files.

### **`node_modules`?**

**Don't delete `node_modules` unless you actually have a dependency/install problem.**

If dependencies are corrupted, you can reinstall them:

```bash
rm -rf node_modules package-lock.json
npm install
```

On Windows PowerShell:

```powershell
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json
npm install
```

But for a normal cache issue:

```
Delete .next
     ↓
npm run dev
```

is usually enough.

## **Next.js Styling**

i)Add StyleSheet in Next.js (e.g. global.css)

ii)CSS Module  (e.g. .module.css)

iii)Controlling CSS Specificity with CSS Modules

iv)Tailwind CSS with Next.js

v)CSS-in-JS

vi)Sass / SCSS

## **Next.js Optimizing**

**Next.js Optimization** means improving the performance of a Next.js application so that it:

- Loads faster
- Uses less bandwidth
- Sends less JavaScript to the browser
- Loads images efficiently
- Improves user experience
- Improves SEO and Core Web Vitals

Next.js provides several built-in features for optimization.

---

## **ii. Bundle Optimization**

### **Definition**

A **bundle** is the JavaScript and other resources that are prepared for the browser.

A large bundle can cause:

```
Large JavaScript
      ↓
More download
      ↓
More processing
      ↓
Slower website
```

Therefore, we should try to keep the client-side bundle small.

### **Example**

In the App Router, components are **Server Components by default**.

```jsx
export default function Home() {
  return <h1>Hello World</h1>;
}
```

This does not require making the component a Client Component.

If we need browser-side interactivity:

```jsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

### **Remember**

```
Server Component
      ↓
Less client-side JavaScript

Client Component
      ↓
More JavaScript sent to browser
```

**Use `"use client"` only when required**, such as when using:

- **`useState`**
- **`useEffect`**
- Event handlers like **`onClick`**
- Browser APIs like **`window`** and **`localStorage`**

---

## **iii. Dynamic Imports / Lazy Loading**

### **Definition**

**Lazy loading** means loading a component only when it is needed instead of loading it as part of the initial page.

Next.js provides **`next/dynamic`** for this purpose.

### **Syntax**

```jsx
import dynamic from "next/dynamic";

const Component = dynamic(
  () => import("./Component")
);
```

### **Example**

```jsx
import dynamic from "next/dynamic";

const HeavyComponent = dynamic(
  () => import("./HeavyComponent")
);

export default function Home() {
  return (
    <div>
      <h1>Home Page</h1>

      <HeavyComponent />
    </div>
  );
}
```

### **With loading message**

```jsx
const HeavyComponent = dynamic(
  () => import("./HeavyComponent"),
  {
    loading: () => <p>Loading...</p>,
  }
);
```

### **Remember**

```
Normal import
     ↓
Loaded normally

dynamic()
     ↓
Can be loaded separately
```

Use lazy loading especially for **large or less-important components**.

---

# **iv. Image Optimization**

### **Definition**

Images can be large and can significantly affect page loading speed.

Next.js provides the **`Image` component** from **`next/image`** to optimize images.

### **Syntax**

```jsx
import Image from "next/image";

<Image
  src="/image.jpg"
  alt="Description"
  width={500}
  height={300}
/>
```

### **Example**

Place an image inside:

```
public/
└── image.jpg
```

Then:

```jsx
import Image from "next/image";

export default function Home() {
  return (
    <Image
      src="/image.jpg"
      alt="My Image"
      width={500}
      height={300}
    />
  );
}
```

### **Benefits**

Next.js Image Optimization can provide:

- Automatic image optimization
- Appropriate image sizing
- Responsive loading behavior
- Lazy loading when appropriate
- Reduced layout shift

### **Remember**

Prefer:

```jsx
<Image />
```

instead of:

```html
<img />
```

when you want Next.js image optimization.

---

# **v. Lazy Loading**

### **Definition**

**Lazy loading** means loading resources only when they are required.

For example:

```
Initial page
     ↓
Load important content
     ↓
Load heavy component later
```

### **Syntax**

```jsx
import dynamic from "next/dynamic";

const MyComponent = dynamic(
  () => import("./MyComponent")
);
```

### **Example**

```jsx
const Chart = dynamic(
  () => import("./Chart")
);

export default function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>

      <Chart />
    </div>
  );
}
```

A chart might be relatively heavy, so loading it separately can help reduce the initial JavaScript required by the page.

### **Remember**

> **Lazy loading = Load only when needed.**
> 

---

# **vi. Script Optimization**

### **Definition**

Third-party scripts such as:

- Google Analytics
- Advertising scripts
- Chat widgets
- Social media scripts

can affect website performance.

Next.js provides the **`Script`** component.

### **Syntax**

```jsx
import Script from "next/script";

<Script
  src="https://example.com/script.js"
  strategy="afterInteractive"
/>
```

### **Example**

```jsx
import Script from "next/script";

export default function Page() {
  return (
    <>
      <h1>Home Page</h1>

      <Script
        src="https://example.com/script.js"
        strategy="afterInteractive"
      />
    </>
  );
}
```

### **Common loading strategies**

```
beforeInteractive
afterInteractive
lazyOnload
```

### **Remember**

Use **`next/script`** when adding third-party scripts so that you can control when they load.

---

# **vii. Font Optimization**

### **Definition**

Fonts can affect page performance and layout.

Next.js provides **`next/font`** for optimized font loading.

### **Example**

```jsx
import { Geist } from "next/font/google";

const geist = Geist({
  subsets: ["latin"],
});

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className={geist.className}>
        {children}
      </body>
    </html>
  );
}
```

### **Benefits**

**`next/font`** helps with:

- Font optimization
- Better loading behavior
- Reduced layout shift
- Self-hosting supported fonts

### **Remember**

```
next/font
    ↓
Optimized font loading
```

---

# **viii. Static Rendering**

### **Definition**

**Static rendering** means generating reusable output that can be served without generating the page from scratch for every request.

It is useful for content that doesn't change frequently.

Examples:

- Blog pages
- Documentation
- About page
- Marketing pages

### **Example**

```jsx
export default function About() {
  return <h1>About Us</h1>;
}
```

This type of page doesn't need request-specific data.

### **Remember**

```
Static content
     ↓
Reusable output
     ↓
Fast response
```

---

# **ix. Server Components**

### **Definition**

In the Next.js App Router, **Server Components are the default**.

They allow work to be performed on the server without requiring the component itself to be a Client Component.

### **Example**

```jsx
export default async function Products() {
  const response = await fetch(
    "https://api.example.com/products"
  );

  const products = await response.json();

  return (
    <div>
      {products.map((product) => (
        <p key={product.id}>
          {product.name}
        </p>
      ))}
    </div>
  );
}
```

### **Benefits**

Server Components can help:

- Reduce client-side JavaScript
- Fetch data on the server
- Keep server-only logic away from the browser
- Improve initial page performance

### **Remember**

```
Server Component
      ↓
Runs on server
      ↓
Less unnecessary client JS
```

---

# **x. Client Components**

### **Definition**

A **Client Component** is required when a component needs browser-side functionality.

Use:

```jsx
"use client";
```

### **Example**

```jsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

### **Remember**

Use Client Components when you need:

```
useState
useEffect
onClick
onChange
window
document
localStorage
```

Avoid unnecessarily converting large parts of your application to Client Components.

---

# **xi. Static File Optimization**

### **Definition**

Static files are files that don't need to be generated dynamically.

Examples:

- Images
- PDFs
- Icons
- Videos
- Other assets

Place them inside:

```
public/
```

### **Example**

```
public/
├── logo.png
├── banner.jpg
└── document.pdf
```

Access:

```
/logo.png
/banner.jpg
/document.pdf
```

### **Example**

```jsx
import Image from "next/image";

export default function Home() {
  return (
    <Image
      src="/logo.png"
      alt="Logo"
      width={200}
      height={100}
    />
  );
}
```

### **Remember**

Don't write:

```
/public/logo.png
```

Use:

```
/logo.png
```

The **`public`** directory itself is not included in the URL.

---

# **xii. Minification and Production Optimization**

### **Definition**

During a production build, Next.js optimizes the application for deployment.

Create a production build using:

```bash
npm run build
```

Then run it:

```bash
npm start
```

### **Development vs Production**

```
npm run dev
     ↓
Development
     ↓
Debugging + Hot Reload
```

```
npm run build
     ↓
Production build
     ↓
Optimized application
```

### **Remember**

Don't judge final production performance only from:

```bash
npm run dev
```

Always test the production build when performance matters.

---

# **xiii. Avoid Unnecessary Dependencies**

### **Definition**

Every additional package can potentially increase:

- Installation size
- Build complexity
- Client-side JavaScript
- Maintenance

### **Example**

Instead of installing a large library for a very simple operation:

```jsx
// Simple operation
const total = price * quantity;
```

don't automatically add a package just to perform that operation.

### **Remember**

> Use dependencies when they provide meaningful value, not simply because they exist.
> 

---

# **xiv. Bundle Optimization — Summary**

The main goal is:

```
Less unnecessary JavaScript
          ↓
Less downloading
          ↓
Less browser processing
          ↓
Better performance
```

Important techniques:

```
i. Use Server Components
ii. Minimize Client Components
iii. Use dynamic imports
iv. Optimize images
v. Optimize fonts
vi. Optimize third-party scripts
vii. Avoid unnecessary dependencies
```

# **xv. Core Optimization Tools**

| **Feature** | **Next.js Tool** |
| --- | --- |
| Image optimization | **`next/image`** |
| Font optimization | **`next/font`** |
| Script optimization | **`next/script`** |
| Lazy loading | **`next/dynamic`** |
| Server rendering | Server Components |
| Client interactivity | **`"use client"`** |
| Static assets | **`public/`** |
| Production optimization | **`next build`** |

### **1. Next.js Configuring**

#### **What is Next.js configuration?**

Next.js configuration allows developers to customize the behavior of a Next.js application. Configuration is usually managed through the **`next.config.js`**, **`next.config.mjs`**, or **`next.config.ts`** file in the project root.

#### **Common configuration options**

- **`reactStrictMode`**: Enables React Strict Mode checks during development.
- **`images`**: Configures image optimization and allowed remote image sources.
- **`redirects()`**: Redirects users from one URL to another.
- **`rewrites()`**: Maps one URL to another without changing the browser's URL.
- **`headers()`**: Adds custom HTTP response headers.
- **`basePath`**: Runs the application under a specified URL prefix.
- **`output`**: Controls the build output, such as standalone deployment or static export.

#### **Example**

js

```
/**@type{import('next').NextConfig} */constnextConfig= {  reactStrictMode:true,  poweredByHeader:false,};module.exports= nextConfig;
```

#### **Important points**

Configuration changes generally require restarting the development server. The configuration file is different from environment variables, which store values such as API URLs and secrets.

### **2. Next.js TypeScript**

#### **What is TypeScript?**

TypeScript is a programming language built on JavaScript that adds static type checking. Next.js supports TypeScript directly, helping developers identify errors before running their applications.

#### **Setting up TypeScript**

Create a Next.js project with TypeScript:

bash

```
npx create-next-app@latest my-app --typescript
```

For an existing JavaScript project, create a **`tsconfig.json`** file or start the development server and follow Next.js's setup instructions.

#### **Typing component props**

tsx

```
typeUserProps= {name:string;age:number;};exportdefaultfunctionUser({ name, age }: UserProps){return (    <p>{name} is{age} years old.    </p>  );}
```

#### **Typing state and events**

tsx

```
"use client";import { useState }from"react";exportdefaultfunctionCounter(){const [count,setCount]=useState<number>(0);return (    <buttononClick={()=>setCount(count+1)}>      Count:{count}    </button>  );}
```

#### **Important points**

TypeScript improves code readability, autocomplete, maintainability, and error detection. Next.js supports TypeScript for components, route handlers, configuration, and API data. Type checking does not automatically validate untrusted data at runtime.

### **3. Next.js Environment Variables**

#### **What are environment variables?**

Environment variables store configuration values outside the application source code. They are useful for database URLs, API keys, authentication secrets, and deployment settings.

Next.js loads environment variables from **`.env`** files in the project root.

#### **Common environment files**

- **`.env`**: Default environment variables.
- **`.env.local`**: Local overrides, commonly used for private development settings.
- **`.env.development`**: Development-specific variables.
- **`.env.production`**: Production-specific variables.
- **`.env.test`**: Test-specific variables.

#### **Defining and accessing variables**

Example **`.env.local`**:

env

```
DATABASE_URL="your-database-url"
AUTH_SECRET="your-secret"
NEXT_PUBLIC_API_URL="https://api.example.com"
```

Access variables on the server:

ts

```
constdatabaseUrl= process.env.DATABASE_URL;
```

Access a variable intended for browser use:

ts

```
constapiUrl= process.env.NEXT_PUBLIC_API_URL;
```

#### **Important security rules**

Variables prefixed with **`NEXT_PUBLIC_`** can be exposed to browser code and are generally inlined at build time. Never put passwords, private API keys, database credentials, or authentication secrets in public variables.

Add sensitive **`.env`** files to **`.gitignore`**, and configure production secrets through your hosting provider.

### **4. MDX in Next.js**

#### **What is MDX?**

MDX combines Markdown with JSX, allowing developers to write content using Markdown syntax while embedding React components. It is useful for blogs, documentation, tutorials, and content-heavy websites.

#### **Installing MDX support**

bash

```
npm install @next/mdx @mdx-js/loader @mdx-js/react @types/mdx
```

Configure MDX in **`next.config.mjs`**:

js

```
import createMDXfrom"@next/mdx";constwithMDX=createMDX({  extension: /\.mdx?$/,});exportdefaultwithMDX({pageExtensions: ["js","jsx","ts","tsx","md","mdx"],});
```

Additional setup, such as an **`mdx-components.tsx`** file, may be required for App Router projects.

#### **Example MDX content**

mdx

```
# My Article

This is a paragraph written in Markdown.

<MyButton />
```

Here, **`MyButton`** is a React component that can be rendered inside the MDX document.

#### **Benefits of MDX**

MDX supports readable content, reusable components, code examples, and consistent styling. However, MDX should be treated as trusted code because it can execute JavaScript through embedded components.

### **5. Next.js `src` Directory**

#### **What is the `src` directory?**

The **`src/`** directory provides an optional way to organize application source code separately from root-level configuration files.

For example:

text

```
my-app/
├── public/
├── src/
│   ├── app/
│   │   ├── page.tsx
│   │   └── layout.tsx
│   ├── components/
│   └── lib/
├── next.config.ts
├── package.json
└── tsconfig.json
```

#### **Purpose of the directory**

- **`src/app/`**: Contains App Router pages, layouts, and route handlers.
- **`src/components/`**: Stores reusable UI components.
- **`src/lib/`**: Contains utility functions, database clients, and shared logic.
- **`public/`**: Stores static assets served from the root URL.

#### **Important points**

Using **`src/`** is optional. Next.js supports either an **`app/`** directory at the project root or **`src/app/`**. If both root-level **`app/`** and **`src/app/`** exist, the root-level **`app/`** directory takes precedence.

Configuration files such as **`next.config.ts`** and **`package.json`** remain at the project root.

### **6. Draft Mode in Next.js**

#### **What is Draft Mode?**

Draft Mode allows a Next.js website to display unpublished content from a CMS. It is useful when content editors need to preview drafts before publishing them.

In the App Router, Draft Mode is managed through **`draftMode()`** from **`next/headers`**.

#### **Enabling Draft Mode**

A route handler can validate a preview request and enable Draft Mode.

ts

```
// app/api/draft/route.tsimport { draftMode }from"next/headers";import { NextResponse }from"next/server";exportasyncfunctionGET(request:Request) {const {searchParams }=newURL(request.url);constsecret= searchParams.get("secret");if (secret!== process.env.DRAFT_SECRET) {returnnewNextResponse("Invalid token", {      status:401,    });  }constdraft=awaitdraftMode();  draft.enable();return NextResponse.redirect(newURL("/", request.url)  );}
```

This is a simplified example. A production implementation should also validate the requested preview path and use a sufficiently strong secret.

#### **Checking Draft Mode**

tsx

```
import { draftMode }from"next/headers";exportdefaultasyncfunctionPage(){const {isEnabled }=awaitdraftMode();return (    <main>{isEnabled?"Draft preview enabled":"Published content"}    </main>  );}
```

#### **Important points**

Draft Mode allows pages to fetch draft content instead of published content. The CMS integration must support preview queries. Protect preview endpoints carefully, because unauthorized access could expose unpublished information.

### **7. Next.js Security Headers**

#### **What are security headers?**

Security headers are HTTP response headers that instruct browsers how to handle a website securely. They help protect applications against attacks such as cross-site scripting (XSS), clickjacking, and insecure resource loading.

#### **Common security headers**

- **`Content-Security-Policy (CSP)`**: Restricts which sources can load scripts, styles, images, and other resources.
- **`X-Frame-Options`**: Helps prevent a website from being embedded in unauthorized frames.
- **`X-Content-Type-Options`**: Prevents browsers from guessing content types; commonly set to **`nosniff`**.
- **`Referrer-Policy`**: Controls how much referrer information is sent to other websites.
- **`Strict-Transport-Security (HSTS)`**: Instructs browsers to use HTTPS for future requests.
- **`Permissions-Policy`**: Controls access to browser features such as the camera and microphone.

#### **Configuring security headers**

Example in **`next.config.js`**:

js

```
/**@type{import('next').NextConfig} */constnextConfig= {asyncheaders() {return [      {        source:"/:path*",        headers: [          {            key:"X-Content-Type-Options",            value:"nosniff",          },          {            key:"X-Frame-Options",            value:"DENY",          },          {            key:"Referrer-Policy",            value:"strict-origin-when-cross-origin",          },        ],      },    ];  },};module.exports= nextConfig;
```

#### **Important points**

Security headers should be selected according to application requirements. A strict Content Security Policy may require additional configuration for scripts, styles, and nonces. HSTS should only be enabled when the website is correctly configured for HTTPS.

### **8. Unit Testing in Next.js**

#### **What is unit testing?**

Unit testing checks individual functions or components in isolation to verify that they behave as expected.

For Next.js projects, common testing tools include Jest, Vitest, React Testing Library, and other compatible testing frameworks.

#### **Installing testing dependencies**

For a Jest-based setup, install the relevant packages:

bash

```
npm install -D jest jest-environment-jsdom \
  @testing-library/react \
  @testing-library/dom \
  @testing-library/jest-dom \
  @testing-library/user-event
```

Next.js also provides setup guidance and templates for Jest. Follow the configuration appropriate to your project and installed versions.

#### **Example component**

tsx

```
exportdefaultfunctionGreeting(){return <h1>Hello, Next.js!</h1>;}
```

#### **Example unit test**

tsx

```
import { render, screen }from"@testing-library/react";import Greetingfrom"./Greeting";test("renders the greeting", ()=> {render(<Greeting />);expect(    screen.getByRole("heading", {      name:"Hello, Next.js!",    })  ).toBeInTheDocument();});
```

#### **Running tests**

bash

```
npm test
```

The command depends on the test script configured in **`package.json`**.

#### **Important points**

Unit tests help identify bugs early and make refactoring safer. Test pure functions, components, and utility logic separately. Server Components, async components, route handlers, and end-to-end user flows may require additional testing strategies.

### **9. Implement User Authentication in Next.js with Auth.js**

#### **What is Auth.js?**

Auth.js is an authentication solution for web applications, including Next.js. It supports authentication providers, session management, and integrations with different identity systems.

Authentication verifies who a user is. Authorization determines what that user is allowed to access.

#### **Installing Auth.js**

bash

```
npm install next-auth@beta
```

The exact installation command and API depend on the Auth.js version used in the project.

#### **Configuring authentication**

Create an authentication configuration file, such as **`auth.ts`**:

ts

```
import NextAuthfrom"next-auth";import GitHubfrom"next-auth/providers/github";exportconst {handlers,auth,signIn,signOut }=NextAuth({    providers: [GitHub],  });
```

This example uses GitHub as an OAuth provider. Configure the corresponding provider credentials through environment variables.

#### **Creating the authentication route**

Create **`app/api/auth/[...nextauth]/route.ts`**:

ts

```
import { handlers }from"@/auth";exportconst {GET,POST }= handlers;
```

The route allows Auth.js to process authentication-related requests.

#### **Accessing the session**

tsx

```
import { auth }from"@/auth";exportdefaultasyncfunctionPage(){constsession=awaitauth();if (!session?.user) {return <p>Please sign in to continue.</p>;  }return <p>Welcome,{session.user.name}!</p>;}
```

#### **Protecting application resources**

- Check the session on the server before returning protected data.
- Enforce authorization in server actions, route handlers, and database queries.
- Use middleware or proxy-based checks where appropriate, but do not rely on redirects alone for security.
- Store provider credentials and authentication secrets in environment variables.
- Use HTTPS in production and configure callback URLs correctly.

#### **Important points**

Authentication should be verified on the server for every sensitive operation. Hiding a page or button in the UI does not prevent unauthorized API or database access. The exact Auth.js APIs may vary by version.

### **10. Next.js Deploying**

#### **What is deployment?**

Deployment is the process of making a Next.js application available to users through a production server or hosting platform.

Next.js applications can be deployed to managed hosting services, Node.js servers, Docker containers, or static hosting platforms, depending on the features used.

#### **Preparing for deployment**

Before deploying, check that:

- The application builds successfully.
- Environment variables are configured.
- Authentication callback URLs are correct.
- Database access and production credentials are configured.
- Images, fonts, and other assets load correctly.
- Security headers and HTTPS are configured.
- Error handling and logging are in place.

#### **Production build commands**

bash

```
npm run build
npm run start
```

The first command builds the application. The second starts the production server when the project's scripts are configured accordingly.

#### **Common deployment methods**

- Managed hosting: Simplifies builds, deployments, and scaling.
- Node.js server: Runs the Next.js production server.
- Docker: Packages the application and its runtime dependencies.
- Static hosting: Serves exported HTML, CSS, JavaScript, and assets when the app supports static export.

#### **Important points**

Not every Next.js application can run as a purely static website. Features such as request-time rendering, server actions, and server-side authentication may require a compatible server or platform.

### **11. Deploying Your Next.js App**

#### **Deploying to a hosting platform**

A typical deployment workflow involves connecting a repository to a hosting provider, configuring build settings, and publishing the application.

#### **Deployment steps**

1. Push the project to a Git repository.
2. Connect the repository to your hosting platform.
3. Configure the build command, usually **`npm run build`**.
4. Configure environment variables for the production environment.
5. Deploy the application.
6. Test the deployed website, including authentication, APIs, images, and database operations.

#### **Example project scripts**

json

```
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "eslint ."
  }
}
```

This is an illustrative configuration. The available scripts depend on the project and the Next.js version.

#### **Common deployment problems**

- Missing environment variables.
- Incorrect production API URLs.
- Build errors caused by TypeScript or imports.
- Database connection failures.
- Incorrect OAuth callback URLs.
- Caching problems or incorrect image configuration.
- Unsupported server features on static hosting.

#### **Important points**

Test the production build before deployment. Keep development and production environment settings separate, and avoid committing secrets to version control.

### **12. Next.js Static HTML Export**

#### **What is static export?**

Static export generates HTML files and other static assets during the build process. These files can be hosted on a static web server or content delivery network without running a Next.js server for each request.

#### **Enabling static export**

Configure **`next.config.ts`**:

ts

```
importtype { NextConfig }from"next";constnextConfig:NextConfig= {  output:"export",};exportdefaultnextConfig;
```

Build the application:

bash

```
npm run build
```

The exported site is generally generated in the **`out/`** directory.

#### **Advantages**

- Can be hosted on static hosting platforms.
- Does not require a continuously running Next.js server.
- Can provide fast page delivery through a CDN.
- Reduces server runtime requirements.

#### **Limitations**

Features requiring request-time server execution are not available in a pure static export. Examples include request-dependent server rendering, server actions, and the default server-based image optimization service.

Dynamic routes generally need to be generated at build time, and routes must be compatible with static export.

#### **Important points**

Static export is suitable for documentation sites, portfolios, and content that can be generated at build time. Choose a regular server deployment when the application requires runtime server features.

### **13. Migrating from Create React App to Next.js: A Practical Guide**

#### **What is the difference?**

Create React App (CRA) is a React project setup tool that commonly produces client-rendered single-page applications. Next.js adds routing conventions, server rendering, static generation, and other full-stack capabilities.

#### **Key differences**

- CRA commonly uses React Router or another routing library; Next.js provides file-system-based routing.
- CRA typically renders pages in the browser; Next.js supports server rendering and static generation.
- Next.js has built-in image optimization and font integration.
- Next.js supports server components, route handlers, and server-side data access.
- Environment variable conventions differ between the two systems.

#### **Migration steps**

1. Create a new Next.js project.
2. Move reusable React components into the new project.
3. Move static assets into the **`public/`** directory where appropriate.
4. Replace React Router routes with Next.js route files.
5. Move data fetching to suitable Server Components or client-side components.
6. Update environment variable names.
7. Review browser-only APIs and client-side dependencies.
8. Test routing, forms, authentication, and API calls.
9. Build and deploy the application.

#### **Example route conversion**

A CRA application might use:

jsx

```
<Route path="/about" element={<About />} />
```

In the Next.js App Router, create:

text

```
app/
└── about/
    └── page.tsx
```

The **`page.tsx`** file exports the page component for the **`/about`** route.

#### **Environment variable differences**

CRA typically uses variables prefixed with **`REACT_APP_`** for browser exposure. Next.js uses **`NEXT_PUBLIC_`** for variables exposed to client-side code.

For example, **`REACT_APP_API_URL`** may become **`NEXT_PUBLIC_API_URL`**.

#### **Important points**

Migration is not just a file-renaming exercise. Review routing, data fetching, rendering behavior, environment variables, and dependencies carefully. Components using state, effects, or browser-only APIs may need the **`"use client"`** directive in the App Router.

### **14. Next.js Components**

#### **What are components?**

Components are reusable building blocks of a user interface. In Next.js, components can represent buttons, navigation bars, forms, cards, layouts, and complete page sections.

#### **Creating a component**

tsx

```
exportdefaultfunctionWelcome(){return <h2>Welcome to Next.js</h2>;}
```

Use it inside another component:

tsx

```
import Welcomefrom"@/components/Welcome";exportdefaultfunctionPage(){return <Welcome />;}
```

#### **Server Components**

In the App Router, components are Server Components by default. They can fetch data on the server, access server-only resources, and reduce the amount of JavaScript sent to the browser.

#### **Client Components**

Client Components are used when a component needs state, event handlers, effects, or browser APIs.

tsx

```
"use client";import { useState }from"react";exportdefaultfunctionToggle(){const [visible,setVisible]=useState(false);return (    <buttononClick={()=>setVisible(!visible)}>{visible?"Hide":"Show"}    </button>  );}
```

#### **Props and reusability**

Props allow components to receive data from their parent components. Reusable components improve consistency and reduce duplicated code.

#### **Important points**

Use Server Components by default and add **`"use client"`** only when interactive client-side behavior is required. Keep sensitive server-only logic out of client bundles.

### **15. Fonts in Next.js**

#### **What is font optimization?**

Next.js provides the **`next/font`** module to optimize font loading. It supports local fonts and Google Fonts and can reduce layout shifts by managing font loading.

#### **Using a Google Font**

tsx

```
import { Inter }from"next/font/google";constinter=Inter({  subsets: ["latin"],  display:"swap",});exportdefaultfunctionRootLayout({  children,}: {  children: React.ReactNode;}){return (    <htmllang="en">      <bodyclassName={inter.className}>{children}      </body>    </html>  );}
```

#### **Using a local font**

tsx

```
import localFontfrom"next/font/local";constmyFont=localFont({  src:"./fonts/my-font.woff2",});
```

Apply the font's generated class name to the relevant element.

#### **Advantages**

- Fonts can be self-hosted and optimized.
- External font requests can be reduced.
- Font loading behavior can be controlled.
- Layout shifts caused by font changes can be reduced.

#### **Important points**

Google Fonts are generally downloaded during the build and served from the application when using **`next/font/google`**. Ensure the build environment can access the font source when required. For local fonts, verify that file paths are correct.

### **16. Next.js File Conventions**

#### **What are file conventions?**

Next.js uses specific file and folder names to determine how routes, layouts, loading states, errors, and other application features work.

#### **Common App Router files**

- **`page.tsx`**: Defines a route's UI.
- **`layout.tsx`**: Defines a shared layout.
- **`template.tsx`**: Defines a layout-like wrapper that remounts when appropriate navigation occurs.
- **`loading.tsx`**: Defines a loading UI.
- **`error.tsx`**: Defines an error boundary for a route segment.
- **`not-found.tsx`**: Defines a not-found UI.
- **`route.ts`**: Defines an HTTP route handler.
- **`default.tsx`**: Defines a fallback UI for an unmatched parallel route slot.
- **`generateMetadata`**: Generates metadata for a page or layout.
- **`generateStaticParams`**: Supplies dynamic route parameters for static generation.

#### **Example folder structure**

text

```
app/
├── layout.tsx
├── page.tsx
├── loading.tsx
├── not-found.tsx
├── blog/
│   ├── page.tsx
│   └── [slug]/
│       └── page.tsx
└── api/
    └── users/
        └── route.ts
```

#### **Dynamic routes**

Folders such as **`[slug]`** create dynamic route segments. For example, **`app/blog/[slug]/page.tsx`** can handle routes such as **`/blog/nextjs`**.

#### **Important points**

File conventions reduce the need for manual routing configuration. Special files must be placed in the appropriate route segment, and their behavior depends on whether the project uses the App Router or Pages Router.

### **17. File Conventions in Next.js**

#### **Route-related conventions**

Next.js determines which UI to render based on the folder structure inside **`app/`**.

For example:

text

```
app/
├── page.tsx
├── about/
│   └── page.tsx
└── contact/
    └── page.tsx
```

This structure creates the **`/`**, **`/about`**, and **`/contact`** routes.

#### **Special-purpose conventions**

- **`page.tsx`** makes a route publicly accessible.
- **`layout.tsx`** wraps pages and nested layouts.
- **`template.tsx`** creates a new component instance when its segment is navigated.
- **`loading.tsx`** displays a loading fallback.
- **`error.tsx`** handles rendering errors within a route segment.
- **`not-found.tsx`** renders not-found UI.
- **`route.ts`** handles HTTP requests without rendering a page component.

#### **Private folders and route groups**

A folder beginning with an underscore, such as **`_components`**, is a private folder convention and is excluded from routing.

A folder wrapped in parentheses, such as **`(dashboard)`**, groups routes without adding that folder name to the URL.

#### **Important points**

File and folder naming directly influences application routing and behavior. Use route groups for organization and private folders for implementation details that should not become routes.

### **18. Next.js File Conventions: `default.js`**

#### **What is `default.js`?**

In the App Router, **`default.js`** provides a fallback UI for a parallel route slot when Next.js cannot recover a matching slot during certain navigation scenarios, especially on a full page load.

Parallel routes are created using named folders beginning with **`@`**, such as **`@analytics`** or **`@team`**.

#### **Example folder structure**

text

```
app/
├── layout.tsx
├── page.tsx
└── @analytics/
    ├── page.tsx
    └── default.tsx
```

#### **Example implementation**

tsx

```
exportdefaultfunctionDefault(){returnnull;}
```

This example renders nothing when the fallback is used.

#### **Why is it useful?**

Parallel routes can display multiple sections of a page independently. A default file provides fallback behavior when a slot does not have a matching route available.

#### **Important points**

**`default.js`** is different from **`page.js`**. A page file defines route UI, whereas a default file provides fallback UI for a parallel route slot. It is also different from **`default export`**, which is JavaScript syntax used to export a module's main value.

### **19. Next.js Layouts**

#### **What are layouts?**

Layouts define shared UI that is reused across multiple pages. They are useful for navigation bars, headers, footers, sidebars, and common page structures.

#### **Root layout**

The root layout is required in the App Router and must define the **`<html>`** and **`<body>`** elements.

tsx

```
exportdefaultfunctionRootLayout({  children,}: {  children: React.ReactNode;}){return (    <htmllang="en">      <body>        <header>My Website</header>{children}        <footer>Copyright 2026</footer>      </body>    </html>  );}
```

#### **Nested layouts**

A nested **`layout.tsx`** applies to routes inside its folder.

text

```
app/
├── layout.tsx
└── dashboard/
    ├── layout.tsx
    └── page.tsx
```

The dashboard layout wraps dashboard pages while the root layout remains shared.

#### **Benefits of layouts**

- Reuse common UI.
- Maintain a consistent page structure.
- Preserve shared layout state across many navigations.
- Organize different sections of an application.

#### **Important points**

Layouts are Server Components by default and preserve their state during navigation when reused. They do not automatically receive the current pathname as a prop. Use client-side navigation hooks where appropriate if the pathname is needed.

### **20. `loading.js` in Next.js**

#### **What is `loading.js`?**

**`loading.js`** or **`loading.tsx`** defines a loading UI for a route segment in the App Router. Next.js uses it to show a fallback while the relevant route content is loading.

#### **Example implementation**

tsx

```
exportdefaultfunctionLoading(){return <p>Loading, please wait...</p>;}
```

#### **Folder structure**

text

```
app/
├── blog/
│   ├── loading.tsx
│   └── page.tsx
```

The loading UI is associated with the **`/blog`** route segment and its descendants, subject to the route's layout and rendering structure.

#### **Benefits**

- Improves perceived performance.
- Provides immediate feedback during navigation.
- Works with React Suspense.
- Helps users understand that content is being loaded.

#### **Important points**

A loading file is a special convention, not a regular page route. It is useful for async data fetching and streaming, but it does not replace proper error handling or data-loading logic.

### **21. Next.js File Conventions: `not-found.js`**

#### **What is `not-found.js`?**

**`not-found.js`** or **`not-found.tsx`** defines the UI displayed when a resource or route cannot be found. In the App Router, it can be used with the **`notFound()`** function.

#### **Example implementation**

tsx

```
exportdefaultfunctionNotFound(){return (    <main>      <h2>Page Not Found</h2>      <p>The requested page could not be found.</p>    </main>  );}
```

#### **Using `notFound()`**

tsx

```
import { notFound }from"next/navigation";exportdefaultasyncfunctionProductPage(){constproduct=awaitgetProduct();if (!product) {notFound();  }return <h1>{product.name}</h1>;}
```

In this example, **`getProduct()`** represents a data-fetching function defined elsewhere.

#### **Benefits**

- Provides a user-friendly missing-page experience.
- Handles unavailable resources.
- Keeps error UI consistent with the site's design.
- Helps distinguish missing resources from unexpected server errors.

#### **Important points**

Calling **`notFound()`** terminates rendering of the relevant route segment and displays the nearest applicable not-found UI. A root-level **`not-found.tsx`** can also handle unmatched URLs. Exact status-code behavior can depend on the rendering and streaming context.

### **22. Next.js File Conventions: `route.js`**

#### **What is `route.js`?**

**`route.js`** or **`route.ts`** defines a Route Handler in the App Router. It allows a Next.js application to respond to HTTP requests such as GET, POST, PUT, PATCH, and DELETE.

#### **Example GET handler**

ts

```
import { NextResponse }from"next/server";exportasyncfunctionGET() {return NextResponse.json({    message:"Hello from Next.js",  });}
```

#### **Example POST handler**

ts

```
import { NextResponse }from"next/server";exportasyncfunctionPOST(request:Request) {constbody=await request.json();return NextResponse.json({    received: body,  });}
```

#### **Example folder structure**

text

```
app/
└── api/
    └── users/
        └── route.ts
```

This handler responds at **`/api/users`**.

#### **Common uses**

- Creating API endpoints.
- Receiving form or JSON data.
- Handling webhooks.
- Processing authentication callbacks.
- Returning JSON or other HTTP responses.

#### **Important points**

Route Handlers are different from page components. A **`route.ts`** file handles HTTP requests, whereas **`page.tsx`** renders UI. Protect sensitive operations with authentication, authorization, input validation, and appropriate HTTP status codes.

### **23. `template.js` in Next.js**

#### **What is `template.js`?**

**`template.js`** or **`template.tsx`** is a special App Router file similar to **`layout.js`**, but it creates a new component instance when its route segment is navigated in situations where the template is reused.

#### **Example implementation**

tsx

```
exportdefaultfunctionTemplate({  children,}: {  children: React.ReactNode;}){return <section>{children}</section>;}
```

#### **Layout versus template**

- A layout persists across navigation when the same layout is reused.
- A template is remounted when navigation enters its segment again.
- Remounting resets local component state and reruns mount-related effects.
- Templates can be useful for animations, entry transitions, and navigation-specific UI behavior.

#### **Example folder structure**

text

```
app/
├── layout.tsx
└── dashboard/
    ├── template.tsx
    └── page.tsx
```

#### **Important points**

Use layouts for persistent shared UI and templates when a fresh component instance is desired during navigation. Templates are not a replacement for every layout, because remounting can reset state unnecessarily.

### **24. Metadata Files in Next.js**

#### **What are metadata files?**

Metadata files allow developers to define information about a page, including its title, description, favicon, Open Graph images, and other information used by browsers and social media platforms.

Next.js supports metadata through configuration files and the Metadata API.

#### **Common metadata files**

- **`favicon.ico`**: Defines the website's favicon.
- **`icon.png`** or **`icon.svg`**: Provides application icons.
- **`apple-icon.png`**: Provides an icon for Apple devices.
- **`opengraph-image.png`**: Defines an Open Graph image for link previews.
- **`twitter-image.png`**: Defines an image for Twitter/X-style social previews.
- **`robots.txt`**: Provides crawling instructions for search engines.
- **`sitemap.xml`**: Provides a list of URLs for search engines.

These files can be placed in the appropriate **`app/`** directory locations. Next.js also supports special file-based conventions for generating some metadata dynamically.

### **Defining metadata**

tsx

```
importtype { Metadata }from"next";exportconstmetadata:Metadata= {  title:"My Website",  description:"Learn about my website.",};exportdefaultfunctionRootLayout({  children,}: {  children: React.ReactNode;}){return (    <htmllang="en">      <body>{children}</body>    </html>  );}
```

### **Benefits**

- Improves search result presentation.
- Creates better social sharing previews.
- Provides meaningful browser tab titles.
- Helps search engines understand page content.

### **Important points**

Static metadata can be exported through **`metadata`**, while dynamic metadata can be generated through **`generateMetadata()`**. These exports are supported in Server Components, not Client Components.

# **Next.js Functions: `generateMetadata`, `generateStaticParams`, and ESLint**

These are important Next.js concepts for building SEO-friendly pages, generating routes efficiently, and maintaining code quality. Here's how each works, with examples using the **App Router**.

## **1. `generateMetadata` in Next.js**

**`generateMetadata`** is a function used to define a page's metadata, such as its title, description, and social sharing information.

It is useful when metadata needs to be generated dynamically based on route parameters or data fetched from an API.

### **Static metadata**

Use the **`metadata`** object when the metadata doesn't change dynamically.

tsx

```
// app/about/page.tsximporttype { Metadata }from'next'exportconstmetadata:Metadata= {  title:'About Us',  description:'Learn more about our company.',}exportdefaultfunctionAboutPage(){return <h1>About Us</h1>}
```

### **Dynamic metadata with `generateMetadata`**

tsx

```
// app/products/[id]/page.tsximporttype { Metadata }from'next'typeProps= {params:Promise<{id:string }>}exportasyncfunctiongenerateMetadata(  {params }:Props):Promise<Metadata> {const {id }=await paramsreturn {    title:`Product ${id}`,    description:`Learn more about product ${id}.`,  }}exportdefaultasyncfunctionProductPage({  params,}: Props){const {id }=await paramsreturn <h1>Product{id}</h1>}
```

For current App Router versions, **`params`** is a promise, so you should **`await`** it. Older Next.js versions may use synchronous **`params`**.

### **Common metadata properties**

| **Property** | **Purpose** |
| --- | --- |
| **`title`** | Page title displayed in browser tabs and search results |
| **`description`** | Summary of the page |
| **`openGraph`** | Metadata for social sharing previews |
| **`twitter`** | Metadata for X/Twitter sharing cards |
| **`robots`** | Search engine crawling and indexing instructions |
| **`alternates`** | Canonical URLs and alternate language URLs |

Example:

tsx

```
exportconstmetadata= {  title:'My Blog',  description:'Articles about web development.',  openGraph: {    title:'My Blog',    description:'Read our latest articles.',    url:'https://example.com/blog',    type:'website',  },}
```

**Important rules:**

- **`metadata`** and **`generateMetadata`** are supported in Server Components, not Client Components.
- Use **`generateMetadata`** when the metadata depends on dynamic data.
- Avoid defining both **`metadata`** and **`generateMetadata`** in the same route segment.
- Metadata can be inherited and merged from parent layouts.

Official reference: Next.js **`generateMetadata`** documentation .

[](https://www.google.com/s2/favicons?domain=https://nextjs.org&sz=32)

Next.js

## **2. `generateStaticParams` in Next.js**

**`generateStaticParams`** is used to pre-generate pages for dynamic routes at build time. It is especially useful for blogs, product pages, documentation sites, and category pages.

For example, a route such as:

text

```
app/blog/[slug]/page.tsx
```

can generate URLs like **`/blog/nextjs-basics`** and **`/blog/react-guide`**.

### **Example: Generate static blog pages**

tsx

```
// app/blog/[slug]/page.tsxconstposts= [  { slug:'nextjs-basics', title:'Next.js Basics' },  { slug:'react-guide', title:'React Guide' },]exportfunctiongenerateStaticParams() {return posts.map((post)=> ({    slug: post.slug,  }))}exportdefaultasyncfunctionBlogPost({  params,}: {  params: Promise<{ slug:string }>}){const {slug }=await paramsconstpost= posts.find((item)=> item.slug=== slug)if (!post) {return <h1>Post not found</h1>  }return <h1>{post.title}</h1>}
```

During the build, Next.js can generate these routes:

- **`/blog/nextjs-basics`**
- **`/blog/react-guide`**

The function must return an array of objects whose keys match the dynamic route segments.

[](https://www.google.com/s2/favicons?domain=https://nextjs.org&sz=32)

Next.js

### **Fetch routes from an API**

tsx

```
exportasyncfunctiongenerateStaticParams() {constresponse=awaitfetch('https://api.example.com/posts'  )constposts=await response.json()return posts.map((post: {slug:string })=> ({    slug: post.slug,  }))}
```

In this example, each post's **`slug`** determines a route to pre-generate.

### **Control which routes are generated**

**Option A: Generate every known route at build time.**

Return all the required parameters from **`generateStaticParams`**.

**Option B: Generate only selected routes at build time.**

tsx

```
exportconstdynamicParams=trueexportasyncfunctiongenerateStaticParams() {return [{ slug:'nextjs-basics' }]}
```

With **`dynamicParams = true`**, routes that were not generated at build time can still be rendered on demand, subject to the route's rendering and caching configuration.

To return a 404 for paths that were not generated, use:

tsx

```
exportconstdynamicParams=false
```

### **Important rules**

- **`generateStaticParams`** replaces **`getStaticPaths`** from the older Pages Router.
- It runs during **`next build`** before the relevant pages are generated.
- It is not rerun during ISR revalidation.
- It can be used with dynamic pages, layouts, and supported route handlers.
- If you need to generate all pages at runtime rather than at build time, an empty array is an option in applicable configurations. Cache Components has additional requirements.

Official reference: Next.js **`generateStaticParams`** documentation .

[](https://www.google.com/s2/favicons?domain=https://nextjs.org&sz=32)

Next.js

## **3. ESLint in Next.js**

ESLint is a JavaScript and TypeScript linting tool that identifies potential bugs, coding mistakes, and problematic patterns before they become production issues.

Next.js provides **`eslint-config-next`**, which includes recommended rules for Next.js, React, and React Hooks.

[](https://www.google.com/s2/favicons?domain=https://nextjs.org&sz=32)

Next.js

### **Install ESLint**

For an existing Next.js project:

bash

```
npm install -D eslint eslint-config-next
```

### **Configure ESLint**

Create an **`eslint.config.mjs`** file in your project root.

js

```
import { defineConfig, globalIgnores }from'eslint/config'import nextVitalsfrom'eslint-config-next/core-web-vitals'consteslintConfig=defineConfig([...nextVitals,globalIgnores(['.next/**','out/**','build/**','next-env.d.ts',  ]),])exportdefaulteslintConfig
```

This configuration enables Next.js Core Web Vitals rules, which highlight issues that may affect performance and user experience.

### **Run ESLint**

bash

```
npx eslint .
```

To automatically fix supported issues:

bash

```
npx eslint . --fix
```

You can also add scripts to your **`package.json`**:

json

```
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

Then run:

bash

```
npm run lint
```

**Important for Next.js 16:** The **`next lint`** command has been removed. Use the ESLint CLI directly, and run linting explicitly because **`next build`** no longer runs ESLint automatically.

[](https://www.google.com/s2/favicons?domain=https://nextjs.org&sz=32)

Next.js

+1

### **Common ESLint rules in Next.js**

| **Rule** | **What it helps prevent** |
| --- | --- |
| **`@next/next/no-img-element`** | Use of plain **`<img>`** instead of optimized **`next/image`** |
| **`@next/next/no-html-link-for-pages`** | Plain anchors for internal page navigation where **`next/link`** is appropriate |
| **`@next/next/no-async-client-component`** | Async Client Components |
| React Hooks rules | Incorrect hook usage and dependency issues |
| Core Web Vitals rules | Common performance-related problems |

You can customize rules in your ESLint configuration:

js

```
{rules: {'@next/next/no-img-element':'warn','react/no-unescaped-entities':'off',  },}
```

Rule severity can be **`off`**, **`warn`**, or **`error`**.

## **4. Quick comparison**

| **Feature** | **`generateMetadata`** | **`generateStaticParams`** | **ESLint** |
| --- | --- | --- | --- |
| Main purpose | SEO and page metadata | Pre-generate dynamic routes | Code quality |
| When it runs | During metadata resolution | During development/build as applicable | When linting is run |
| Input | Route parameters, data, parent metadata | Data used to produce route parameters | Source code and configuration |
| Output | Metadata object | Array of parameter objects | Warnings and errors |
| Example use | Dynamic product title | Pre-render blog slugs | Detect invalid patterns |

## **5. How they work together**

Consider an e-commerce website with product URLs such as **`/products/phone`** and **`/products/laptop`**.

- **`generateStaticParams`** defines which product routes can be pre-generated.
- **`generateMetadata`** generates the title and description for each product.
- **ESLint** helps catch code-quality issues in both implementations.

A typical project structure could look like this:

text

```
app/
  products/
    [slug]/
      page.tsx
eslint.config.mjs
package.json
```

For a production application, combine static generation where appropriate, metadata based on actual product data, and automated lint checks in your development or CI workflow.

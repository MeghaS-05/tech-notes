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

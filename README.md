# nextjs-interview-questions (2025–2026)

### Table of Contents
1. [What are the rendering methods in Nextjs?](#1-what-are-the-rendering-methods-in-nextjs)
2. [Server Side Rendering](#2-server-side-rendering)
3. [Client Side Rendering](#3-client-side-rendering)
4. [Static Site Generation](#4-static-site-generation)
5. [Incremental Static Regeneration?](#5-incremental-static-regeneration)
6. [How does routing works in Nextjs?](#6-how-does-routing-works-in-nextjs)
7. [What are API Routes?](#7-what-are-api-routes)
8. [Difference between getStaticProps and getServerSideProps](#8-difference-between-getstaticprops-and-getserversideprops)
9. [How does Nextjs improve performance?](#9-how-does-nextjs-improve-performance)
10. [CSR vs SSR vs SSG](#10-csr-vs-ssr-vs-ssg)
11. [App Router](#11-app-router)
12. [Page Router](#12-page-router)

## 1. **What are the rendering methods in Nextjs?**

Next.js supports multiple rendering strategies
- SSR (Server Side Rendering) renders on every request
- SSG (Static Site Generation) renders at build time
- ISR (Incremental Static Regeneration) updates static pages after build
- CSR (Client Side Rendering) renders in the browser

## 2. **Server Side Rendering?**

`How SSR Works`
- User opens a website.
- Browser sends request to server.
- Server fetches data if needed.
- Server generates complete HTML.
- Browser receives ready to display page.

```jsx
export async function getServerSideProps() {
  return { props: { data: "Hello" } }
}
```
<br>

### Restaurant Example 🍽️

Imagine you go to a restaurant.

🔵 SSR Style

- You order food.
- The kitchen prepares the full dish.
- Waiter brings you a ready to eat plate.
- You immediately start eating.

- 👉 You do not cook anything yourself.
- 👉 Everything is prepared before it reaches you.

*That is Server Side Rendering.* 

- Server = Kitchen
- Browser = You
- Food = Fully rendered HTML page


### Real Website Example

Let’s take an e-commerce website like Amazon.

`When you open a product page:`
- Server fetches product data

  
`Server builds full HTML with:`
- Product name
- Price
- Image
- Reviews
- Server sends ready page
- You instantly see content.

### Flow

Imagine You Open a Product Page
```jsx
www.shop.com/product/123
```

***Step 1: Browser Sends Request***

- Your browser says:
- "Hey server, give me product 123 page."


***Step 2: Server Builds Full HTML***

`Server does this:`
- Gets product data from database
- Uses your React or template code
- Combines both
- Generates complete HTML

Example, Database has:
```jsx
Name: iPhone 15
Price: ₹80,000
```
Your template code:
```jsx
<h1>{product.name}</h1>
<p>{product.price}</p>
```

Server converts it into:
```jsx
<html>
  <body>
    <h1>iPhone 15</h1>
    <p>₹80,000</p>
  </body>
</html>
```
👉 Full HTML


***Step 3: Browser Receives Ready Page***

- Browser gets this complete HTML and:
- Displays product name instantly
- Displays price instantly
- No waiting for JavaScript to fetch data
- User sees content immediately.


| Question                     | SSR             | CSR             |
| ---------------------------- | --------------- | --------------- |
| Where is code written?       | In your project | In your project |
| Where does it execute first? | Server          | Browser         |
| Who builds HTML?             | Server          | Browser         |


## 3. **Client Side Rendering**

- 👉 The browser builds the page using JavaScript.
- 👉 Server sends minimal HTML.
- 👉 UI is generated in the browser.

### What Happens Next

- Browser downloads JavaScript
- React runs in browser
- API call is made
- Data is fetched as JSON
- React builds HTML dynamically
- User finally sees content

### Real Life Example

Imagine online dashboard like company admin panel.

`When you log in:`
- Page loads
- Spinner appears
- Data loads after few seconds
- Then content shows
- That is CSR.

### When CSR Is Good

- ✅ Highly interactive apps
- ✅ Real time dashboards
- ✅ After login applications
- ✅ Apps where SEO does not matter

## 4. **Static Site Generation**

- 👉 HTML pages are generated at build time, not at request time.
- 👉 The pages are prebuilt and stored as static files.
- 👉 Server simply sends already created HTML files.

```jsx
export async function getStaticProps() {
  return { props: { posts: [] } }
}
```
### Real Life Example

Imagine printing newspapers.

***SSG***
- You print 10,000 newspapers in the morning.
- When someone buys, you just give a copy.

***SSR***
- You print newspaper only when customer comes.

***CSR***
- You give blank paper and pen, customer writes news themselves.


### When To Use SSG

- ✅ Blog
- ✅ Marketing website
- ✅ Documentation
- ✅ Landing pages
- ✅ Portfolio site

## 5. **Incremental Static Regeneration?**

ISR allows updating static pages after deployment without rebuilding the entire app.

```jsx
export async function getStaticProps() {
  return {
    props: {},
    revalidate: 60
  }
}

```

***ISR is useful when:***
- Data changes occasionally
- You want fast page loads
- You don't want to rebuild the entire site
- You want SEO-friendly static HTML

## 6. **How does routing works in Nextjs?**

Next.js uses file-based routing.
- pages/index.js → /
- pages/blog.js → /blog
- pages/blog/[id].js → dynamic route

## 7. **What are API Routes?**

API Routes allow creating backend endpoints inside the Next.js app.

```jsx
export default function handler(req, res) {
  res.status(200).json({ message: "Hello API" })
}

```

## 8. **Difference between getStaticProps and getServerSideProps**

| Feature  | getStaticProps       | getServerSideProps     |
| -------- | -------------------- | ---------------------- |
| Runs     | Build time           | Every request          |
| Speed    | Faster               | Slower                 |
| SEO      | Good                 | Good                   |
| Use case | Blogs, landing pages | Dashboards, auth pages |

## 9. **How does Nextjs improve performance**
- Code splitting
- Image optimization
- Pre-fetching pages
- Static generation
- Edge middleware

<br>

## 10. **CSR vs SSR vs SSG**

| Feature                     | CSR (Client Side Rendering) | SSR (Server Side Rendering) | SSG (Static Site Generation) |
| --------------------------- | --------------------------- | --------------------------- | ---------------------------- |
| **Where HTML is generated** | Browser                     | Server                      | Build time                   |
| **When HTML is generated**  | After page loads            | On every request            | During project build         |
| **What server sends**       | Empty HTML + JS             | Fully rendered HTML         | Prebuilt HTML file           |
| **Initial Load Speed**      | Slower                      | Fast                        | Very Fast                    |
| **SEO**                     | Weak by default             | Strong                      | Excellent                    |
| **Server Work**             | Low                         | High                        | Very Low                     |
| **API Calls happen**        | In browser                  | On every request (server)   | During build                 |
| **Best for**                | Dashboards, internal apps   | E-commerce, news            | Blogs, marketing sites       |
| **Content freshness**       | Always latest               | Always latest               | Static until rebuild         |


## 11. **App Router**

App Router provides Hierarchical File Structure routing. which provides features such as shared layout, nested routing, loading states, error handling, 404 not found page, and many more.


### Reserved File Names:

| File            | Purpose       |
| --------------- | ------------- |
| `layout.tsx`    | Shared layout |
| `page.tsx`      | Route page    |
| `loading.tsx`   | Loading UI    |
| `error.tsx`     | Error UI      |
| `not-found.tsx` | 404 page      |
| `route.ts`      | API route     |


### 📁 Basic Folder Structure
```jsx
my-app/
 ├─ app/
 │   ├─ page.tsx        → Home page (/)
 │   ├─ layout.tsx      → Shared layout
 │   ├─ about/
 │   │    └─ page.tsx   → /about
 │   └─ blog/
 │        └─ [id]/
 │             └─ page.tsx → /blog/123
```

### 🔹 1. page.tsx → Defines a Route
```jsx
// app/about/page.tsx
export default function AboutPage() {
  return <h1>About Page</h1>;
}

//localhost:3000/about
```

### 🔹 2. layout.tsx → Shared Layout
```jsx
// app/layout.tsx
export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <nav>Navbar</nav>
        {children}
      </body>
    </html>
  );
}

```

- ✔ Navbar will appear on all pages
- ✔ Layouts can be nested

### 🔹 3. Dynamic Routes

```jsx
app/blog/[id]/page.tsx
```
```jsx
export default function BlogPost({ params }) {
  return <h1>Blog ID: {params.id}</h1>;
}
```
***URL***
```jsx
/blog/123
```
## 11. **Page Router**

- The Pages Router is the older routing system used in Next.js before the App Router (Next.js 13).
- It is based on the pages/ folder.
- If you create a file inside pages/, it automatically becomes a route.

### 📁 Basic Folder Structure

```jsx
my-app/
 ├─ pages/
 │   ├─ index.tsx        → /
 │   ├─ about.tsx        → /about
 │   ├─ blog/
 │   │    └─ [id].tsx    → /blog/123
 │   └─ api/
 │        └─ hello.ts    → /api/hello
```

### 🔹 1️⃣ Basic Route
```jsx
// pages/about.tsx
export default function About() {
  return <h1>About Page</h1>;
}
```
URL:
```jsx
localhost:3000/about
```

### 🔹 2️⃣ Home Page
```jsx
// pages/index.tsx
export default function Home() {
  return <h1>Home Page</h1>;
}
```
index.tsx = root route /

### 🔹 3️⃣ Dynamic Routes
```jsx
pages/blog/[id].tsx
```

```jsx
import { useRouter } from "next/router";

export default function BlogPost() {
  const router = useRouter();
  const { id } = router.query;

  return <h1>Blog ID: {id}</h1>;
}
```

### ⚠️ When to Use Pages Router?

- Working on older project
- Migration not done yet
- Need traditional React style routing

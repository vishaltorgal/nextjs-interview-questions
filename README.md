# nextjs-interview-questions (2025–2026)

### Table of Contents
1. [What are the rendering methods in Nextjs?](#1-what-are-the-rendering-methods-in-nextjs)
2. [What is Server Side Rendering?](#2-what-is-server-side-rendering)
3. [What is Static Site Generation?](#3-what-is-static-site-generation)
4. [What is Incremental Static Regeneration?](#4-what-is-incremental-static-regeneration)
5. [How does routing works in Nextjs?](#5-how-does-routing-works-in-nextjs)
6. [What are API Routes?](#6-what-are-api-routes)
7. [Difference between getStaticProps and getServerSideProps](#7-difference-between-getstaticprops-and-getderversideprops)
8. [How does Nextjs improve performance?](#8-how-does-nextjs-improve-performance)



## 1. **What are the rendering methods in Nextjs?**

Next.js supports multiple rendering strategies
- SSR (Server Side Rendering) renders on every request
- SSG (Static Site Generation) renders at build time
- ISR (Incremental Static Regeneration) updates static pages after build
- CSR (Client Side Rendering) renders in the browser

## 2. **What is Server Side Rendering?**

SSR generates HTML on the server for every request. This improves SEO and initial page load but can increase server load

```jsx
export async function getServerSideProps() {
  return { props: { data: "Hello" } }
}
```

## 3. **What is Static Site Generation?**

SSG generates pages at build time and serves static HTML. It is very fast and ideal for blogs or marketing pages.

```jsx
export async function getStaticProps() {
  return { props: { posts: [] } }
}
```

## 4. **What is Incremental Static Regeneration?**

ISR allows updating static pages after deployment without rebuilding the entire app.

```jsx
export async function getStaticProps() {
  return {
    props: {},
    revalidate: 60
  }
}

```

## 5. **How does routing works in Nextjs?**

Next.js uses file-based routing.
- pages/index.js → /
- pages/blog.js → /blog
- pages/blog/[id].js → dynamic route

## 6. **What are API Routes?**

API Routes allow creating backend endpoints inside the Next.js app.

```jsx
export default function handler(req, res) {
  res.status(200).json({ message: "Hello API" })
}

```

## 7. **Difference between getStaticProps and getServerSideProps**

| Feature  | getStaticProps       | getServerSideProps     |
| -------- | -------------------- | ---------------------- |
| Runs     | Build time           | Every request          |
| Speed    | Faster               | Slower                 |
| SEO      | Good                 | Good                   |
| Use case | Blogs, landing pages | Dashboards, auth pages |

## 7. **How does Nextjs improve performance**
- Code splitting
- Image optimization
- Pre-fetching pages
- Static generation
- Edge middleware


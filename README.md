# Next JS Interview Questions

### **1. Basics of Next.js**

<details>
<summary><strong>1. What is Next.js?</strong></summary>
Next.js is a <strong>React-based full stack Framework </strong> that simplifies building modern web applications. It enhances React by providing additional features, tools, and optimizations. Here’s a breakdown in simple terms:

### Key Features of Next.js:
1. **Server-Side Rendering (SSR):** 
   - Pages can be rendered on the server before being sent to the browser.
   - Improves SEO and load times because search engines and users receive fully formed pages.

2. **Static Site Generation (SSG):**
   - Pages can be pre-generated at build time and served as static files.
   - This makes the app super fast and scalable for pages that don’t change often.

3. **API Routes:**
   - You can create backend-like API endpoints directly in the Next.js project without needing a separate backend server.
   - Example: `pages/api/hello.js` can serve as an API endpoint.

4. **Dynamic Routing:**
   - Create routes with parameters like `/products/[id]` for dynamic pages.
   - No need to manually configure routes; they’re inferred from the file structure.

5. **Built-in CSS and Image Optimization:**
   - Supports CSS modules, Sass, and built-in image optimization for faster loading.
   - Helps deliver optimized images in various formats and sizes automatically.

6. **Incremental Static Regeneration (ISR):**
   - Allows updating static pages after the build process without rebuilding the entire app.
   - Useful for apps with content that changes periodically.

7. **File-Based Routing:**
   - The folder structure in the `pages` directory directly maps to application routes.
   - No need to configure routing manually.

8. **Automatic Code Splitting:**
   - Loads only the JavaScript required for a particular page, improving performance.

9. **Full-stack Capabilities:**
   - Combines frontend and backend features, making it easier to handle data fetching and server-side logic.

10. **Edge-Ready:**
   - Supports edge rendering for low-latency, region-based deployments (like Vercel’s Edge Network).

</details>
<details>
<summary><strong>2. Why is Next.js Popular?</strong></summary>
- SEO Friendly: Pre-rendering ensures search engines can easily crawl pages.
- Developer-Friendly: Built-in tools simplify common tasks.
- Scalable and Flexible: Works well for small apps and large-scale projects.
- Community Support: Actively maintained by Vercel with a large ecosystem of plugins and extensions.
</details>

</details>
<details>
<summary><strong>3. When to Use Next.js?</strong></summary>


- When your app needs **good SEO** (e.g., blogs, e-commerce, portfolios).
- When you want **fast performance** with static/dynamic rendering.
- When you prefer to keep frontend and backend logic in the same codebase.
- For **React projects** that need advanced features out of the box.



</details>



3. **What is the difference between React and Next.js?**
   - React is a library for building UIs; Next.js is a framework built on React that adds server-side rendering, static site generation, and file-based routing.
---

4. **How is routing handled in Next.js?**
   - File-based routing: The folder structure inside the `pages/` directory defines routes.
---

5. **What is the purpose of the `pages` directory in Next.js?**
   - It contains React components mapped to specific routes based on the file structure.

---

### Rendering Techniques in Next.js

Next.js is a powerful React framework that supports different rendering techniques, which can be used based on the needs of your application. These techniques are:

- **Server-side Rendering (SSR)**
- **Static Site Generation (SSG)**
- **Client-side Rendering (CSR)**
- **Incremental Static Regeneration (ISR)**

Each of these rendering methods has its own use case, and understanding when to use them can significantly improve the performance and SEO of your application.

---

### 1. **Server-side Rendering (SSR) in Next.js**

**What it is**:  
Server-side rendering (SSR) means that the HTML for a page is generated on the server for each request, then sent to the browser. This allows the browser to load a fully rendered page (with HTML, CSS, and JS) when the user requests the page, which can improve performance for certain types of content (especially dynamic content). SSR can improve SEO because search engine crawlers can immediately access the fully rendered HTML without needing to run JavaScript.

**How it works**:
- When the page is requested, the server runs the React code to generate the HTML, which is then sent to the browser.
- It is especially useful for content that changes often and needs to be up-to-date for each request (like user-specific data).

**Implemented with `getServerSideProps`**:
- `getServerSideProps` is a special Next.js function that runs on the server **before** the page is sent to the browser. This function fetches data that’s needed to render the page on each request.
- It enables you to pre-render a page on every request with dynamic data from APIs, databases, or other sources.

**Example of SSR**:
```js
// pages/index.js
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  
  return {
    props: { data }, // Data will be passed to the page as props
  };
}

export default function HomePage({ data }) {
  return (
    <div>
      <h1>Server-Side Rendered Page</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}
```
In this example, the page will be rendered on the server with the data fetched from the API for each request.

---

### 2. **Static Site Generation (SSG) in Next.js**

**What it is**:  
Static Site Generation (SSG) involves pre-rendering pages at **build time**. This means that all the pages are generated once when the site is built and served as static HTML files. It’s fast because static files can be cached and served immediately by CDNs without needing to regenerate the HTML on every request.

**How it works**:
- Pages are pre-rendered at build time and stored as static HTML files.
- The data needed to render the page can either be fetched during the build process or from an external source.
- SSG is ideal for pages that do not change frequently or for content that can be cached and served as static files.

**Implemented with `getStaticProps`**:
- `getStaticProps` is a special function in Next.js that runs at build time to fetch the data needed to render the page. The fetched data is used to generate static HTML files.
- Since the data is fetched during build time, the page will not have access to runtime data (e.g., data that changes often or is user-specific).

**Example of SSG**:
```js
// pages/index.js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  
  return {
    props: { data }, // Data is passed to the page as props at build time
  };
}

export default function HomePage({ data }) {
  return (
    <div>
      <h1>Static Site Generated Page</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}
```
Here, the data is fetched during the build process and used to pre-render the page as static HTML.

---

### 3. **Client-side Rendering (CSR)**

**What it is**:  
Client-side rendering (CSR) refers to the process where JavaScript in the browser (via React) is responsible for rendering the content. Initially, a minimal HTML page is sent to the browser, and JavaScript is used to dynamically fetch data and render the page.

**How it works**:
- The browser receives an empty or minimal HTML file and JavaScript files.
- React then takes over and fetches the necessary data (via AJAX or APIs), and renders the page on the client-side.
- CSR is often used for dynamic, interactive applications that require real-time updates or frequent user interactions.

**Example of CSR**:
```js
// pages/index.js
import { useEffect, useState } from 'react';

export default function HomePage() {
  const [data, setData] = useState([]);

  useEffect(() => {
    async function fetchData() {
      const res = await fetch('https://api.example.com/data');
      const data = await res.json();
      setData(data);
    }
    fetchData();
  }, []);

  return (
    <div>
      <h1>Client-Side Rendered Page</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}
```
In this example, data is fetched on the client-side when the component mounts, and the page is rendered dynamically in the browser.

---

### 4. **Incremental Static Regeneration (ISR)**

**What it is**:  
Incremental Static Regeneration (ISR) allows you to update static pages after the build, without rebuilding the entire site. This enables you to regenerate specific static pages **incrementally** in the background based on certain conditions, such as the passage of time or specific user interactions.

**How it works**:
- With ISR, you can specify how often a static page should be re-generated by using the `revalidate` option in `getStaticProps`.
- After the initial build, Next.js will serve the static page, and in the background, it can regenerate the page when the revalidation time has passed. This allows you to keep your pages up-to-date without needing to rebuild the entire site.

**Implemented with `revalidate` in `getStaticProps`**:
- The `revalidate` key inside `getStaticProps` is used to specify the time (in seconds) after which the static page will be regenerated.

**Example of ISR**:
```js
// pages/index.js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data },
    revalidate: 60, // Re-generate the page every 60 seconds
  };
}

export default function HomePage({ data }) {
  return (
    <div>
      <h1>Incrementally Regenerated Static Page</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}
```
In this example, the page is generated at build time and will be re-generated every 60 seconds.

---

### 5. **Difference Between SSR and SSG**

- **SSR (Server-Side Rendering)**:
  - **When**: HTML is generated on every request on the server.
  - **Use case**: Dynamic content that needs to be up-to-date with every request (e.g., personalized data, real-time data).
  - **Performance**: Can be slower compared to static files because the page is generated on each request.
  - **SEO**: Good for SEO since search engines get fully rendered HTML.

- **SSG (Static Site Generation)**:
  - **When**: HTML is generated once at build time and served as static files.
  - **Use case**: Content that doesn’t change frequently or can be cached (e.g., blogs, marketing pages, documentation).
  - **Performance**: Fast, as static files can be served via a CDN.
  - **SEO**: Excellent for SEO as the HTML is pre-rendered.

### Summary

- **SSR** is used for pages that need to be dynamically generated on every request with fresh data.
- **SSG** is used for pages that are static and can be pre-rendered at build time.
- **CSR** is used for client-side rendering where React handles rendering dynamically on the client side.
- **ISR** allows static pages to be updated incrementally without rebuilding the entire site, providing flexibility in managing static content with dynamic updates.


---

### **3. Data Fetching**

11. **What is `getStaticProps` in Next.js?**
    - Fetches data at build time for SSG.
    ```javascript
    export async function getStaticProps() {
      return { props: { data: 'Static Data' } };
    }
    ```
---

12. **What is `getServerSideProps` in Next.js?**
    - Fetches data at request time for SSR.
    ```javascript
    export async function getServerSideProps() {
      return { props: { data: 'Server Data' } };
    }
    ```
---

13. **What is `getStaticPaths`?**
    - Used with `getStaticProps` to define dynamic routes for static generation.
    ```javascript
    export async function getStaticPaths() {
      return { paths: [{ params: { id: '1' } }], fallback: false };
    }
    ```
---

14. **What is the `fallback` key in `getStaticPaths`?**
    - Determines behavior for routes not generated at build time.
      - `false`: 404 for non-pre-rendered pages.
      - `true`: Pages are generated on demand.

15. **Can you use client-side data fetching in Next.js?**
    - Yes, with React hooks like `useEffect` and `fetch`.

---

### **4. Routing and Navigation**

16. **How does dynamic routing work in Next.js?**
    - Use brackets in file names, e.g., `[id].js` for `/post/1`.
---

17. **How do you navigate between pages in Next.js?**
    - Use the `Link` component.
    ```javascript
    import Link from 'next/link';
    <Link href="/about">About</Link>
    ```
---

18. **What is shallow routing?**
    - Allows you to update the URL without triggering a full page reload or data fetching.
---

19. **How do API routes work in Next.js?**
    - Define API routes in the `pages/api/` directory. Each file exports a handler function.
    ```javascript
    export default function handler(req, res) {
      res.status(200).json({ message: 'Hello World' });
    }
    ```
---

20. **How do you handle custom routes in Next.js?**
    - Use the `next.config.js` file for rewrites or redirects.
    ```javascript
    module.exports = {
      async rewrites() {
        return [{ source: '/custom', destination: '/about' }];
      },
    };
    ```

---

### **5. Performance Optimization**

21. **What is code splitting in Next.js?**
    - Automatically splits code to load only the JavaScript required for the page.
---
22. **How does Next.js optimize images?**
    - Use the `next/image` component for lazy loading, resizing, and optimizing images.
    ```javascript
    import Image from 'next/image';
    <Image src="/image.png" width={500} height={500} />;
    ```
---
23. **What is `next/script`?**
    - Optimizes loading of third-party scripts with features like lazy loading and priority.
---
24. **How can you optimize font loading in Next.js?**
    - Use the `next/font` module for automatic font optimization.
---
25. **How does prefetching work in Next.js?**
    - Automatically prefetches linked pages when they are visible in the viewport.

---

### **6. Configuration and Deployment**

26. **What is `next.config.js`?**
    - A configuration file for customizing the Next.js application.

---
27. **How do you add environment variables in Next.js?**
    - Use a `.env.local` file or `process.env` in `next.config.js`.

---
28. **How do you deploy a Next.js app?**
    - Deploy on platforms like Vercel (recommended), AWS, or Netlify.

---
29. **What is the difference between `publicRuntimeConfig` and `serverRuntimeConfig`?**
    - `publicRuntimeConfig`: Accessible on both client and server.
    - `serverRuntimeConfig`: Accessible only on the server.

---
30. **How do you enable TypeScript in Next.js?**
    - Add a `tsconfig.json` file. Next.js automatically detects and compiles TypeScript.

---

### **7. Middleware and API Handling**

31. **What is middleware in Next.js?**
    - Code executed before rendering, implemented in the `middleware.js` file.

---
32. **How do you handle API versioning in Next.js?**
    - Create versioned folders inside `pages/api/`, e.g., `/api/v1/`.

---
33. **What is `useSWR`?**
    - A React hook for client-side data fetching with caching and revalidation.

---
34. **How do you handle CORS in Next.js API routes?**
    - Use middleware or libraries like `cors`.

---
35. **What is the `res.revalidate` method in Next.js?**
    - Triggers a re-build of static pages.

---

### **8. Styling**

36. **How do you style components in Next.js?**
    - Use CSS, Sass, CSS Modules, or styled-components.
---
37. **What are CSS Modules in Next.js?**
    - Scoped CSS classes.
    ```javascript
    import styles from './Component.module.css';
    <div className={styles.className}>Hello</div>;
    ```
---
38. **Can you use global styles in Next.js?**
    - Yes, by importing a CSS file in `_app.js`.
---
39. **What is styled-jsx?**
    - A built-in library for scoped CSS using JSX syntax.
---
40. **How do you use Sass with Next.js?**
    - Install `sass` and use `.scss` files directly.

---

### **9. Advanced Topics**

41. **What is a custom App component?**
    - The `pages/_app.js` file customizes the default App component.
---
42. **What is a custom Document in Next.js?**
    - The `pages/_document.js` file customizes the HTML structure.
---
43. **What are static exports in Next.js?**
    - Generate a static version of the app using `next export`.
---
44. **How do you implement internationalization in Next.js?**
    - Use the `i18n` property in `next.config.js`.
---
45. **What is the purpose of `getInitialProps`?**
    - Used to fetch data for both SSR and CSR but is now considered legacy.

---

### **10. Miscellaneous**

46. **How does Next.js handle SEO?**
    - Built-in SSR, metadata management with `next/head`.
---
47. **What is the `next/head` component?**
    - A component for managing metadata in the `<head>` tag.
---
48. **How do you handle redirects in Next.js?**
    - Define redirects in `next.config.js`.
    ```javascript
    module.exports = {
      async redirects() {
        return [{ source: '/old', destination: '/new', permanent: true }];
      },
    };
    ```
---
49. **What is the difference between static and dynamic imports?**
    - Static: Imported at build time.
    - Dynamic: Imported at runtime using `import()`.
---
50. **How do you handle 404 pages in Next.js?**
    - Create a `pages/404.js` file for a custom 404 page.

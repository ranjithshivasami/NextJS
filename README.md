# Next JS Interview Questions

### **1. Basics of Next.js**

1. **What is Next.js?**
   - A React framework for building server-rendered or statically exported React applications.  
   - Provides features like server-side rendering (SSR), static site generation (SSG), API routes, and file-based routing.

---

2. **What are the main features of Next.js?**
   - File-based routing
   - SSR and SSG
   - API routes
   - Built-in CSS and Sass support
   - Optimized image handling
   - Automatic code splitting and bundling
---

3. **What is the difference between React and Next.js?**
   - React is a library for building UIs; Next.js is a framework built on React that adds server-side rendering, static site generation, and file-based routing.
---

4. **How is routing handled in Next.js?**
   - File-based routing: The folder structure inside the `pages/` directory defines routes.
---

5. **What is the purpose of the `pages` directory in Next.js?**
   - It contains React components mapped to specific routes based on the file structure.

---

### **2. Rendering Techniques**

6. **What is server-side rendering (SSR) in Next.js?**
   - A page is rendered on the server for each request, sending HTML to the browser.
   - Implemented using `getServerSideProps`.

---

7. **What is static site generation (SSG) in Next.js?**
   - Pages are pre-rendered at build time and served as static files.
   - Implemented using `getStaticProps`.

---

8. **What is client-side rendering (CSR)?**
   - Pages are rendered entirely on the client using React, typically for dynamic data fetching.

---

9. **What is incremental static regeneration (ISR)?**
   - Allows static pages to be updated incrementally without rebuilding the entire site.
   - Implemented with `revalidate` in `getStaticProps`.

---

10. **What is the difference between SSR and SSG in Next.js?**
    - SSR generates HTML on every request; SSG generates it at build time.

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

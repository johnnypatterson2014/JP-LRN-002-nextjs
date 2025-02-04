## Example Next.js App 

Typescript
 - TypeScript is a way of writing JavaScript a bit more structured than pure JavaScript. This variant is used in many modern web applications and has been adopted by LangChain and LlamaIndex for their JavaScript versions.

NextJS
 - is a React framework that makes it easier to create a web based UI
 - it is simplified and optimized to create web applications (frontend UI)
 - Next.js handles the tooling and configuration needed for React, and provides additional structure, features, and optimizations for your application.

Vercel
 - Vercel is a hosting service created by the creators of Next.js and specially designed to host applications of this framework
 - vercel is designed to automatically deploy your nextjs app whenever you push changes to your git repo


install npm first time:
	npm install -g pnpm

create example nextjs project from a template:
	npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm

install the project's packages:
	npm install

run the dev server:
	npm run dev

Create a github repo and push code there.

Create a Vercel account and deploy the git repo project there. 
Vercel project: https://vercel.com/johnnys-projects-a3be4325/jp-lrn-002-nextjs

Running app is here:
https://jp-lrn-002-nextjs.vercel.app/

View postgres db tables here:
https://console.neon.tech/app/projects/floral-truth-39027350/branches/br-polished-lab-a66o8rdi/tables?database=neondb


## Next.js tutorial

https://nextjs.org/learn/dashboard-app/

### Chapter 1: getting started
https://nextjs.org/learn/dashboard-app/getting-started
 - create sample next.js app

 - /app						- contains all routes, components, logic, etc.
 -     /lib					- contains reusable utility functions
 - 	   /ui					- contains all ui components
 - /public					- static assets (images, etc)
 - .config					- config files in root folder

Example class to represent object data returned from the db:
 - 	/app/lib/definitions.ts

### Chapter 2: CSS
https://nextjs.org/learn/dashboard-app/css-styling

 - global css styles: /app/ui/global.css
 - import into your root layout: /app/layout.tsx (applied to all pages by default)
 - project uses tailwind css framework. https://tailwindcss.com/
 - css modules can also be used: https://nextjs.org/docs/app/getting-started/css
 - clsx - another css tool (makes it easy to toggle class names). https://www.npmjs.com/package/clsx

### Chapter 3: Optimizing fonts and images
https://nextjs.org/learn/dashboard-app/optimizing-fonts-images

### Chapter 4: Creating layouts and pages
https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages

 - nested routing: Next.js uses file-system routing where folders are used to create nested routes. 
 - eg. /app/page.tsx
 -         /layout.tsx
 -         /dashboard/page.tsx
 -                   /layout.tsx (optional)
 -                   /customers/page.tsx
 -                   /invoices/page.tsx

### Chapter 5: Navigating Between Pages
https://nextjs.org/learn/dashboard-app/navigating-between-pages

### Chapter 6: Setting Up Your Database
https://nextjs.org/learn/dashboard-app/setting-up-your-database

 - deploy next.js app to vercel (just need to link to github repo)
 - use vercel to create a db integration (eg. postgres)
 - seed db using a script
 - example to manually execute an sql query: /app/query/route.ts

### Chapter 7: Fetching Data
https://nextjs.org/learn/dashboard-app/fetching-data

 - use react server components to fetch data
 - for our example, we wil use the postgres.js library: https://github.com/porsager/postgres
 - see example: 
 - 		/app/lib/data.ts - functions to make sql queries
 - 		/app/dashboard/page.tsx - calls the sql functions and uses UI components to display the data
 - 		/app/ui/dashboard/*.tsx - ui components to display the data

Note: sql calls are not async. We will fix this.
 - 		/app/dashboard/page.tsx: see line 13; fetchLatestInvoices() must wait for fetchRevenue() to finish first

 Parallel data fetching
  - For example, in data.ts, we're using Promise.all() in the fetchCardData() function.
  - problem: what if one data call takes a lot longer than the others?

Note: The dashboard is static, so any data updates will not be reflected on your application. We will fix this.

### Chapter 8: Static and Dynamic Rendering
https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering

### Chapter 9: Streaming
https://nextjs.org/learn/dashboard-app/streaming

Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.

By streaming, you can prevent slow data requests from blocking your whole page. This allows the user to see and interact with parts of the page without waiting for all the data to load before any UI can be shown to the user.

Streaming works well with React's component model, as each component can be considered a chunk.

There are two ways you implement streaming in Next.js:
 - At the page level, with the loading.tsx file (which creates <Suspense> for you).
 - At the component level, with <Suspense> for more granular control.

 - loading.tsx is a special Next.js file built on top of React Suspense. It allows you to create fallback UI to show as a replacement while page content loads.
 - Since <SideNav> is static, it's shown immediately. The user can interact with <SideNav> while the dynamic content is loading.
 - The user doesn't have to wait for the page to finish loading before navigating away (this is called interruptable navigation).

Adding loading skeletons
 - A loading skeleton is a simplified version of the UI. Many websites use them as a placeholder (or fallback) to indicate to users that the content is loading. Any UI you add in loading.tsx will be embedded as part of the static file, and sent first. Then, the rest of the dynamic content will be streamed from the server to the client.

Create a new folder called /(overview) inside the dashboard folder. Then, move your loading.tsx and page.tsx files inside the folder: Now, the loading.tsx file will only apply to your dashboard overview page (and not the child pages invoices and customers).

Route groups allow you to organize files into logical groups without affecting the URL path structure. When you create a new folder using parentheses (), the name won't be included in the URL path. So /dashboard/(overview)/page.tsx becomes /dashboard.

Streaming a component
 - So far, you're streaming a whole page. But you can also be more granular and stream specific components using React Suspense.
 - Suspense allows you to defer rendering parts of your application until some condition is met (e.g. data is loaded). You can wrap your dynamic components in Suspense. Then, pass it a fallback component to show while the dynamic component loads.

Grouping components

### Chapter 10: Partial Prerendering
https://nextjs.org/learn/dashboard-app/partial-prerendering

### Chapter 11: Adding Search and Pagination
https://nextjs.org/learn/dashboard-app/adding-search-and-pagination

Here's a quick overview of the implementation steps:
 - Capture the user's input.
 - Update the URL with the search params.
 - Keep the URL in sync with the input field.
 - Update the table to reflect the search query.

see files:
 - /app/dashboard/invoices/page.tsx
 - /app/ui/search.tsx
 - /app/ui/invoices/pagination.tsx

### Chapter 12: Mutating Data
https://nextjs.org/learn/dashboard-app/mutating-data

React Server Actions allow you to run asynchronous code directly on the server. They eliminate the need to create API endpoints to mutate your data. Instead, you write asynchronous functions that execute on the server and can be invoked from your Client or Server Components.

Here are the steps you'll take to create a new invoice:
 - Create a form to capture the user's input.
 - Create a Server Action and invoke it from the form.
 - Inside your Server Action, extract the data from the formData object.
 - Validate and prepare the data to be inserted into your database.
 - Insert the data and handle any errors.
 - Revalidate the cache and redirect the user back to invoices page.

These are the steps you'll take to update an invoice:
 - Create a new dynamic route segment with the invoice id.
 - Read the invoice id from the page params.
 - Fetch the specific invoice from your database.
 - Pre-populate the form with the invoice data.
 - Update the invoice data in your database.










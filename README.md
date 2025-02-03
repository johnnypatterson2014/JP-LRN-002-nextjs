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
 - see example: /app/lib/data.ts













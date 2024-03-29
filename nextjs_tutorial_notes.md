# README
## on ch2

## general
- this code is written based off this doc for the app router course:
https://nextjs.org/learn/dashboard-app
- you connect your github repo with vercel here
    - you also make the root directory on vercel nextjs-dashboard
- you also created a postgres db using vercel
- you got the env variables from vercel
- you also seeded a database with the seed file in scripts with npm run seed
- you can explore the database more on vercel
- you can even query on vercel:
    SELECT invoices.amount, customers.name
    FROM invoices
    JOIN customers ON invoices.customer_id = customers.id
    WHERE invoices.amount = 666;

## project structure
/app: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
/app/lib: Contains functions used in your application, such as reusable utility functions and data fetching functions.
/app/ui: Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
/public: Contains all the static assets for your application, such as images.
/scripts: Contains a seeding script that you'll use to populate your database in a later chapter.
Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.
app/lib/placeholder-data.js: contains placehodler data

## testing
- run npm i and npm run dev (starts app on port 3000)

# Errors 

# Terminal commands

## initializing project
npx create-next-app@latest nextjs-dashboard --use-npm --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example"

# Definitions

## what is dynamic rendering?
With dynamic rendering, content is rendered on the server for each user **at request time (when the user visits the page)**. There are a couple of benefits of dynamic rendering:

## Static Rendering
With static rendering, data fetching and rendering happens on the server at **build time (when you deploy)** or during revalidation. The result can then be distributed and cached in a Content Delivery Network (CDN).

![Alt text](notes_images/image_4.png)

## React Server Components

They allow you to query the database directly from the server without an additional API layer.

By default, Next.js applications use React Server Components. Fetching data with Server Components is a relatively new approach and there are a few benefits of using them:

Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use async/await syntax without reaching out for useEffect, useState or data fetching libraries.
Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
As mentioned before, since Server Components execute on the server, you can query the database directly without an additional API layer.

## API layer
APIs are an intermediary layer between your application code and database. There are a few cases where you might use an API:

If you're using 3rd party services that provide an API.
If you're fetching data from the client, you want to have an API layer that runs on the server to avoid exposing your database secrets to the client.
In Next.js, you can create API endpoints using Route Handlers.

## CSS Modules
Provide a way to make CSS classes locally scoped to components by default, reducing the risk of styling conflicts.
CSS Modules allow you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about style collisions as well.

## Tailwind
Tailwind is a CSS framework that speeds up the development process by allowing you to quickly write utility classes directly in your TSX markup.

## Next.js
- a framework for building server-rendered React applications, but it does have some backend capabilities
- a backend framework that serves a front end. SSR (server side rendering) provides improved perfromance and SEO.
- SSR only happens for the initial page load, after that it all goes client side

## GraphQL
- a query language for APIs that allows users to request the exact data needed from an API rather than a fixed set of endpoints.

## create-next-app
- a Command Line Interface (CLI) tool that sets up a Next.js application for you.

# Questions

## okay but how is the backend and frontend code seperated? is it not a security risk for them to be together?

## does nextJS need special deployment? can you deploy nextJS on not vercel infra?

## what are the benefits of static rendering?
Real-Time Data - Dynamic rendering allows your application to display real-time or frequently updated data. This is ideal for applications where data changes often.
User-Specific Content - It's easier to serve personalized content, such as dashboards or user profiles, and update the data based on user interaction.
Request Time Information - Dynamic rendering allows you to access information that can only be known at request time, such as cookies or the URL search parameters.

## Why might static rendering not be a good fit for a dashboard app?
Because the application will not reflect the latest data changes
When your data updates, you want to show the latest changes in your dashboard. Static Rendering is not a good fit for this use case.

## what are the benefits of static rendering
Faster Websites - Prerendered content can be cached and globally distributed. This ensures that users around the world can access your website's content more quickly and reliably.
Reduced Server Load - Because the content is cached, your server does not have to dynamically generate content for each user request.
SEO - Prerendered content is easier for search engine crawlers to index, as the content is already available when the page loads. This can lead to improved search engine rankings.
Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data that is regularly updated.

## what is the disadvantage of parallel data fetching?
- what if one request is slower than the otehrs?

## what is parallel data fetching
- a technique sed to avoid waterwfalls by making all data requests at the same time
In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData() function:

## what are request waterfalls
A "waterfall" refers to a sequence of network requests that depend on the completion of previous requests. In the case of data fetching, each request can only begin once the previous request has returned data.
This pattern is not necessarily bad. There may be cases where you want waterfalls because you want a condition to be satisfied before you make the next request. For example, you might want to fetch a user's ID and profile information first. Once you have the ID, you might then proceed to fetch their list of friends. In this case, each request is contingent on the data returned from the previous request.

However, this behavior can also be unintentional and impact performance.
below shows a pic of time taken for sequential vs parallel
![Alt text](notes_images/image_3.png)

## how does client side rendering work? 
The alternative to prerendering in web development is Client-Side Rendering (CSR). Unlike prerendering techniques such as Static Site Generation (SSG) or Server-Side Rendering (SSR) that generate HTML on the server, Client-Side Rendering dynamically generates HTML content on the client (browser) using JavaScript. Here's an overview of how CSR works and its characteristics:

How Client-Side Rendering Works
Initial Request: When a user requests a page, the server sends a minimal HTML document along with the JavaScript files needed to render the page content.

JavaScript Execution: The browser executes the JavaScript, which typically includes fetching data from an API and then using that data to generate HTML content directly in the browser.

Page Rendering: Once the JavaScript has finished running, the page content is rendered and displayed to the user. All subsequent navigations and interactions that require new data fetches or page updates are handled entirely through JavaScript without needing to request full page HTML from the server.

## what does it mean to prerender a route?
This is the process where Next.js generates the HTML for each page in advance, instead of having it all done by client-side JavaScript. When a user requests a page, the server sends the pre-generated HTML, which can be displayed immediately, making the page load faster than it would if the browser had to build the page from scratch using JavaScript. This is beneficial for both performance and SEO, as search engines can crawl the site more effectively.

## what are the different ways to fetch data
API layers and database queries

### database queries
When you're creating a full-stack application, you'll also need to write logic to interact with your database. For relational databases like Postgres, you can do this with SQL, or an ORM like Prisma.

There are a few cases where you have to write database queries:

When creating your API endpoints, you need to write logic to interact with your database.
If you are using React Server Components (fetching data on the server), you can skip the API layer, and query your database directly without risking exposing your database secrets to the client.

## how does automatic code splitting work?
To improve the navigation experience, Next.js automatically code splits your application by route segments. This is different from a traditional React SPA, where the browser loads all your application code on initial load.

Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work.

Futhermore, in production, whenever <Link> components appear in the browser's viewport, Next.js automatically prefetches the code for the linked route in the background. By the time the user clicks the link, the code for the destination page will already be loaded in the background, and this is what makes the page transition near-instant!

## why optimize navigation?
To link between pages, you'd traditionally use the <a> HTML element. At the moment, the sidebar links use <a> elements, but notice what happens when you navigate between the home, invoices, and customers pages on your browser.

There's a full page refresh on each page navigation!

## how do you use the link component?
you can use the <Link /> Component to link between pages in your application. <Link> allows you to do client-side navigation with JavaScript.

## what is partial rerendering
- only the page components update while the layout won't re-render.
- used in nextjs nav

## what does a layout.tsx file do?
any nested pages will be in the child component

## how does nextjs routing work?

it uses folders to create nested routes
![Alt text](notes_images/image.png)
You can create separate UIs for each route using layout.tsx and page.tsx files.

page.tsx is a special Next.js file that exports a React component, and it's required for the route to be accessible. In your application, you already have a page file: /app/page.tsx - this is the home page associated with the route /.

To create a nested route, you can nest folders inside each other and add page.tsx files inside them. For example:
![Alt text](notes_images/image_2.png)

By having a special name for page files, Next.js allows you to colocate UI components, test files, and other related code with your routes. Only the content inside the page file will be publicly accessible. For example, the /ui and /lib folders are colocated inside the /app folder along with your routes.


## how does next.js optimize images?
Preventing layout shift automatically when images are loading.
Resizing images to avoid shipping large images to devices with a smaller viewport.
Lazy loading images by default (images load as they enter the viewport).
Serving images in modern formats, like WebP and AVIF, when the browser supports it.

you don't have to worry about:
    Ensure your image is responsive on different screen sizes.
    Specify image sizes for different devices.
    Prevent layout shift as the images load.
    Lazy load images that are outside the user's viewport.

## why optimize fonts
CSS Modules allow you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about style collisions as well.

## how does nextjs optimize fonts
Next.js automatically optimizes fonts in the application when you use the next/font module. It downloads font files at build time and hosts them with your other static assets. This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

## what is next JS, defined simply?
https://www.youtube.com/watch?v=BILxV_vrZO0

stages of web dev:
1. documents with links between them
- when a browser made a request to a server for a particular page, the server would find the html file stored on its hard drive and send it back to the browser
- everything was static. every user received the exact same static experience.
2. servers started preprocessing html before it was sent to the client. 
- everytime a browser would request a page, based on the user's cookies or auth heads, the server would generate the html on the fly for that user
- even tho pages were being dynamically created on the server, the end result was still a static experience
3. to make static pages more interactive, js was created (in 10 days by one man)er 
- it was named javascript because it was the sidekick language to java
- was used for pop ups and such 
4. in 1999, ajax was invented. it allowed browsers to send and receive data from the server without needing to reload the page
5. there was dom manipulation with jQuery
6. in 2011, Angular was invented
7. React was invented, the View was a function of your app state. all you had to do was worry about how the state of your application changed, and react would handle the rest

- in single page applications instead of making a new request every time a user visited a page, your app loads all the needed components on the initial request. subsequent transitions happen entirely on the client. this gives the app a native like feel. 

what are the problems with SPAs?
- by their nature, spas tend to encourage large bundle sizes if you're not careful. this is problematic for users with slow interenet connections or on mobile devices. 
- data is loaded on an as-needed basis
    - this can lead to every route transition being met with a barrage of loading spinners
- SEO is less than ideal because you are relying on google's ability to execute your js before its able to figure out the content of your page

what was the problem with react?
- the majority of websites will never face the problems react was designed to solve and foks underestimate the real world cost of too much javascript
-  it was also hard to get started with

8. create react app is created to get react up and running easily
end.

spas should exist, but they should not be the default way we create applciations. the solution is NextjS

NextJS provides
- simplicity of the documen era
- power of the ssr era
- composition of the React era
- UX of the SPA era

How does it work?
- nextJS is built on top of React
- this lets React be a UI framework and nothing else
- to create a new page in your app with nextJS, you just add a file in the pages directory that exports a react component describing the UI for that page
- by default, nextJS will statically generate the page at build time and serve up the HTML for every request
- unlike websites of old, if that page needs external data that can be fetched at build time, you just export a get static props function which fetches and 
returns the data which will then be passed as props to the component
- if your page needs data that can't be fetched at build time you have 2 choices
    - server render page (fetch data on server)
    - fetch data on client
- nextJS lets you pick when you want to use fetch data (build time or as users user your app)
- you get improved performance! images are only loaded when you enter the viewpoert for ex.
- you can create api routes without having to spin up your own server

## what is the difference between the App router and the pages router
App router:
   - server centric routing
   - support for server components
   - more complex
   - better performance
   - more flexible
Pages router:
   - client side routing
   - no support for server components
   - simpler
   - worse performance
   - less felxible

## ExpressJS vs NextJS
- https://stackoverflow.com/questions/69918766/nextjs-vs-express

## Is Next.js front end or back end?
Next.js is mainly focused on the frontend, specifically React applications. It handles rendering React components on the server (Server-Side Rendering) and also supports generating static sites (Static Site Generation). This is different from Express.js, which is a backend framework used for handling HTTP requests, middleware, and routing on the server.

## give me a couple good ideas for fullstack projects which use NextJS, GraphQL, Docker, Kubernetes, Spring, Redux
1. E-commerce Platform
Project Description: Develop a scalable and efficient e-commerce platform. This platform could include features like product listings, a shopping cart, user authentication, order management, and payment processing.

Frontend: Use Next.js for server-side rendering to improve SEO and performance, and Redux for state management.
Backend: Spring Boot can be the core for creating RESTful or GraphQL APIs. GraphQL can be used for efficient data fetching, particularly useful for complex product data and user accounts.
Database & Storage: Integrate a database like PostgreSQL for storing product and user data. Utilize cloud storage for product images and assets.
Docker & Kubernetes: Containerize the application using Docker for consistency across environments and deploy using Kubernetes for orchestration, scaling, and management.
Additional Features: Implement features like product recommendations, reviews, and a sophisticated search functionality.
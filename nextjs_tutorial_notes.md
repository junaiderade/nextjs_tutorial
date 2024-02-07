# README
## on ch2

## general
- this code is written based off this doc for the app router course:
https://nextjs.org/learn/dashboard-app


## project structure
/app: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
/app/lib: Contains functions used in your application, such as reusable utility functions and data fetching functions.
/app/ui: Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
/public: Contains all the static assets for your application, such as images.
/scripts: Contains a seeding script that you'll use to populate your database in a later chapter.
Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.
app/lib/placeholder-data.js: contains placehodler data

## testing
- run npm i and npm run dev (starts app on port 300)

# Errors 

# Terminal commands

## initializing project
npx create-next-app@latest nextjs-dashboard --use-npm --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example"

# Definitions

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
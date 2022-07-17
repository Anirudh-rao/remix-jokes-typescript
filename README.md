# Remix Jokes Application

This Repo is Created from the official Remix Docs  [Click here](https://remix.run/docs/en/v1/tutorials/jokes) 

**Remix** is a new FullStack Javascript FrameWork that allows us to create full Stack Applictions with ease.


## To Get Started:
1. Use the Command `npx create-remix@latest` 
2. You'll be Prompeted Certain Features  Select as follows:
    ```
    ? Where would you like to create your app? **remix-jokes**
    ? What type of app do you want to create? Just the basics
    ? Where do you want to deploy? Choose Remix App Server if you're unsure; it's easy to change deployment targets. **Remix App Server**
    ? TypeScript or JavaScript? **TypeScript**
    ? Do you want me to run `npm install`? **Yes**
    ```
3. Once completed `cd remix-jokes` and run `npm run dev` to get Started

## Exploring Project Structure:
```
remix-jokes
├── README.md
├── app
│   ├── entry.client.tsx
│   ├── entry.server.tsx
│   ├── root.tsx
│   └── routes
│       └── index.tsx
├── package-lock.json
├── package.json
├── public
│   └── favicon.ico
├── remix.config.js
├── remix.env.d.ts
└── tsconfig.json
```

Let's talk briefly about a few of these files:

1. `app/` - This is where all your Remix app code goes
2. `app/entry.client.tsx` - This is the first bit of your JavaScript that will run when the app loads in the browser. We use this file to hydrate our React components.
3. `app/entry.server.tsx`- This is the first bit of your JavaScript that will run when a request hits your server. Remix handles loading all the necessary data and you're responsible for sending back the response. We'll use this file to render our React app to a string/stream and send that as our response to the client.
4. `app/root.tsx` - This is where we put the root component for our application. You render the <html> element here.
5. `app/routes/` - This is where all your "route modules" will go. Remix uses the files in this directory to create the URL routes for your app based on the name of the files.
6. `public/` - This is where your static assets go (images/fonts/etc)
7. `remix.config.js` - Remix has a handful of configuration options you can set in this file.

Let's go ahead and run the build:
```
npm run build
```

That should output something like this:
```
Building Remix app in production mode...
Built in 132ms
```

Now you should also have a `.cache/ directory` (something used internally by Remix), a `build/ directory`, and a `public/build` directory. The build/ directory is our server-side code. The `public/build/`holds all our client-side code. These three directories are listed in your `.gitignore file`so you don't commit the generated files to source control.

Let's run the built app now:
```
npm start
```
This will start the server and output this:
```
Remix App Server started at http://localhost:3000
```

***
The <LiveReload /> component is useful during development to auto-refresh our browser whenever we make a change. Because our build server is so fast, the reload will often happen before you even notice ⚡
***

Your `app/ directory` should now look like this:
```
app
├── entry.client.tsx
├── entry.server.tsx
└── root.tsx
```

With that set up, go ahead and start the dev server up with this command:
```
npm run dev
```

## Routes

The first thing we want to do is get our routing structure set up. Here are all the routes our app is going to have:
```
/
/jokes
/jokes/:jokeId
/jokes/new
/login
```

You can programmatically create routes via the `remix.config.js`, but the more common way to create the routes is through the file system. This is called **"file-based routing."**

Each file we put in the app/routes directory is called a **"Route Module"**and by following the route filename convention, we can create the routing URL structure we're looking for. Remix uses React Router under the hood to handle this routing.


## Parametarized Routes

Soon we'll add a database that stores our jokes by an ID, so let's add one more route that's a little more unique, a parameterized route:
```
/jokes/:jokeId
```
Here the parameter `$jokeId` can be anything, and we can lookup that part of the URL up in the database to display the right joke. To make a parameterized route, we use the $ character in the filename. (Read more about the convention [here](https://remix.run/docs/en/v1/api/conventions#route-filenames)).

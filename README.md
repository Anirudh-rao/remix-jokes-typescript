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

Each file we put in the app/routes directory is called a **Route Module** and by following the route filename convention, we can create the routing URL structure we're looking for. Remix uses React Router under the hood to handle this routing.


## Parametarized Routes

Soon we'll add a database that stores our jokes by an ID, so let's add one more route that's a little more unique, a parameterized route:
```
/jokes/:jokeId
```
Here the parameter `$jokeId` can be anything, and we can lookup that part of the URL up in the database to display the right joke. To make a parameterized route, we use the $ character in the filename. (Read more about the convention [here](https://remix.run/docs/en/v1/api/conventions#route-filenames)).

## Styling

From the beginning of styling on the web, to get CSS on the page, we've used `<link rel="stylesheet" href="/path-to-file.css" />`. This is how you style your Remix applications as well, but Remix makes it much easier than just throwing link tags all over the place. 
Remix brings the power of its Nested Routing support to CSS and allows you to associate links to routes. When the route is active, the `link` is on the page and the CSS applies. When the route is not active (the user navigates away), the `link` tag is removed and the CSS no longer applies.

You do this by exporting a [links](https://remix.run/docs/en/v1/api/conventions#links) function in your route module.


Now if you go to `/ `you may be a bit disappointed. Our beautiful styles aren't applied! Well, you may recall that in the app/root.tsx we're the ones rendering everything about our app. From the `<html>` to the `</html>`. That means if something doesn't show up in there, it's not going to show up at all!

So we need some way to get the `link`exports from all active routes and add `<link />` tags for all of them. Luckily, Remix makes this easy for us by providing a convenience `<Links />` component.


🤯 What is this? Why aren't the CSS rules applied? Did the body get removed or something?! Nope. If you open the Elements tab of the dev tools you'll notice that the link tag isn't there at all!

```
This means that you don't have to worry about unexpected CSS clashes when you're writing your CSS. You can write whatever you like and so long as you check each route your file is linked on you'll know that you haven't impacted other pages! 🔥

This also means your CSS files can be cached long-term and your CSS is naturally code-split. Performance FTW ⚡
```

One quick note about CSS. A lot of you folks may be used to using runtime libraries for CSS (like [Styled-Components](https://styled-components.com/)). While you can use those with Remix, we'd like to encourage you to look into more traditional approaches to CSS. Many of the problems that led to the creation of these styling solutions aren't really problems in Remix, so you can often go with a simpler styling approach.

That said, many Remix users are very happy with [Tailwind](https://tailwindcss.com/) and we recommend this approach. Basically, if it can give you a URL (or a CSS file which you can import to get a URL), then it's a generally a good approach because Remix can then leverage the browser platform for caching and loading/unloading.

## Database

Most real-world applications require some form of data persistence. In our case, we want to save our jokes to a database so people can laugh at our hilarity and even submit their own (coming soon in the authentication section!).

You can use any persistence solution you like with Remix; [Firebase](https://firebase.google.com/), [Supabase](https://supabase.com/), [Airtable](https://www.airtable.com/), [Hasura](https://hasura.io/), [Google Spreadsheets](https://www.google.com/sheets/about/), [Cloudflare Workers KV](https://www.cloudflare.com/products/workers-kv/), [Fauna](https://fauna.com/features), a custom [PostgreSQL](https://www.postgresql.org/), or even your backend team's REST/GraphQL APIs. Seriously. Whatever you want.

#### Set up Prisma:
```
The prisma team has built a VSCode extension you might find quite helpful when working on the prisma schema.
```

In this tutorial we're going to use our own `SQLite database`. Essentially, it's a database that lives in a file on your computer, is surprisingly capable, and best of all it's supported by **Prisma** , our favorite database ORM! It's a great place to start if you're not sure what database to use.

There are two packages that we need to get started:

1. `prisma` for interacting with our database and schema during development.
2. `@prisma/client` for making queries to our database during runtime.


Install the prisma packages:
```
npm install --save-dev prisma
npm install @prisma/client
```
 Now we can initialize prisma with sqlite:
```
npx prisma init --datasource-provider sqlite
```

That gives us this output:
```
✔ Your Prisma schema was created at prisma/schema.prisma
  You can now open it in your favorite editor.

warn You already have a .gitignore. Don't forget to exclude .env to not commit any secret.

Next steps:
1. Set the DATABASE_URL in the .env file to point to your existing database. If your database has no tables yet, read https://pris.ly/d/getting-started
2. Run prisma db pull to turn your database schema into a Prisma schema.
3. Run prisma generate to generate the Prisma Client. You can then start querying your database.

More information in our documentation:
https://pris.ly/d/getting-started

```

Now that we've got prisma initialized, we can start modeling our app data. Because this isn't a prisma tutorial, I'll just hand you that and you can read more about the prisma schema from their [docs](https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference):

**prisma/schema.prisma**
```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}

model Joke {
  id         String   @id @default(uuid())
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
  name       String
  content    String
}
```

With that in place, run this:
```
npx prisma db push
```

This command will give you this output:
```
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
Datasource "db": SQLite database "dev.db" at "file:./dev.db"

🚀  Your database is now in sync with your schema. Done in 194ms

✔ Generated Prisma Client (3.5.0) to ./node_modules/
@prisma/client in 26ms

```
This command did a few things. For one, it created our database file in prisma/dev.db. Then it pushed all the necessary changes to our database to match the schema we provided. Finally it generated Prisma's TypeScript types so we'll get stellar autocomplete and type checking as we use its API for interacting with our database.

Let's add that `prisma/dev.db` to our `.gitignore` so we don't accidentally commit it to our repository. We'll also want to add the `.env `file to the `.gitignore `as mentioned in the prisma output so we don't commit our secrets!
```
node_modules

/.cache
/build
/public/build

/prisma/dev.db
.env
```

```
If your database gets messed up, you can always delete the prisma/dev.db file and run npx prisma db push again. Remember to also restart your dev server with npm run dev.

```

Now we just need to run this file. We wrote it in `TypeScript` to get type safety (this is much more useful as our app and data models grow in complexity). So we'll need a way to run it.
 
Install esbuild-register as a dev dependency:
```
npm install --save-dev esbuild-register
```

And now we can run our seed.ts file with that:
```
node --require esbuild-register prisma/seed.ts
```
Now our database has those jokes in it. No joke!

But I don't want to have to remember to run that script any time I reset the database. Luckily, we don't have to!

Add this to your package.json:
```
// ...
  "prisma": {
    "seed": "node --require esbuild-register prisma/seed.ts"
  },
  "scripts": {
// ...

```
Now, whenever we reset the database, prisma will call our seeding file as well.

#### Connect to Database:
Ok, one last thing we need to do is connect to the database in our app. We do this at the top of our prisma/seed.ts file:
```
import { PrismaClient } from "@prisma/client";
const db = new PrismaClient();
```
This works just fine, but the problem is, during development, we don't want to close down and completely restart our server every time we make a server-side change. So `@remix-run/serve` actually rebuilds our code and requires it brand new. The problem here is that every time we make a code change, we'll make a new connection to the database and eventually run out of connections! This is such a common problem with database-accessing apps that Prisma has a warning for it:

**Warning: 10 Prisma Clients are already running**

So we've got a little bit of extra work to do to avoid this development time problem.

**Note** that this isn't a remix-only problem. Any time you have "live reload" of server code, you're going to have to either disconnect and reconnect to databases (which can be slow) or do the workaround I'm about to show you.


I'll leave analysis of this code as an exercise for the reader because again, this has nothing to do with Remix directly.

The one thing that I will call out is the file name convention. The `.server` part of the filename informs Remix that this code should never end up in the browser. This is optional, because Remix does a good job of ensuring server code doesn't end up in the client. But sometimes some server-only dependencies are difficult to treeshake, so adding the .server to the filename is a hint to the compiler to not worry about this module or its imports when bundling for the browser. The `.server` acts as a sort of boundary for the compiler.


#### Read from Database in Remix loader:

Ok, ready to get back to writing Remix code? Me too!

Our goal is to put a list of jokes on the `/jokes `route so we can have a list of links to jokes people can choose from. In Remix, each route module is responsible for getting its own data. So if we want data on the `/jokes route`, then we'll be updating the `app/routes/jokes.tsx `file.

To load data in a Remix route module, you use a [loader](https://remix.run/docs/en/v1/api/conventions#loader). This is simply an async function you export that returns a response, and is accessed on the component through the [useLoaderData](https://remix.run/docs/en/v1/api/remix#useloaderdata) hook. 


```
Remix and the tsconfig.json you get from the starter template are configured to allow imports from the app/ directory via ~ as demonstrated above so you don't have ../../ all over the place.
```


#### Data Overfetching

I want to call out something specific in my solution. Here's my loader:
```

type LoaderData = {
  jokeListItems: Array<{ id: string; name: string }>;
};

export const loader: LoaderFunction = async () => {
  const data: LoaderData = {
    jokeListItems: await db.joke.findMany({
      take: 5,
      select: { id: true, name: true },
      orderBy: { createdAt: "desc" },
    }),
  };
  return json(data);
};

```
Notice that all I need for this page is the joke `id` and `name`. I don't need to bother getting the content. I'm also limiting to a total of`5` items and ordering by creation date so we get the latest jokes. So with prisma, I can change my query to be exactly what I need and avoid sending too much data to the client! That makes my app faster and more responsive for my users.

And to make it even cooler, you don't necessarily need prisma or direct database access to do this. You've got a graphql backend you're hitting? Sweet, use your regular graphql stuff in your loader. It's even better than doing it on the client because you don't need to worry about shipping a [huge graphql client](https://bundlephobia.com/package/graphql@16.0.1) to the client. Keep that on your server and filter down to what you want.

Oh, you've just got REST endpoints you hit? That's fine too! You can easily filter out the extra data before sending it off in your loader. Because it all happens on the server, you can save your user's download size easily without having to convince your backend engineers to change their entire API. Neat!

#### Network Safety

In our code we're using the `useLoaderData's` type generic and specifying our `LoaderData` so we can get nice auto-complete, but it's not really getting us type safety because the loader and the `useLoaderData` are running in completely different environments. Remix ensures we get what the server sent, but who really knows? Maybe in a fit of rage, your co-worker set up your server to automatically remove references to dogs (they prefer cats).

So the only way to really be 100% positive that your data is correct, you should use [assertion functions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#assertion-functions) on the data you get back from useLoaderData. That's outside the scope of this tutorial, but we're fans of [zod](https://www.npmjs.com/package/zod) which can aid in this.


# Mutations
We've got ourselves a `/jokes/new route`, but that form doesn't do anything yet. Let's wire it up! As a reminder here's what that code should look like right now (the method="post" is important so make sure yours has it):

*app/routes/jokes/new.tsx*
```

export default function NewJokeRoute() {
  return (
    <div>
      <p>Add your own hilarious joke</p>
      <form method="post">
        <div>
          <label>
            Name: <input type="text" name="name" />
          </label>
        </div>
        <div>
          <label>
            Content: <textarea name="content" />
          </label>
        </div>
        <div>
          <button type="submit" className="button">
            Add
          </button>
        </div>
      </form>
    </div>
  );
}

```

Not much there. Just a form. What if I told you that you could make that form work with a single export to the route module? Well you can! It's the [action](https://remix.run/docs/en/v1/api/conventions#action) function export! Read up on that a bit.

If you've got that working, you should be able to create new jokes and be redirected to the new joke's page.
```

The redirect utility is a simple utility in Remix for creating a Response object that has the right headers/status codes to redirect the user.

```


Hooray! How cool is that? No `useEffect` or `useAnything hooks`. Just a form, and an async function to process the submission. Pretty cool. You can definitely still do all that stuff if you wanted to, but why would you? This is really nice.

Another thing you'll notice is that when we were redirected to the joke's new page, it was there! But we didn't have to think about updating the cache at all. Remix handles invalidating the cache for us automatically. You don't have to think about it. That is cool 😎

Why don't we add some validation? We could definitely do the typical React validation approach. Wiring up useState with `onChange`handlers and such. And sometimes that's nice to get some real-time validation as the user's typing. But even if you do all that work, you're still going to want to do validation on the server.

Before I set you off on this one, there's one more thing you need to know about route module action functions. The return value is expected to be the same as the loader function: A response, or (as a convenience) a serializable JavaScript object. Normally you want to redirect when the action is successful to avoid the annoying "confirm resubmission" dialog you might have seen on some websites.

But if there's an error, you can return an object with the error messages and then the component can get those values from [useActionData](https://remix.run/docs/en/v1/api/remix#useactiondata) and display them to the user.


Why don't you pop open my code example for a second. I want to show you a few things about the way I'm doing this.

First I want you to notice that I've added an `ActionData` type so we could get some type safety. Keep in mind that `useActionData` can return `undefined` if the action hasn't been called yet, so we've got a bit of defensive programming going on there.

You may also notice that I return the fields as well. This is so that the form can be re-rendered with the values from the server in the event that `JavaScript` fails to load for some reason. That's what the `defaultValue` stuff is all about as well.

The `badRequest` helper function is important because it gives us typechecking that ensures our return value is of type `ActionData`, while still returning the accurate HTTP status, [400 Bad Request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400), to the client. If we just return the `ActionData` value, that would result in a`200 OK` response, which isn't suitable since the form submission had errors.

Another thing I want to call out is how all of this is just so nice and declarative. You don't have to think about state at all here. Your action gets some data, you process it and return a value. The component consumes the action data and renders based on that value. No managing state here. No thinking about race conditions. Nothing.

Oh, and if you do want to have client-side validation (for while the user is typing), you can simply call the `validateJokeContent` and `validateJokeName` functions that the action is using. You can actually seamlessly share code between the client and server! Now that is cool!
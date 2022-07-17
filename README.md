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
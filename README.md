## Creating the nextjs project  

Navigate to a folder on your machine. In my case I navigated to the location "E:\Sudhanshu\Learning\nextjs" on my laptop.  

Right click inside the folder and you will see **Git Bash** if you have Git Scm installed on your machine.  

Creating the default nextjs app using create-next-app  

```
npx create-next-app nextjs-comment-system
```

The default nextjs project is created inside the folder **nextjs-comment-system**. Navigate to the project folder.
```
cd nextjs-comment-system
```

Go to the address bar of the windows explorer and type **cmd** and hit enter.  

The folder will open up in the command prompt.  

## Initializing the git repository

First let us configure our Git Bash to create **main** as the default branch rather than **master**

Enter the below mentioned command and hit enter.  
```
git config --global init.defaultBranch main
```
This will set **main** as the default branch.  

Initialize the repository.  
```
git init
git add .
git commit -m "Initial Commit"
```

The repository will the name of the folder will be initialized with the default branch as **main**.  

Let us open our project in VSCode with the below command on cmd and hit enter.  
```
code .
```

The project will open up in VSCode and we would be using VSCode as the code editor for our project.  

Push this newly created Git Repository to remote. You may be asked to provide the credentials of Github if you are doing it for the first time.  

Check the github account and you should see the newly pushed repository **nextjs-comment-system** with the Initial commit.  

Lets us create a new branch. We will use VSCode to create a new branch named **development** and push this to remote repo.  

We would be doing all our development work on this branch and merge the code to main once we have the code working till a logical
endpoint.  

You can run the app by ``npm run dev`` and navigate to the URL ``http:\\localhost:3000`` to see your app in action.  

## Cleaning up the boiler plate code

Let us remove all the boiler plate code from the app and start from scratch.  

Remove the jsx from index.js inside the pages folder. We will just keep an empty div.  

Remove the files from the styles folder and also the references of the styles from the code. We will configure tailwind and use 

the tailwind utility classes for styling.  

Remove the hello.js from the api folder within the pages folder.  

Note: If you want to preview the markdown you are editing right now press Ctrl+Shift+V on windows to preview.  

## Configuring Typescript in the project

You can create the nextjs app with typescript by default or you can configure the existing nextjs app to work with Typescript.  

Considering the features that Typescript have over JavaScript let is configure our project with TypeScript.  

If you are creating a project from scratch you can use the below mentioned command to create a nextjs app with typescript support.  
```
npx create-next-app@latest --ts
```

We would be migrating our nextjs app from javascript to typescript.  

create an empty tsconfig.json file in the root folder.  

If your app is already running exit the app by pressing Ctrl+c and rerun the app by ``npm run dev``. The terminal itself will guide you with the next steps to configure typescript.  

```js
It looks like you''re trying to use TypeScript but do not have the required package(s) installed.

Please install @types/react and @types/node by running:

    npm install --save-dev @types/react @types/node

If you are not trying to use TypeScript, please remove the tsconfig.json file from your package root (and any TypeScript files in your pages directory).       
```

Let us install the packages and then run the app with ``npm run dev``.  

You would notice that the tsconfig.json is populated with some default configuration and a file named ``next-env.d.ts`` file

is created in the root of the project.  

This file will make typescript aware of the types available in nextjs. You can turn on the ``strict`` feature of typescript in
the tsconfig.json file for typescript to report the type checking errors.  

Now the files in the project should be all .tsx instead of .js. Rename the file ``_app.js`` to ``_app.tsx``.  

As soon as you rename the file to .tsx the typescript type checking comes into action and the code inside ``_app.tsx`` starts
complaining.  

Replace the code inside the file with this one.  
```tsx
import type { AppProps } from 'next/app'

export default function MyApp({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}
```

Basically here we are trying to specify the type name that is passed to the MyApp function and the type is AppProps.  

You would notice that the import statement in _app.tsx still complains **Cannot find module 'next/app'. Did you mean to set the 'moduleResolution' option to 'node', or to add aliases to the 'paths' option?ts(2792)**  

To resolve this let us add the below key-value pair in the tsconfig.json right above the **resolveJsonModule**.  

```json
"moduleResolution": "node",
```

Rename the index.js file inside the pages folder to index.tsx. We are now done with the migration of our newly created nextjs
app from javascript to typescript.  

## Configuring the nextjs app to use tailwindcss for styling

Configuring tailwindcss with nextjs can be done manually or the nextjs project can be created with nextjs+tailwind example using the below command.
```
npx create-next-app --example with-tailwindcss with-tailwindcss-app
# or
yarn create next-app --example with-tailwindcss with-tailwindcss-app
```

In our case we would be doing the configuration manually by following the official guideline mentioned on the link below.

[Configuring Tailwind with nextjs](https://tailwindcss.com/docs/guides/nextjs)  

The steps include running the commands below.
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Add the following code to the newly created tailwind.config.js file.
```js
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Create the file ``globals.css`` in the styles folder and the the code below.
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Make sure that the file ``globals.css`` is imported in the ``_app.tsx`` for tailwindcss to reflect on the UI.  














# React TypeScript Shopping Cart Website
## Table of Contents

- [Intoduction](#Intro)

- [Installation](#Instalation)

- [Start](#Start)

- [Utilities](#Utilities)

- [Data](#Data)

- [Context](#Context)

- [Hooks](#Hooks)

- [Pages & Components](#Pages)

- [The End](#End)

## Intro
So this is a project that I saw on Youtube, that's why I want to honor Web Dev Simplified for this project.
This is a Shopping Cart, Amazon like website that uses many React features and is great for starters who want to learn it.
First of all, it uses browser routing using the BrowserRouter component from "react-router-dom".
Also, it incorporates custom hooks as well as advanced context functions.

## Start 
First to write this code you are going to need **npm node**. To install it go to this site: https://nodejs.org/en/download

When you have node, to create the project you are going to write:

```node
npm create vite@latest
```
Then, for the project name you write "." so the project is created inside of the current folder you're in.
Make sure the current directory you're in is empty, otherwise it will delete all the files in that directory.
Okay, now, using your arrow keys select React as a framework.
For the variant you can choose either **TypeScript** of **TypeScript + SWC**. If the SWC version doesn't work, choose just TypeScript.
Now run:
```node
npm install 
```
Then to run the project type:
```node
npm run dev
```
### Additional installations
For the styling and the routing you are going to need to install:
```node
npm install react-router-dom bootstrap react-bootstrap
```
Then to be sure that everything works as we want it to in the future, delete all the css files, all the assets and all the code inside the public folder.
To make it easier you can also delete all the code inside the App.tsx and main.tsx.

## Utilities
There is only one file inside the utilities, it's the *currency formater*.

### Currency formater
First, we initialise a currency formater. It will be a 
```ts
new Intl.NumberFormat(undefined, {currency: "USD", style: "currency"})
```
object. So the default currency is *US* dollars, but it will adapt to the location of the viewer of the site. And the style is currency, obviously.
Then we export the *formatCurrency* function that will use the currency formater to format any given number.
```ts
export function formatCurrency(number: number){
    return CURRENCY_FORMATER.format(number)
}
```

## Data
Inside the data folder we have only one **JSON** file.

Inside of it is an array containing 6 objects, but you can add as many as you want.
Every object has an **id** which is a number, a **name** which is a string, a **price** which is float (decimal number) and an **imgUrl** which is going to be a string, representing an url for the image of the product.
```json
[
  {
    "id": 1,
    "name": "Book",
    "price": 10.99,
    "imgUrl": "/img/book.jpg"
  },
  {
    "id": 2,
    "name": "Computer",
    "price": 1199,
    "imgUrl": "/img/computer.jpg"
  }
]
```

## Context
Inside the context folder we have only have one file, which is *shoppingCartContext.tsx*.

### Create Context React Hook
The **useContext()** hook in React is a way to access data and functions from the context of a parent component in a child component without having to pass props through every level of the component tree.
It allows you to share and retrieve values, such as state or functions, that are stored in a context object.
#### ***Create a Context:*** 
First, you define a context using 
```tsx
React.createContext()
```
or just 
```tsx
createContext()
```
This creates a context object that will hold the shared data and functions.

#### ***Provide Context***:
In a parent component, you use the **Context.Provider** component to wrap the part of the component tree where you want to share the context. 
You pass the data and functions as values to the **Provider**.

#### ***Access Context***:
In a child component, you can use the 
```tsx
useState()
```
hook to access the context's values. It takes the context object as an argument and returns the current context value.

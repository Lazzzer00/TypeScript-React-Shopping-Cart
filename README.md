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
First to write this code you are going to need npm node. To install it go to this site: https://nodejs.org/en/download
When you have node, to create the project you are going to write:

```node
npm create vite@latest
```
Then, for the project name you write "." so the project is created inside of the current folder you're in.
Make sure the current directory you're in is empty, otherwise it will delete all the files in that directory.
Okay, now, using your arrow keys select React as a framework.
For the variant you can choose either TypeScript of TypeScript + SWC. If the SWC version doesn't work, choose just TypeScript.
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

# React TypeScript Shopping Cart Website
## Table of Contents

- [Intoduction](#Intro)

- [Installation](#Instalation)

- [Utilities](#Utilities)

- [Data](#Data)

- [Hooks](#Hooks)

- [Context](#Context)

- [Pages & Components](#Pages)

- [The End](#End)

## Intro
So this is a project that I saw on Youtube, that's why I want to honor Web Dev Simplified for this project.
This is a Shopping Cart, Amazon like website that uses many React features and is great for starters who want to learn it.
First of all, it uses browser routing using the BrowserRouter component from "react-router-dom".
Also, it incorporates custom hooks as well as advanced context functions.

## Insallation
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

## Hooks

#### The **useLocalStorage.tsx** hook
It is a generic hook, which means it can work with any data type, and it takes 2 parameters:
- **key**: A string that serves as the identifier for the value in local storage.
- **intitialValue**: The initial value to be used if no value is found in local storage. It can be either a static value or a function that computes the initial value.
```tsx
export function useLocalStorage<T>(key: string, initialValue: T | (() => T)){}
```

Inside the hook:
- It uses the **useState** hook to initialize a **value** state variable. The initial value is provided as a function, which is executed to determine the initial state value.
- The code checks if there is a value stored in the local storage corresponding to the given **key**. If a value is found, it is parsed from **JSON** and used as the initial state.
- If no value is found in local storage, it checks if **initialValue** is a function and executes it to get the initial state. If **initialValue** is not a function, it uses it directly as the initial state.

The **useEffect** hook is used to save the **value** to local storage whenever it changes.
It creates an effect that listens for changes to both the **key** and the **value**. 
When either of them changes, it updates the value in local storage by stringifying the **value** and storing it under the given **key**.

The hook returns an array with 2 items:
- **value**: The current value stored in local storage and managed as part of the component's state.
- **setValue**: A function that can be used to update the **value** stored in local storage. This function can be called with a new value, and it will also update the state.
```tsx
export function useLocalStorage<T>(key: string, initialValue: T | (() => T)){
    const [value, setValue] = useState<T>(() => {
        const jsonValue = localStorage.getItem(key)
        if(jsonValue !== null) return JSON.parse(jsonValue)

        if(typeof initialValue === "function") return (initialValue as () => T)()
        else return initialValue
    })

    useEffect(() => {
        localStorage.setItem(key ,JSON.stringify(value))
    }, [key, value])

    return [value, setValue] as [typeof value, typeof setValue]
}
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

### Shopping Cart Context
#### *Shopping Cart Context Types*
First of all, we need 2 functions to open and close the cart.
```tsx
type ShoppingCartContext = {
    openCart: () => void
    closeCart: () => void
    ...
    ...
}   
```
Secondly, we need a function to get the quantity of an item so that we can update the counter. Then we need an increase and a decrease quantity function. And lastly, we need a remove from cart function for the remove button.
```tsx
type ShoppingCartContext = {
    openCart: () => void
    closeCart: () => void
    getItemQuantity: (id: number) => number
    increaseCartQuantity: (id: number) => void
    decreaseCartQuantity: (id: number) => void
    removeFromCart: (id: number) => void
    ...
    ...
}
```
Then we need to set a type for the **Cart Item**. 
```tsx
type CartItem = {
    id: number
    quantity: number
}
```
And lastly we need a counter for the total count of the items, we will call it **CartQuantity**. And we an array of all the **Cart Items**.
```tsx
type ShoppingCartContext = {
    openCart: () => void
    closeCart: () => void
    getItemQuantity: (id: number) => number
    increaseCartQuantity: (id: number) => void
    decreaseCartQuantity: (id: number) => void
    removeFromCart: (id: number) => void
    cartQuantity: number
    cartItems: CartItem[]
}
```
And at the end we declare:
```tsx
const ShoppingCartContext = createContext({} as ShoppingCartContext)
```
#### *UseShoppingCart & ShoppingCartProvider*
Inside of this filewe export 2 functions as components. 
##### *useShoppingCart* 
Inside of this we call **useContext** and pass it the **ShoppingCartContext**.
```tsx
export function useShoppingCart() {
    return useContext(ShoppingCartContext)
}
```
##### *ShoppingCartProvider*
###### *Props*
The function takes in an object with a parameter of children with a type of **ShoppingCartProviderProps**.
```tsx
type ShoppingCartProviderProps = {
    children: ReactNode
}

export function ShoppingCartProvider({ children }: ShoppingCartProviderProps){}
```
###### *State variables*
First we declare 4 variables:
```tsx
const [isOpen, setIsOpen] = useState(false)
const [cartItems, setCartItems] = useLocalStorage<CartItem[]>("shopping-cart", [])
```
Then we calculate the total cart quantity like this:
```tsx
const cartQuantity = cartItems.reduce((quantity, item) => item.quantity + quantity, 0)
```
And we declare 2 function for toggling the cart open and closed.
```tsx
const openCart = () => setIsOpen(true)
const closeCart = () => setIsOpen(false)
```
###### *Shopping Cart Context functions*
The first one is **getItemQuantity** which is pretty simple, it returns the quantity of the wanted item or 0 if the quantity is 0.
```tsx
function getItemQuantity(id: number) {
    return cartItems.find(item => item.id === id)?.quantity || 0
}
```

# Introduction To React

## Learning Objectives

By the end of this lesson, you should be able to:

- Understand what React is and what problem it solves.
- Use Vite to start a React project.
- Understand the role of the files and folders in Vite for React starter code.
- Create a simple application that uses React to render its front end.

<hr>

## Getting Started

This lesson will help you build a simple app demonstrating React with Vite's fundamental syntax, organization, and conventions.

The final app will look similar to this:

![In class build](../assets/class-build.png)

There are several ways to [create an application with React or add React to a current project](https://vitejs.dev/guide/). We'll use `Vite` (pronounced `veet`), which is a feature-rich application that has the following features:

- Automatic browser reloading when you make a change and other pre-configurations that make using it very easy
- Helpful error messages
- File and folder structure that is easy to use and maintain
- Configured for easy deployment

To use Vite to create a new app:

- `npm create vite@4 my-app`

Inside this project, you will see the following files.

```
.
├── node_modules
├── public
├── src
├── .eslintrc.cjs
├── .gitignore
├── index.html
├── package-lock.json
├── package.json
└── vite.config.js
```

> **Note:** If node modules are missing, use `npm install` to install the needed packages.

> Where will you build your application?

<details><summary>Answer</summary>

You will work inside the `src` folder.

</details>

To start your app:

```
npm run dev
```

Go to the **src/App.jsx** file.

What does each line of code do?

We will remove the **boilerplate** code for the rest of this lesson and add our code.

## Creating Components

This app is tiny. Production level apps are massive. One of the benefits of React is that it allows you to create small custom components. Each component is typically stored in its own file.

Inside the **src** folder, add a new file called `Header.jsx`.

Then, add a function called `Header`:

```js
// Header.jsx
function Header() {}
```

Add a return statement with parenthesis. Return statements can only return one line of code. The parenthesis allows you to space your HTML/JSX across multiple lines to make it easier to read and edit, but JavaScript will still read it as one line of code.

```js
// Header.js
function Header() {
 return ()
}
```

Add some JSX that will be rendered in the browser.

```js
// Header.jsx
function Header() {
  return (
    <header>
      <h1>My header</h1>
    </header>
  );
}
```

We want to use this code in `App.js`. To export this code, we must do so explicitly:

```js
// Header.js
function Header() {
  return (
    <header>
      <h1>My header</h1>
    </header>
  );
}

export default Header;
```

The default keyword allows the ability to rename this component in `App.jsx`.

Return to `App.jsx` and import this component:

```js
// App.jsx
import Header from "./Header";
```

Use this new custom component you've created:

```js
function App() {
 return (
 <Header />
 <div className="App">
 <h2>React is cool </h2>
 </div>
 );
}
```

This will cause an error. JSX expressions can have only one parent element. Let's move your custom header inside the `div`.

```js
function App() {
  return (
    <div className="App">
      <Header />
      <h2>React is cool </h2>
    </div>
  );
}
```

Inside of the div is a property `className`. What does it do?

Why can't you use the `class` keyword instead? [Hint](https://www.w3schools.com/js/js_reserved.asp)

## Duplicating Components

What happens when you add three headers?

```js
function App() {
  return (
    <div className="App">
      <Header />
      <Header />
      <Header />
      <h2>React is cool </h2>
    </div>
  );
}
```

## Children Components

Make a new file `Footer.jsx`:

```js
// Footer.jsx
function Footer() {
  return (
    <footer>
      <h3>Links</h3>
      <ul></ul>
    </footer>
  );
}

export default Footer;
```

Make a new file `Links.jsx`

```js
// Links.jsx
function Links() {
  return (
    <>
      <li>
        <a href="#">About</a>
      </li>
      <li>
        <a href="#">Contact</a>
      </li>
      <li>
        <a href="#">Legal</a>
      </li>
      <li>
        <a href="#">Jobs</a>
      </li>
    </>
  );
}

export default Links;
```

**Try it**: Add the Links component inside the Footer's unordered list.

Add the footer to `App.jsx`.

## Rendering Values

React renders data.

Currently, we have built a static app where nothing changes.

Let's demonstrate how to _embed_ (insert) data into JSX.

```js
// App.jsx
const photoOfTheDay = "https://loremflickr.com/320/240";
const currentDate = new Date();
```

Use curly braces for JSX to evaluate the inside value: `{}`.

```js
<Header />
<h2>React is cool</h2>
<img src={photoOfTheDay} alt={currentDate} />
<Footer />
```

## Using CSS

There are several ways to include CSS in a Create React App.

You will notice some default styles have been placed in **src/index.css**. This is an excellent place to store CSS that should impact the entire app. For example, making sure the whole app has the same base font.

Another way to add CSS is to add it for every component. This will assist in keeping your CSS code organized.

Create a file `Footer.css`.

```css
/* Footer.css */

footer {
  background: Gainsboro;
}
```

Import this code into **Footer.jsx**

```js
// Footer.jsx
import "Footer.css";
```

> **Note**: Now, many files are in the `src` folder. To keep projects maintainable and files easily findable, you can add more folders to organize your components.

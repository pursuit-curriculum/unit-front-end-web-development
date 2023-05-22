# Events

Interactive web applications are possible because JavaScript can respond to user interactions (called `events`). While some elements have default behaviors, such as links, you can make your page more interactive so that any click, hover, or mouseover can change what's happening on the page.

When you interact with a web page, you do things like drag your mouse, click on things and press on the keyboard (these are all `events`). It is possible to write code to listen for these events. For example, you can write code to `listen for a click on some button` and then `handle` the event by opening a pop-up menu.

In this lesson, you'll learn how to set up `event listeners` and `event handlers` with JavaScript for web pages.

Event listeners and handlers always go together. They describe two parts of one method. `Listeners` describe which elements (`button`, `h1`, etc.) and events (`click`, `hover` etc.) will be actively listening. `Handlers` describe the action taken when the event has happened (open a pop-up, validate some input, etc. )

## Learning Objectives

By the end of this lesson, you should be able to:

- Use event listeners to run code on specific user interactions such as click and hover.
  Dynamically add event listeners to created elements.
- Access data inside of the `event` object to dynamically change the effect of a listener.
- Use `event.target` to select the element that triggered an event listener.

---

## Event listeners

You may read or code along with the reading. If you want to code along, create a new project with an `index.html` and `app.js` file and connect them.

<details><summary>Optional Starter code</summary>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <script src="script.js" defer></script>
    <title>Clicker Counter</title>
  </head>
  <body>
    <h1>Click count: <span>0</span></h1>
    <section>
      <button>Click Me!</button>
      <button>No, me!</button>
      <button>Click me, I'm the best!</button>
    </section>
    <style>
      h1 {
        color: blue;
      }

      h1 span {
        color: midnightblue;
      }

      button {
        background: white;
        margin: 0;
        padding: 10px;
      }
    </style>
  </body>
</html>
```

</details>

You can attach an event listener to anything you select within the DOM. An event listener watches for certain events to occur on the DOM, at which point it responds. For example, the event listener below will run a `console.log()` message whenever the first h1 on the page is clicked.

First, select the element:

```js
const h1 = document.querySelector("h1");
```

Then add an event listener. The event listener is a method that takes two arguments.

The first is a string that is the name of the event, `click` is a very common event.

Then the second argument is a callback function. This callback function is the `event handler`, this is where you will write whatever functionality to occur once the element has been clicked on

```js
h1.addEventListener("click", () => {});
```

In this case, add a simple console log and see it in the dev tools console:

```js
h1.addEventListener("click", () => {
  console.log("You are clicking the first h1 on the page!");
});
```

### Event types

There are a large number of event types. However, only a few are most commonly used in applications. Below is a list of the most common:

| Event Type    | Description                                                           |
| ------------- | --------------------------------------------------------------------- |
| `"click"`     | Watches for when the user clicks on the target.                       |
| `"dblclick"`  | Watches for when the user double clicks on the target.                |
| `"mousedown"` | Watches for when the user has a mouse button pressed over the target. |
| `"mouseover"` | Watches for when the mouse hovers over the target.                    |
| `"mouseout"`  | Watches for when the mouse leaves the target.                         |
| `"focus"`     | Watches for when a form field has the cursor.                         |
| `"blur"`      | Watches for when the cursor leaves a form field.                      |
| `"change"`    | Watches for when a form field has changed somehow.                    |
| `"submit"`    | Watches for when a form has been submitted.                           |

Resources like MDN and W3 Schools have a more thorough list of all the events that occur. There is no need to memorize the lists, you can always look up the syntax once you understand the concept.

- [MDN: Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)

### F

### Adding event listeners to node lists

Recall that to get more than one HTML element(node), you need to use the `querySelectorAll()` method and that it returns a `node list`, which is an array-like data structure.

The `.addEventListener()` method can only be called on individual nodes, not node lists. You must loop over any list to add an event listener to multiple elements.

If you would like to add an event to each button, fist you must select each button.

You cannot add an event to each node in one step. Instead, you must loop over each node and add the event listener/handler individually.

```js
const buttons = document.querySelectorAll("button");
// loop over each button to add an event.
for (let button of buttons) {
  button.addEventListener("click", () => {
    console.log("A button was clicked!");
  });
}
```

You can select the `span` tag and update the value for every click. Notice that `querySelector` uses the same kind of selection strategies as CSS.

```js
let count = 0;
const span = document.querySelector("h1 span");
```

Replace the console log with the following code in the event handler:

```js
button.addEventListener("click", () => {
  count++;
  span.textContent = count;
});
```

Your counter should now increase with any button click.

### Adding event listeners dynamically

Take a look at the following HTML and associated JavaScript. Before reading the paragraph below, take the time to determine what should happen when a `li` is clicked. If you would like to code along, you can use the same project, but add a new section element below the other section element.

```html
<!-- index.html -->
<section>
  <ol>
    <li>Click me to make more!</li>
  </ol>
</section>
```

```js
// script.js
const lis = document.querySelectorAll("li");
for (let li of lis) {
  li.addEventListener("click", () => {
    const ol = document.querySelector("ol");
    const newLi = document.createElement("li");
    newLi.textContent = "Click me to make more!";
    ol.append(newLi);
  });
}
```

Did you take a bit of time to think about what would happen? The code above will add an event listener to the page so that a new `li` element will be added when a `li` element is clicked.

However, there is a problem. When clicked, each **newly** created `li` _will not_ make a `li`. This is because, when the JavaScript runs, there is only a single `li` on the page. Those `li` elements created in the future do not have an event listener!

There are a few clever ways to solve this. For now, remember that you'll need to add event listeners to the DOM elements you create.

Here is a possible solution:

```js
const lis = document.querySelectorAll("li");
function generateLiHandler() {
  const ol = document.querySelector("ol");
  const newLi = document.createElement("li");
  newLi.textContent = "Click me to make more!";
  ol.append(newLi);
  newLi.addEventListener("click", generateLiHandler);
}

for (let li of lis) {
  li.addEventListener("click", generateLiHandler);
}
```

## The event object

The callback function that event listeners expect has a parameter called `event`. It is an object that contains helpful information about the event that was triggered as well as the target of that event.

```js
const h1 = document.querySelector("h1");
h1.addEventListener("mouseover", (event) => {
  console.log("event.type:", event.type);
  console.log("event.target.textContent:", event.target.textContent);
});
```

In the code above, properties from the `event` object are printed out when the first `h1` element on the page is clicked. `event.type` will print the word "click", since that is the type of event that occurred. The `event.target` is the actual element that was clicked. Therefore, asking for that element's `.textContent` will return whatever text is in the `h1` element.

Notice you can add more than one listener to an element.

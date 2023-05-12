# Forms with Events

Forms and their various fields work a bit differently than other HTML elements. They store the data inside of them differently and have different types of events they can trigger.

This lesson will teach you the basics of working with forms and events. First, you'll learn how to access the data from specific form fields. Then, you'll learn how to add event listeners to forms so they can do whatever you like instead of performing their default behavior.

## Learning Objectives

By the end of this lesson, you should be able to:

- Access data directly from form fields.
- Describe and utilize `event.preventDefault()` to stop the default behavior of certain events.
- Capture the data submitted in a form using the `name` attribute and the `event` object.

---

## Accessing data from form fields

Recall that to access the text inside most elements. You can use the `.textContent` property.

```html
<!-- index.html -->
<p>Parable of the Sower by Octavia E. Butler</p>
```

```js
// main.js
const paragraph = document.querySelector("p");
console.log(paragraph.textContent);
```

This will not work for form fields. Instead, to access the value of a form field, you should use the `.value` property. This will return the current value of the form field. In the case of text inputs, this means returning whatever has been typed inside the field.

```html
<!-- index.html -->
<label>
  Book Title
  <input id="title" name="title" type="text" />
</label>
```

```js
// main.js
const title = document.querySelector("input[type='text']");
console.log(title.value);
```

For dropdowns (i.e., `select` elements), `.value` will work as well, as long as your `option` elements include `value` attributes.

```html
<!-- index.html -->
<label>
  Genre
  <select id="genre" name="genre">
    <option>-- Choose a Genre --</option>
    <option value="non-fiction">Non-fiction</option>
    <option value="fantasy">Fantasy</option>
    <option value="sci-fi">Sci-fi</option>
    <!-- ... -->
  </select>
</label>
```

```js
// main.js
const genre = document.querySelector("select");
console.log(genre.value);
```

However, input types that can be "checked", such as radio buttons and checkboxes, will always return the same value. This is because a `value` attribute is associated with each input. Instead, you can use the `.checked` property to determine whether or not that input is checked. The `.checked` property will return a boolean value depending on whether or not the input is checked.

```html
<!-- index.html -->
<fieldset>
  <legend>Genres</legend>
  <label>
    Non-fiction
    <input
      id="genre-non-fiction"
      type="checkbox"
      name="genre"
      value="non-fiction"
    />
  </label>
  <label>
    Fantasy
    <input id="genre-fantasy" type="checkbox" name="genre" value="fantasy" />
  </label>
  <!-- ... -->
</fieldset>
```

```js
// main.js
const nonFiction = document.querySelector("#genre-non-fiction");
console.log(nonFiction.value); //> non-fiction
console.log(nonFiction.checked); //> false
```

## Default behaviors

As you may have seen already, some elements have a default behavior. For example, links attempt to send the user to a different place, either on the same page or another page. Similarly, forms have the default behavior of sending a request. This typically leads to the page being refreshed when specific attributes are missing from the form field.

Some of these behaviors are undesirable when working with JavaScript on the front end. Thankfully, it is possible to stop the behaviors using a method built-in to the `event` object: `.preventDefault()`.

`event.preventDefault()` does just what it says: it prevents the default event from being fired. For an example, look below.

```html
<!-- index.html -->
<form id="new-book">
  <label>
    Book Title
    <input id="title" name="title" type="text" />
  </label>
  <label>
    Book Author
    <input id="author" name="author" type="text" />
  </label>
  <input type="submit" value="Create New Book" />
</form>
```

```js
// main.js
const form = document.querySelector("form");
form.addEventListener("submit", (event) => {
  event.preventDefault();

  const title = document.querySelector("#title");
  console.log(title.value);

  const author = document.querySelector("#author");
  console.log(author.value);
});
```

In the JavaScript code above, the following is happening:

1. The form element is selected and assigned to a variable.
1. An event listener is added to the element. The callback function will run when the "submit" event is triggered.
1. Inside the callback function, `event.preventDefault()` is called. This stops the form from refreshing the page. If you use `event.preventDefault()`, you should always put it first in the event listener.
1. The values from the `#title` and `#author` inputs are logged out.

The `event.preventDefault()` method is commonly used with forms. However, it can be used with other elements like links and form fields.

## Accessing form data

In the previous example, each value was accessed from each form field. While it's possible to do this, there is a better way.

When submitting a form, it is possible to access all form fields in the form from the `event` object. If a `name` attribute is added to the form field, a new property with that same name will be added to the `event.target` element.

```html
<!-- index.html -->
<form id="new-book">
  <label>
    Book Title
    <input id="title" name="title" type="text" />
  </label>
  <label>
    Book Author
    <input id="author" name="author" type="text" />
  </label>
  <input type="submit" value="Create New Book" />
</form>
```

```js
// main.js
const form = document.querySelector("form");
form.addEventListener("submit", (event) => {
  event.preventDefault();

  console.log(event.target.title.value); // Value of Book Title
  console.log(event.target.author.value); // Value of Book Author
});
```

If the name refers to multiple inputs, as would be the case with checkboxes or radio buttons, the property on `event.target` will return a node list. This can be looped through to access each value and "checked" status.

```js
const form = document.querySelector("form");
form.addEventListener("submit", (event) => {
  event.preventDefault();

  // A list of all checkboxes with the name "genre".
  const genres = event.target.genre;

  for (let genre of genres) {
    console.log(genre.value, genre.checked);
  }
});
```

# Forms with Events

## Learning Objectives

By the end of this lesson, you should be able to:

- Access data directly from form fields.
- Describe and utilize `event.preventDefault()` to stop the default behavior of certain events.
- Capture the data submitted in a form using the `name` attribute and the `event` object.
- Combine DOM knowledge to build a small CRUD application

---

## Setup

Begin by forking the following project.

- [Repl.it: Address Book](https://replit.com/@Pursuit/Events-with-Forms-Address-Book)

## Guiding questions

- Take a look at the form that exists in the project. How many of the fields are required?

- When you click the "Create Contact" button, what happens? Why?

- In the `scripts/main.js` file, write code that prevents the form from submitting. What event type did you have to use? What method from the `event` object did you have to use?

- On submit, log out the value inputted into the "Contact Name" field. What are two ways you could access this data?

- The `event.target` object should hold references to each field within the form. However, at least one field is missing. Why? How can it be fixed?

After you discover the issue, fix it.

- Update your code so that every value is logged out on submission. Then, add the contact to the page and use the `generateContact()` function in the `scripts/generateContact.js` file.

- After submitting, the form fields are not cleared. How could you do so?

- Take a look at [this page](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/reset). How can you update your code to make use of this method?

- When the form is submitted, update the counter at the top of the page to correctly show the number of contacts currently on the page.

There are a few ways to keep track of this count. How did you do so?

- Add four new inputs that are all radio buttons. Each one will represent either:

- Friend
- Family
- Co-worker
- Other

What attribute must you add so that clicking one radio button de-selects the others?

- Set one of the radio buttons to be checked by default. How did you do so?

- In your form's event listener, access the radio button elements list. How can you determine which one is checked?

- Update the event listener, the `generateContact()` function, and the related `contactTemplate()` function in whatever way you like so that the checked category appears in the contact's listing.

- Add an event listener to the remove button for each contact.
- Create a function that when the remove button is clicked, the contact is removed.

# Introduction to Forms

Many types of user interactions on the web are through forms. For example, you're working with forms whenever you search on YouTube, purchase a product from your favorite online store, or submit a post to your favorite social media site.

In this lesson, you'll learn the basics behind building forms with HTML and capturing the input.

## Learning Objectives

By the end of this lesson, you should be able to:

- Build forms with the form tag using generic inputs and a submit button.
- Write valid HTML by including necessary input attributes.
- Associate labels with inputs via the `for` tag or through nesting.
- Modify inputs by changing the `type` attribute.
- Create dropdowns, radio buttons, text areas, and checkboxes in forms.
- Require fields to be completed on submit with the `required` keyword.

---

## What are forms?

You've already encountered many forms if you've spent time on the web. Below are just some examples of where forms are used.

- Sign up for a service with your email and password.

- Paying for a product on an online store.

- Submitting an assignment to a learning management system.

In general, HTML forms will look something like the image below.

![Image of a basic form that looks to allow the user to enter a blog post.](./images/basic-blog-form.png)

Forms generally consist of multiple _fields_, such as "Title, " allowing for user interaction. Forms also typically have a _submit button_, such as the "Create Post" button above, which performs some action with the data inserted into the field.

You can create more creative interpretations of forms, however, for web accessibility, it is best to keep the forms in their standard format.

### The form element

To create a form, you must use the `form` element.

```html
<form></form>
```

All form fields and the submit button will go within the `form` element. It's possible to put other elements inside the `form` element, although elements such as paragraphs or headings will not affect the form submission.

### Text inputs

The most common field to put into a form is text input. The `input` element can be used for various purposes, but using it for text input is the most common.

```html
<form>
  <input type="text" />
</form>
```

This will create an input box with nothing inside or around it.

![Empty input field.](./images/empty-input.png)

In general, the `placeholder` attribute can be added to inputs to suggest to the user what should go inside the input.

```html
<form>
  <input type="text" placeholder="Enter a title..." />
</form>
```

This creates grey text that will be removed when the user starts typing.

![Empty input field with placeholder text.](./images/placeholder-input.png)

### Other inputs

Inputs with `text` are the most permissive, allowing users to type whatever they want.

However, utilizing other types can improve the user experience.

For example, using type `number` will pull up the number keyboard for mobile users and prevent users from entering non-numbers. You can also set `min`, `max`, and `step` attributes.

This input will only accept integers from 1-100. It won't allow for negative numbers or decimals

```html
<input type="number" min="1" max="100" step="1" />
```

A `password` type will immediately hide the characters typed and replace them with dots.

Other input types like `color`, `date`, `email`, and `tel` also have additional built-in features to make user input easier.

### Submit buttons

To have a complete form, you need some kind of submit button. The submit button can be used on many websites to trigger an action with your entered data.

There are two ways to create submit buttons. Both options below are valid.

```html
<!-- Using the `button` element. -->
<button type="submit">Create Post</button>

<!-- Using the `input` element. -->
<input type="submit" value="Create Post" />
```

Adding a submit button will look like the following.

![Simple form with submit button.](./images/submit-button.png)

> **Note:** The submit button appears next to the input field. Suppose you'd like it to appear on a new line, style the form with CSS. Alternatively, add a `br` element between the input and the submit button.

When you press the submit button on your page, you'll see the page refresh. This is the default behavior for forms. Do not worry too much about this behavior -- it will be covered later.

## Valid fields

While HTML is very permissive with what is allowed, it is best to follow appropriate conventions when writing your form fields.

Each `input` element should include:

- A `type` attribute defines what kind of input it is.
- A `name` attribute describes what the value means in the context of the form.
- An `id` attribute is unique across the entire page.

Many other attributes can be added to `input` elements, but these three are essential.

```html
<form>
  <input id="post-title" name="title" type="text" />
</form>
```

One of the few exceptions to this is `input` elements with a `type` of `submit` does not require an `id` or `name` attribute to function as expected.

## Labels

Labels are also essential to include in your forms.

- Labels help describe the form field with which the label is associated.

- They are meant to be visual cues for users to know what the input field is for.

- Labels can improve the accessibility of your website.

- Labels, when connected properly, can make it easier to click on your form fields.

To create a label, you use the `label` element. Any text can go within the `label` element.

```html
<form>
  <label>Blog post title</label>
  <input id="post-title" name="title" type="text" />
</form>
```

This will cause the added text to show up near the input.

![Form input with a label next to it.](./images/input-with-label.png)

However, this `label` is technically not associated with the `input` element. At the moment, it is just a floating label. One effect is clicking the label's text (i.e., "Blog post title") does nothing. If appropriately associated with the input field, clicking the label will move the cursor inside the field.

![Form with linked label.](./images/linked-label.png)

To link your label with a specific field, there are two options:

1. Add the `for` attribute to the `label` element, whose value is whatever the value is for the `id` of the associated element.

```html
<label for="post-title">Title</label>
<input id="post-title" name="title" type="text" />
```

1. Nest the input within the `label` element. The text can go anywhere within the `label` element.

```html
<label for="post-title">
  Title
  <input id="post-title" name="title" type="text" />
</label>
```

Both options will make it so that when you click on the label text, the relevant form field will be selected.

**Note**: Many coding examples and tutorials will omit labels and other best practices to demonstrate a particular concept quickly. While this is fine for learning, when you create an application meant for others to use, you should take the time to add all the elements needed to make a robust user experience.

## Alternative inputs

There are a variety of different types of input types that can be used to improve your form. Some of the most common completely change how the input field functions.

### Radio buttons

Radio buttons allow you to ask the user to choose one of many options.

![Example of radio buttons in a form.](./images/radio-buttons.png)

To create a radio button, you can change the `input` element's `type` to `radio`.

```html
<label>
  Public
  <input id="public" name="visibility" type="radio" value="public" />
</label>

<label>
  Private
  <input id="private" name="visibility" type="radio" value="private" />
</label>
```

Your input buttons must have the same value as the `name` attribute. This links the radio buttons, meaning selecting one option will de-select the other options. If you do not use the same `name` value, the radio buttons can both be chosen.

If you want one of the options to be selected by default, you can add the `checked` property.

```html
<label>
  Public
  <input id="public" name="visibility" type="radio" value="public" checked />
</label>
```

### Checkboxes

Checkboxes allow your user to select any number of options.

![Form with checkbox.](./images/checkbox.png)

To create a checkbox, you can change the `input` element's `type` to `checkbox`. Just like with radio buttons, checkboxes can be checked by default. If you use multiple checkboxes, you must also ensure they have the same name.

```html
<label>
  Pin post?
  <input id="pin-post" name="pin" type="checkbox" value="pin" checked />
</label>
```

## Dropdowns

Dropdowns are another common form element allowing you to pick from multiple options.

![Form with a dropdown.](./images/dropdown.png)

But, they do not use an `input` element. Instead, they use two elements: `select` and `option`.

```html
<label>
  Post category
  <select id="post-category" name="category">
    <option>-- Select a category --</option>
    <option value="personal">Personal</option>
    <option value="professional">Professional</option>
    <option value="promotion">Promotion</option>
  </select>
</label>
```

The `select` element is the wrapping element that defines the dropdown. It requires at least an `id` attribute and a `name` attribute.

Each `option` inside is one of the possibilities that can be selected from the dropdown. The options will appear in the order on the page. Options should include a `value` attribute, but it is common to have one `option` that lacks a `value` that has text like "Choose from the list below," or something similar.

## Input validation

Inputs can be validated so that they only allow certain types of text or stop a form's submission. Much can be said about form validation, as
it's a pretty complex topic. This lesson will only cover some of the most uncomplicated
validation. ### Email An email field can be used to ensure that a valid email
address is typed into your form. You can make an `input` element an email field
by setting the `type` to `email`.

```html
<label>
  Email
  <input id="email" name="email" type="email" />
</label>
```

If an invalid email is provided, an error message will show on the page when the form is submitted.

![Form with email validation error.](./images/email-error.png)

### Required

The `required` keyword can be added to the end of a form field to ensure that the field has some value before submission.

```html
<label>
  Title
  <input id="post-title" name="title" type="text" required />
</label>
```

If no input is provided, an error message will show on the page when the form is submitted.

![Form with requirement validation error.](./images/required-error.png)

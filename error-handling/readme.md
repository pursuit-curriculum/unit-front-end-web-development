# Error Handling

Errors can feel frustrating when they occur, but they are pretty helpful in the programming process. A good error can tell you precisely the problem and how to fix it. Developers will sometimes even include errors in their code as a way to signify something has gone wrong. This can be useful when others use their code.

In this lesson, you'll learn how to create your own errors. You'll also learn how to manage errors thrown in an application, either from code, you've written or when you use another person's code.

## Learning Objectives

By the end of this lesson, you should be able to:

- Throw errors with the throw keyword.
- Catch errors with a try/catch block.

---

## The purpose of errors

You have likely seen several unintentional errors occur in your programs, such as `ReferenceError`, `SyntaxError`, and `TypeError`. These errors occur when you've made a mistake in your code. The program running your code surfaces these errors so you know how and where your code fails.

However, you've also likely come across scenarios where you have returned an "error message" that is a string. For example, look at the following function, which returns an error message.

```js
function getProductDescription(product) {
  if (!product.name || !product.priceInCents) {
    return "Product requires a name and price.";
  }

  const priceInDollars = (product.priceInCents / 100).toFixed(2);
  return `${product.name} - $${priceInDollars}`;
}
```

In the function above, if the product object does not have a `name` or `priceInCents` property, a string is returned that explains the problem. Otherwise, a product description is provided.

This function may seem fine, but imagine trying to use it. How would you know an error has occurred? Look at the invocations below and consider how this function could be used.

```js
getProductDescription({ name: "Shirt", priceInCents: 2499 }); //> "Shirt - $24.99"
getProductDescription({ name: "Shirt" }); //> "Product requires a name and a price."
getProductDescription(); //> Uncaught TypeError: Cannot read property 'name' of undefined
```

You can't just check whether or not a string is returned; whether or not the inserted object has the right keys, a string will be returned. However, you also have a case where a `TypeError` would occur.

An ideal state for many functions is always returning \_the same data type or throwing an error. This way, you always have some idea as to what to expect.

## Creating your own errors

It's possible to write your own errors quite easily. The `throw` keyword expects some text to come after it, which will translate to an error.

```js
function getProductDescription(product) {
  if (!product.name || !product.priceInCents) {
    throw "Product requires a name and price.";
  }

  const priceInDollars = (product.priceInCents / 100).toFixed(2);
  return `${product.name} - $${priceInDollars}`;
}

getProductDescription({ name: "Shirt", priceInCents: 2499 }); //> "Shirt - $24.99"
getProductDescription({ name: "Shirt" }); //> Uncaught 'Product requires a name and price.'
getProductDescription(); //> Uncaught TypeError: Cannot read property 'name' of undefined
```

The `throw` keyword stops the execution of your code like any other error would. In the function above, the function now has two states:

1. It returns the product description as intended.
2. It throws an error.

While this improves the function, it does create more scenarios where an error may occur. You can use a `try/catch` block to handle this.

## Catching errors

If you expect a function to throw an error, you may use a `try/catch` block.

```js
const product = { name: "Shirt" };
let result = null;

try {
  result = getProductDescription(product);
} catch (error) {
  console.log("An error occurred!");
  console.log(error); //> Product requires a name and price.
}

console.log(result);
```

A `try/catch` block allows you to _try out some code_, and if no errors are thrown, the code will continue. If an error is thrown, _the error will be caught_, and some different code can be run. Then, your code will continue. A `try/catch` block is somewhat similar to an `if/else` statement: if the code works, run the code inside the `try` block; otherwise, run the code in the `catch` block.

For example, the code above will have the following output:

```
An error occurred!
Product requires a name and price.
null
```

Here is what is happening in the code above:

1. The `product` does not have a `priceInCents` key. An error will be thrown when the function is called inside the `try` block.
1. The error message is then moved to the `catch` block and stored in the variable `error`.
1. The first `console.log()` statement inside of the `catch` block runs, printing `"An error occurred!"`.
1. The second `console.log()` statement inside of the `catch` block runs, printing the error messages from the function: `"Product requires a name and price."`.
1. The code continues onwards and prints the result of `result`. Because the code inside the `try` block failed, the `result` is still `null`.

The `try/catch` block can protect your code from errors while making it clear that you expect something to fail at specific points in your code.

### Don't just catch it all

It would be best not to wrap all of your code in `try/catch` blocks.

Errors that occur because something's gone wrong with writing your code should be fixed. However, functions that may intentionally throw an error could be caught. Don't mistake using `try/catch` to fix what is wrong with your applications.

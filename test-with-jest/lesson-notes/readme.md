# Test with Jest

## Learning objectives

By the end of this lesson, you should be able to:

1. Distinguish between developer dependencies and production dependencies.

1. Write unit tests using the `jest` framework.

1. Identify best practices for writing unit tests.

1. Use the coverage tool to help identify how your tests can be improved.

## Starter code

Clone the following repository before this lesson begins. Follow the instructions within the repository.

- [Starter: Jest with Tests](https://github.com/pursuit-curriculum-resources/starter-test-with-jest)

> **Note:** You may use this starter code more than once. This means that you may already have a folder on your computer with the same name as the repository above.
>
> You can change the name of the folder a repository is cloned into by running the following command, where `<URL>` refers to the repository URL and `<DIRECTORY_NAME>` refers to the new name you wish to give the project.
>
> ```
> git clone <URL> <DIRECTORY_NAME>
> ```

---

## Guiding Questions

1. Take a look at the starter code. What is the purpose of each function?

   Write a comment above each function describing what you believe the purpose of the function is.

1. Run the following command on your command line. What does this command do?

   ```
   npm install jest --save-dev
   ```

1. What file or files did the above command change?

1. What is a developer dependency? Why should you install Jest as a developer dependency?

1. Update the `"scripts"` key in your `package.json` file so that `npm test` runs the `jest` command.

1. What happens when you run `npm test` now? Why?

1. Create a `__tests__/` directory in the root of your starter code repository. Do you think this will change the output of the `npm test` command? Why or why not?

   After you've made your guess, run the command and verify your guess.

1. Create a new test file in the `__tests__/` directory. This file will test the `src/products.js` file. What should you name your file and why?

1. Run `npm test` again. Has the output in your command line changed? Why or why not?

1. Export both functions from `src/products.js` and require them into your test file. Why is this step necessary?

1. You _do not_ need to import the `jest` package into your test file. Why not?

1. You are now ready to write your first test. You'll be writing unit tests for each of the functions in `src/products.js`. What is the purpose of unit tests?

1. First, you'll test the `getFullName()` function. Copy the code below into your test file. What is the purpose of this code?

   ```javascript
   describe("getFullName()", () => {
     // ...
   });
   ```

1. Replace the comment in the above `describe()` block with the code below. What is the purpose of this code?

   ```javascript
   test("", () => {
     // ...
   });
   ```

1. Try running `npm test` again. What happens? Why?

1. The `getFullName()` function expects a single argument that's an object. What is the required structure of this object for the function to work as intended?

1. Replace the comment in your existing test with the following code. What's the purpose of this code?

   ```javascript
   const input = { names: { first: "Chelsea", surname: "Hernandez" } };
   ```

1. Underneath that code, include the following code. What's the purpose of this code? Why is `actual` the name of the variable?

   ```javascript
   const actual = getFullName(input);
   ```

1. Underneath that code, define a new variable called `expected`. Set it equal to the value you _expect_ to be returned from the function invocation. What value do you expect and why?

1. Finally, you'll need to use Jest's test matchers to compare the two values. Include the following code at the end of your test and then run your tests with `npm test`. Do your tests pass? Why or why not?

   ```javascript
   expect(actual).toEqual(expected);
   ```

1. Change the `test()` function to the `it()` function and then run your tests once again. Is anything different?

1. The `it()` alias function can be used to make it easier to read tests. Right now, your test does not have an accompanying descriptive string. Update the string with a test description. If you read the entire line from left to right, it should read something like, "It should..."

   How did you choose to describe your test?

1. Run `npm test` once more. How did your test output change?

1. Before moving on to test the next function, run Jest's coverage tool. To do so, run the following command. What does the output of this command tell you about the `src/products.js` file?

   ```
   npm test -- --coverage
   ```

1. After running Jest's coverage tool, a new folder was added to your repository. What is contained inside this folder?

1. This folder should not be committed to GitHub as it will change every time the coverage tool is run. How do you force Git to ignore this folder? Make that change now.

1. The `coverage/` directory includes an `index.html` file which will show you more detailed information about the coverage report. Open up that file. What part of `src/products.js` is untested?

1. To complete coverage of this file, you'll need to write tests for the `getProductsPurchased()` function. The function expects a single argument, `contact`, to be passed into the function. What type of object does the function expect?

1. It is often good practice to first begin to test the "happy path." This refers to the main use case of the function. Begin by writing a `describe()` and `it()` block in your test file.

   What did you choose to put into the string of the `describe()` block and why? What did you choose to put into the string of the `it()` block and why?

1. What input would allow the test to pass as expected? Create that input and assign it to the variable `input` now.

1. What do you expect the end value to be after the function is called? Create that expected value and assign it to the variable `expected` now.

1. Complete the test by creating a variable named `actual` and assigning the invocation of the function to it. Then, use Jest's `expect()` function to compare values. After running `npm test`, did the test work as expected? Why or why not?

1. Run the coverage tool again and then return to the HTML version of the report. What code is still left untested?

1. Write a new `it()` block to test whether or not the `purchased` key contains an empty array. Follow the same steps as before to write your test. Then, run `npm test` and the coverage tool. Were the results as you expected? Why or why not?

1. Create and complete all remaining tests so that the coverage tool passes with 100% across all metrics. How did the coverage tool help you decide what tests to write?

1. Take a look at the functions and the tests you've written. Do these tests capture every possible situation for how the function could be used? Is it important to test every single scenario?

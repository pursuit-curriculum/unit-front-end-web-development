### Built-in modules: Readline

You can take user input as a prompt that can help an application feel more user-friendly.

## Learning Objectives

- Add and configure readline to a node project using Common JS Modlues (CJM)
- Learn the syntax for asking a single question.
- Use callbacks to write a series of questions.
- Use recursion to use readline in a loop.

#### Requiring the built-in module.

Add `readline` to your app:

```js
// index.js
const readline = require("readline");
const importedMessage = require("./message");
```

> **Note:** With built-in modules you only use the name of the module. You do not use the relative path.

#### Configuring the built-in module.

After importing `readline`, it must be configured. At first, it may be hard to understand what the configuration is doing. Often, using the code will help clarify the set up. Configuration is often a challenging step in a project.

Configure `readline` according to the documentation. This will allow the application to take user input via terminal. Documentation: [readline](https://nodejs.org/api/readline.html#readline) (Toggle to `CJS` view within the code snippets to match this reading's examples).

> **Note**: There is a newer syntax called `ESM` that the Node.js documentation shows as a default. It requires a little extra set up (files must have the extension `.mjs` instead of `.js`) and some older packages are more challenging to import. `CJS` (CommonJS) will be used in many companies for many years to come, as updating a large production application to a newer syntax is a large project and may not be a priority in contrast to other projects. When using the Node.js documentation for this course, make sure you toggle the examples to show `CJS`.

First, you must get two values out of `node:process`

- stdin, which is short for _standard input device_
- stout, which is short for _standard output device_

In this case, the terminal is the input and output device. Since input and output are easier to read and remember, the documentation uses object destructuring to get these values and rename them:

```js
// index.js
const { stdin: input, stdout: output } = require("node:process");
```

Next, create the interface and set it to a new variable `rl`:

```js
const rl = readline.createInterface({ input, output });
```

#### Using the built-in module

Finally, you will be able to use the readline interface within your application:

```js
rl.question("What is your name? \n", (answer) => {
  console.log(`${importedFunction()}, ${answer}!`);
  rl.close();
});
```

This will create the readline interface that will print the string that is the first argument in the question function. The app will then wait for the user to enter an answer. Once the answer has been entered, the rest of the code will execute. In this case it will log a message that includes the answer. Finally, the interface must be closed so that control of terminal is returned to you. If you forget to close it, you can use <kbd>Control</kbd>+<kbd>C</kbd> to close it.

For reference, here is the entire file:

```js
// index.js
const readline = require("readline");
const importedFunction = require("./message");

const { stdin: input, stdout: output } = require("node:process");
const rl = readline.createInterface({ input, output });

// console.log("Welcome to my app!");
// console.log(importedFunction());

rl.question("What is your name? \n", (answer) => {
  console.log(`${importedFunction()}, ${answer}!`);
  rl.close();
});
```

## Readline sequential questions

To ask a series of questions, put a new `rl.question()` inside the callback of the previous one:

```js
function getUserInput() {
  // First question
  rl.question("First question? \n", (a1) => {
    console.log(a1);
    // Close connection
    rl.close();
  });
}

getUserInput();
```

Move th `rl.close()` inside the final callback

```js
function getUserInput() {
  // First Question
  rl.question("First question \n", (a1) => {
    console.log(a1);

    // Second question
    rl.question("Second Question? \n", (a2) => {
      console.log(a2);
      // Close connection
      rl.close();
    });
  });
}
```

```js
function getUserInput() {
  // First Question
  rl.question("First question \n", (a1) => {
    // Second question
    rl.question("Second question? \n", (a2) => {
      // Third Question
      rl.question("Third question \n", (a3) => {
        // Do something with all the inputs
        console.log(
          "First answer: " +
            a1 +
            ", second answer: " +
            a2 +
            " third answer: " +
            a3 +
            "."
        );

        // Close connection
        rl.close();
      });
    });
  });
}
```

## Readline in a loop

One thing to do is you can rename the `console.log()` function so that it can be clear when you want to print something to the console for the user versus when you use the function for debugging.

You can create a game with readline. This is a very simple game.

```bash
touch cli.js
```

You can create a game with readline. This is a very simple game.

```bash
touch cli.js
```

You can now return to `index.js`.

This is the necessary configuration for readline:

```js
const readline = require("node:readline");

const { stdin: input, stdout: output } = require("node:process");

const rl = readline.createInterface({ input, output });

const { inform } = require("./cli.js");
```

Now create a menu function and call it immediately

```js
// to do swap informs to be from a function in another file to help explain organization
function menu() {
  console.log("menu!");
}

menu();
```

Once the function shell works as expected, use `rl.question` to set up a menu

```js
rl.question("Would you like to (w)in, (l)ose, or (e)xit ", (answer) => {
  console.log(answer);
});
```

You can make the interface more user-friendly by allowing users to type upper or lowercase letters or just type a single letter. Writing code to improve the user experience is often referred to as UX/UI (user experience or user interface)

```js
rl.question("Would you like to (w)in, (l)ose, or (e)xit ", (answer) => {
  answer = answer[0].toLowerCase();
  console.log(answer);
});
```

Now write some conditionals to deal with the responses:

```js
rl.question("Would you like to (w)in, (l)ose, or (e)xit ", (answer) => {
  answer = answer[0].toLowerCase();
  if (answer === "w") {
    inform("Congrats, you won!");
  } else if (answer === "l") {
    inform("Sorry, you lost!");
  } else if (answer === "e") {
    inform("Thanks for playing! Come back soon!");
  } else {
    inform("Sorry, there was an error! Please try again");
  }
});
```

Finally, create a loop to allow a user to play again and again until they type `e` for exit.

```js
// to do swap informs to be from a function in another file to help explain organization
function menu() {
  rl.question("Would you like to (w)in, (l)ose, or (e)xit ", (answer) => {
    answer = answer[0].toLowerCase();

    if (answer === "w") {
      inform("Congrats, you won!");
    } else if (answer === "l") {
      inform("Sorry, you lost!");
    } else if (answer === "e") {
      inform("Thanks for playing! Come back soon!");
    } else {
      inform("Sorry, there was an error! Please try again");
    }

    if (answer !== "e") {
      menu();
    } else {
      rl.close();
    }
  });
}

menu();
```

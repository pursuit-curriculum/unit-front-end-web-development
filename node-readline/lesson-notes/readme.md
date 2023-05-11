### Built-in modules: Readline

You can take user input as a prompt that can help an application feel more user-friendly.

## Learning Objectives

- Add and configure readline to a node project using Common JS Modlues (CJM)
- Learn the syntax for asking a single question.
- Use callbacks to write a series of questions.
- Use recursion to use readline in a loop.

## Guiding questions

Walk through this code and explain what each line does.

```js
// index.js
const readline = require("readline");

const { stdin: input, stdout: output } = require("node:process");
const rl = readline.createInterface({ input, output });

rl.question("What is your name? \n", (answer) => {
  console.log(`My name is ${answer}!`);
  rl.close();
});
```

- How can you add a second question like `what is your age`? that will happen after the `What is your name question`?

- How can you create a menu experience using readline?

- Create a guessing game where the computer selects a random integer from 1 - 10 and the user has 3 guesses.
- Allow the user to enter their name first and use their name in the following responses.
- If the user guesses correctly, congratulate them with a console log message and exit the game.
- If the user is unable to guess, correctly, let them know the number, then choose if they want to play again or exit.
- Allow the user to exit any time by typing the letter `q` for quit.

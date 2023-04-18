# NPM Packages and Code Libraries

INTRO INTRO INTRO INTRO

## Learning Objectives

- Ignore common folders and files with the `.gitignore` file.
- Install built-in packages through NPM and use those packages within a JavaScript project.
- Define scripts through the `package.json` file.
- Distinguish between developer dependencies and production dependencies.
- Install external packages through NPM and use those packages within a JavaScript project.
- Evaluate a longevity of a third-party package. Via popularity, downloads, most recent update.
- Read through documentation to identify how to use an external package.
  Nanoid, Chalk

## Creating an npm project

If you would like to code along, you may begin by creating a top level folder and setting up a `.gitignore` file.

- `mkdir my-npm-project`
- `cd my-npm-project`
- `touch .gitignore`

## Prevent git from tracking unnecessary files and folders

Eventually, you will be tracking your projects with git and uploading them to GitHub. It's a good idea to start with creating a `.gitignore` so you don't forget to do it later.

The `.gitignore` file provides a list of files for git to ignore within a project. When you work with `npm` and download packages, the code is already stored and maintained in their registry. You don't need to track or upload this code to GitHub. This code is stored in a folder called `node_modules/`.

`.DS_Store` is a Mac operating system (OS) file that helps manage your folders and files on your computer. For example, when you open files and folders using the Finder program, you may create `.DS_Store` files. It is only relevant to your computer and your files, so Git does not need to track them.

Whenever you create a .gitignore file, you will want to first add the following contents:

```
node_modules
.DS_Store
```

> **Note:** The `.gitignore` file is not a JavaScript file. You don't need to use quotes or semi-colons. Each file or folder to be ignored should be on a new line.

Now that folder setup is complete; you can initialize a new npm project by typing:

`npm init -y`

If you have successfully initialized a project, the `npm init` command will have created a `package.json` file.

## Application entry point

- `touch index.js`

Open this file and write a simple console log:

```js
console.log("Welcome to my app!");
```

To run this program, type:

- `node index.js`

## Modules

### Your modules

You can create your own modules. They can contain data or app functionality.

Let's create a new file called `message.js`:

- `touch message.js`

```js
// message.js
const whatTimeIsIt = () => {
  return `The date is ${new Date()}`;
};
```

You will need to export this function to be able to use it in another file. You will use a built-in object called `module.exports` to do this.

```js
// message.js
const whatTimeIsIt = () => {
  return `The date is {new Date()}`;
};
module.exports = whatTimeIsIt;
```

You will use the function `require()` to import this module. When requiring your file, you will use the _relative path_ to the file:

```js
// index.js
const importedFunction = require("./message");

console.log(importedFunction());
```

### Built-in modules

Node is built to be lightweight and by default, contains the minimum amount of functionality to run a basic application. There are some built-in node modules that you can add if you need them.

Some examples are:

- readline, Allows user input in the terminal.
- file system, Allows for creating and saving files.
- path, Allows for dynamic paths to be created that can work across multiple operating systems (Windows, Linux, macOS).

You can find a complete (and easy to read) list of Node.js built-in modules at the following website.

- [W3Schools: Node.js Built-in Modules](https://www.w3schools.com/nodejs/ref_modules.asp)

[Node.js](https://nodejs.org/dist/latest-v18.x/docs/api/) also has complete documentation, however it can be a bit dense to go through for beginners.

#### Requiring the built-in module

You may have noticed that terminal does not display very nested objects:

```js
// index.js

const veryNestedObject = {
  one: {
    two: {
      three: {
        four: {
          five: "You found the center!",
        },
      },
    },
  },
};
console.log(veryNestedObject);
// { one: { two: { three: [Object] } } }
```

But what if you wanted to see the full object? You can use the built-in `inspect` function from the `util` module.

Add [`util`](https://nodejs.org/api/util.html#utilinspectobject-options) to your app:

```js
// index.js
const { inspect } = require("node:util");

const veryNestedObject = {
  one: {
    two: {
      three: {
        four: {
          five: "You found the center!",
        },
      },
    },
  },
};

console.log(inspect(veryNestedOBject));
```

So far, the inspect function does nothing. Let's add some options. Options go inside an object. By default, `inspect` only goes to a depth of 2 in an object. Let's try 5.

```js
console.log(inspect(veryNestedObject, { depth: 5 }));
```

Let's also add some colors to the output:

```js
console.log(inspect(veryNestedObject, { depth: 5, colors: true }));
```

> **Note:** With built-in modules you only use the name of the module. You do not use the relative path. This is how Node.js distinguishes whether it is looking for a built-in module or your own file.

### Third-party modules

You can also import third-party code into our app.

To install some third-party code, you must know its name. A very simple package to try is [`lolcats`](https://www.npmjs.com/package/lolcats). This package will allow you to print a more colorful message in terminal.

Make sure you are on the same level as your `package.json` file for your installation to work:

- `npm install lolcats`

You can confirm that this worked by seeing that you have:

- A new folder `node_modules/`. Inside this folder is

  - the `lolcats` folder (The package you just installed.)
  - other folders required by lolcats. These additional packages are often referred to as _dependencies_.

  ![Node module folders with lolcats and its dependencies]({{site.url}}{{site.baseurl}}/assets/{{page.folder_name}}/node-modules-lolcats.png)

- A new file called `package-lock.json`.
  - The `package-lock.json` file contains more detailed information about the installed packages and their dependencies. It is automatically generated and updated, and you never need to edit it.
- `package.json` has a new field, `dependencies`

```json
{
  "name": "lesson",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "lolcats": "^2.0.1"
  }
}
```

When you want to import a third-party module, you will use the name of the module instead of including a relative path:

```js
// index.js
const lolcats = require("lolcats");
```

Update the `console.log()` statement to be the function `lolcats.print()`:

```js
rl.question("What is your name? \n", (answer) => {
  lolcats.print(`${importedFunction()}, ${answer}!`);
  rl.close();
});
```

## Installing Developer Dependencies

When building web applications, clients will interact with the core functionality. But there are also several helpful developer tools that the client never needs to use or see.

An example of this is unit testing. Developers need a way to test their code. However, clients never need to access this functionality.

When creating npm projects, you have the option to add third-party libraries as developer dependencies.

- `npm install jest --save-dev`

```json
{
  "name": "lesson",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "lolcats": "^2.0.1"
  },
  "devDependencies": {
    "jest": "^28.1.2"
  }
}
```

Our application requires the package `lolcats` to run and has `jest` as a developer dependency.

Let's set up Jest:

- `mkdir __tests__`
- `touch __tests__/index.test.js`

Let's write a test:

<!-- prettier-ignore-start -->
**\_\_test__/index.test.js**
<!-- prettier-ignore-end -->

```js
it("1 is equal to 1", () => {
  expect(1).toBe(1);
});
```

## Create a custom script

To run the jest test suite, you have to create a script to run it.

Change the property of the key `tests` that is within the `scripts` object:

**package.json**

```json
{
  "name": "lesson",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "jest"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "lolcats": "^2.0.1"
  },
  "devDependencies": {
    "jest": "^28.1.2"
  }
}
```

You can now run the jest test suite by typing:

- `npm test`

Or

- `npm run test`

> **Note:** npm has a number of aliases for common scripts such as `test` and `start`. When you use an alias you can omit the word `run` in your terminal command. If you create a script named something that is not an alias, you must include the word `run`.

[List of npm scripts](https://docs.npmjs.com/cli/v8/using-npm/scripts)

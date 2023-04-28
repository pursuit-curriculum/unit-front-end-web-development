# JSON and Persisting Data

Data has become an important commodity in the modern world. Data is collected about nearly everything. Businesses use data to keep track of inventory. Scientists use data to keep track of the weather. You have data for your photographs, your friends (being able to contact them, remember their birthdays), and more.

Before computers, most records were kept on paper and organized into files. But now, records are stored electronically.

You are likely most familiar with storing data as files and that is what we will work on in this lesson. However, keep in mind that this is not always the optimal way to maintain data, especially when the data set is very large. Later in the course you will learn about databases and how to use them to build applications.

## Lesson Objectives

By the end of this lesson

- Define CRUD and how it relates to coding operations.
- Create some data using Faker.js.
- Use built in `fs` module to read and write JSON.
- Use the methods `JSON.parse()` and `JSON.stringify()` to translate data from a file to a datatype that can be more easily manipulated by JavaScript.
- Read and create some data from and to a file.

## CRUD

Whatever application you are working on, you will be in some way, working with data.

There are five common things to do with data:

- Read a list (see a list of your wishlist items: just the names and price of the items)
- Read details of one item (See one of your wishlist item details: image, weight, shipping cost, whether it is in stock)
- Create a new wishlist item
- Delete a wishlist item
- Update a wishlist item

As you progress through the course and learn new technologies, you'll see this pattern emerging over and over again.

## Faker.js

So far, you've been working with fake or mock data.

Many developers continue to work with fake data. That's because before a new app or feature goes live (becomes available to the users), it's important to eliminate as many bugs as possible through testing. And, instead of trying to collect real data, developers usually generate some fake data to test various scenarios.

To make generating fake data easier, there is an npm package called [faker](https://fakerjs.dev).

You can code along with the following examples, or just read.

- Start a new npm project with `index.js` as the entry point and `products.js` for creating new products.
- `npm install @faker-js/faker@7 --save-dev`
- Set up a script for `npm start` so that it runs the `index.js` file.
- Require `faker` and create a function that creates a random product.

```js
// products.js
const { faker } = require("@faker-js/faker");

function createRandomProduct() {
  const product = {
    _id: faker.datatype.uuid(),
    name: `${faker.commerce.productAdjective()} ${faker.commerce.product()}`,
    description: faker.commerce.productDescription(),
    brand: faker.company.name(),
    price: faker.commerce.price(10, 200, 2, "$"),
    currency: "USD",
    inStock: faker.datatype.boolean(),
    attributes: {
      material: faker.commerce.productMaterial(),
      color: faker.vehicle.color(),
    },
  };
  return product;
}

console.log(createRandomProduct());
```

Create another function that takes an argument that is an integer and have it return an array of random products.

```js
function randomProductFactory(number) {
  const products = [];
  for (let i = 0; i < number; i++) {
    products.push(createRandomProduct());
  }
  return products;
}

console.log(randomProductFactory(5));
```

Create a `run()` function in `index.js` and accompanying `package.json` scripts that will allow a user to create one product and another that will allow user input to create a certain number of products.

- `npm run create`
- `npm run create 5`

```js
// index.js
const { randomProductFactory, createRandomProduct } = require("./products");

function run() {
  if (process.argv[3]) {
    console.log(randomProductFactory(process.argv[3]));
  } else {
    console.log(createRandomProduct());
  }
}

run();
```

```json
"start": "node index.js",
"create": "node index.js create"
```

## `fs` module

Now that you can reliably make product objects, you need a way to store the values. [`fs`](https://nodejs.org/api/fs.html) is short for file system and is a built-in Node module that will allow you to read and write from files.

Since you are adding new functionality, you have a design decision to make. You can just add the file writing functionality right into the `randomProductFactory()` function. It's a small app, you are probably not going to make this particular app much bigger. However, the concern of creating data is different from the concern of reading and writing a file. So do you add the file write functionality into `randomProductFactory()` or do you make it separate? Thinking about the pros and cons and being able to explain why you chose to code something a particular way is important to consider and be able to explain. For now, make it separate.

Make a new file called `helpers` and a new directory `data`.

The next design decision is do you want to have one filepath and one file name to store your data? In one way, it's simpler, you won't have to pass arguments or worry about the location. However, if you call the function from the top level (where index.js is) or from inside a new folder (e.g. if you made one called products), then you'd have to update the function. The same goes for whether you hard-code a file name. For now, add the path and file name as separate arguments.

```js
// helpers js
const fs = require("node:fs");
const { writeFileSync } = require("node:fs");

function writeJSONFile(path, fileName, data) {
  return writeFileSync(`${path}/${fileName}`, data, { encoding: "utf-8" });
}

module.exports = {
  writeJSONFile,
};
```

You'll note that there is an options object that takes a key value pair for encoding. This has to do with the kind of text file you are writing to. It is tangential to what we are learning about. However, [Here is a 10 minute video](https://www.youtube.com/watch?v=MijmeoH9LT4) introduction, if you are interested.

Update the run function:

```js
function run() {
  if (process.argv[3]) {
    console.log(randomProductFactory(process.argv[3]));
  } else {
    const newProduct = createRandomProduct();
    writeJSONFile("./data", "products.json", newProduct);
  }
}
```

You'll get an error because you are passing a JavaScript datatype. However, the method `fs.writeFileSync()` only accepts strings.

## `JSON.parse()` and `JSON.stringify()`

Remember, JSON like a JavaScript object and they are similar in many ways. One way they differ is that JSON designed to be one long string of data. This is in large part because when data is sent over the internet it is often sent as long strings and the conversion from string to object and object to string is very common.

There are two methods that JavaScript has to assist with the conversions. `JSON.parse()` and `JSON.stringify()`

```js
function writeJSONFile(path, fileName, data) {
  data = JSON.stringify(data);
  return writeFileSync(`${path}/${fileName}`, data, { encoding: "utf-8" });
}
```

What happens when you run the application again? Does it append to the file or does it replace the contents of the file?

Since it replaces the contents, you will need to write some functionality where you get the data first, and then append the new data to it and then write the new collection to the file.

Start by writing a function that reads the data

```js
// helpers.js
function readJSONFile(path, fileName) {
  return readFileSync(`./${path}/${fileName}`, "utf8");
}
```

Then call this function in the `run` function

```js
function run() {
  let products = readJSONFile("./data", "products.json");
  console.log(products);
  if (process.argv[3]) {
    console.log(randomProductFactory(process.argv[3]));
  } else {
    products = createRandomProduct();
    writeJSONFile("./data", "products.json", products);
  }
}
```

It's not quite working. The one object keeps getting replaced. Instead we should have an array of objects and every time we create a new object, we should push it into the array and then replace the entire file with the new array.

Delete the content in the `products.json` file.

```js
function run() {
  let products = readJSONFile("./data", "products.json");
  console.log(products);
  if (process.argv[3]) {
    console.log(randomProductFactory(process.argv[3]));
  } else {
    products.push(createRandomProduct());
    writeJSONFile("./data", "products.json", products);
  }
}
```

We get an error because the file is empty. We can write logic to create an empty array if the file is empty.

```js
// helpers.js
function readJSONFile(path, fileName) {
  const object = readFileSync(`./${path}/${fileName}`, "utf8");
  return object;
}
```

Now we were able to write one product, but the next one causes an error. If we log the `typeof` products in the run function, we will see that it is a string. The data coming from the file must be converted from a string to a JavaScript datatype.

Return to the `helpers` file and update the `readJSONFile()` function to convert the JSON string into an object:

```js
// helpers.js
function readJSONFile(path, fileName) {
  const object = readFileSync(`./${path}/${fileName}`, "utf8");
  return object ? JSON.parse(object) : [];
}
```

Finally, let's update the `run` function so that it can also add multiple products at a time.

```js
function run() {
  let products = readJSONFile("./data", "products.json");
  console.log(products);
  if (process.argv[3]) {
    products.push(...randomProductFactory(process.argv[3]));
  } else {
    products.push(createRandomProduct());
  }
  writeJSONFile("./data", "products.json", products);
}
```

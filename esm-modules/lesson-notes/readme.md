# ESM Modules

## Introduction

Let's build a small node application together. We will work on an imaginary business venture to sell ice cream.

The company has sent over some data on some possible ice creams, but it's a bit hard to read and analyze the data in its current format. We'll build a little app that imports the data and then write some functions to explore the data.

## Learning Objectives

By the end of this lesson, you should be able to:

- Create a new node project and set it up to use ESM modules rather than the current default CJS
- Import and export modules using the ESM syntax

## Getting started

- `mkdir icecream-flavors`.
- `cd icecream-flavors`.
- `touch index.js icecreams.js icecreams.json`.
- `echo "node_modules\n.DS_Store" >> .gitignore`.
- `npm init -y`, the flag `-y` will automatically set all default input for `package.json`.
- Update the `package.json` to be type module so that you can use `import` and `export` statements.

<details><summary>Copy and paste only the array into <code>icecreams.js</code>:</summary>

<code><pre>

```js
[
  {
    flavor: "Vanilla",
    color: "White",
    flavorType: "Sweet",
  },
  {
    flavor: "Chocolate",
    color: "Brown",
    flavorType: "Bittersweet",
  },
  {
    flavor: "Strawberry",
    color: "Pink",
    flavorType: "Fruity",
  },
  {
    flavor: "Mint Chocolate Chip",
    color: "Green",
    flavorType: "Sweet and Salty",
  },
  {
    flavor: "Coffee",
    color: "Dark Brown",
    flavorType: "Umami",
  },
  {
    flavor: "Raspberry Habanero",
    color: "Red",
    flavorType: "Spicy",
  },
  {
    flavor: "Salted Caramel",
    color: "Golden Brown",
    flavorType: "Sweet and Salty",
  },
  {
    flavor: "Blueberry Cheesecake",
    color: "Blue",
    flavorType: "Fruity",
  },
  {
    flavor: "Pistachio",
    color: "Light Green",
    flavorType: "Bittersweet",
  },
  {
    flavor: "Coconut",
    color: "Off-White",
    flavorType: "Sweet",
  },
  {
    flavor: "Lemon Sorbet",
    color: "Yellow",
    flavorType: "Fruity",
  },
  {
    flavor: "Spiced Pumpkin",
    color: "Orange",
    flavorType: "Spicy",
  },
];
```

</pre></code>

</details>

<details><summary>Copy and paste only the array into <code>icecreams.json</code>:</summary>

<code><pre>

```json
[
  {
    "flavor": "Vanilla Ice to Meet You",
    "color": "White",
    "flavorType": "Sweet"
  },
  {
    "flavor": "Choco-lot of Love",
    "color": "Brown",
    "flavorType": "Bittersweet"
  },
  {
    "flavor": "Strawberry Short Circuit",
    "color": "Pink",
    "flavorType": "Fruity"
  },
  {
    "flavor": "Mint Condition",
    "color": "Green",
    "flavorType": "Sweet and Salty"
  },
  {
    "flavor": "Espresso Yourself",
    "color": "Dark Brown",
    "flavorType": "Umami"
  },
  {
    "flavor": "Rasp-beary Spicy",
    "color": "Red",
    "flavorType": "Spicy"
  },
  {
    "flavor": "Salted Caramelicious",
    "color": "Golden Brown",
    "flavorType": "Sweet and Salty"
  },
  {
    "flavor": "Blueberry Thrill",
    "color": "Blue",
    "flavorType": "Fruity"
  },
  {
    "flavor": "Pistach-YO!",
    "color": "Light Green",
    "flavorType": "Bittersweet"
  },
  {
    "flavor": "Coco-nutty Fun",
    "color": "Off-White",
    "flavorType": "Sweet"
  },
  {
    "flavor": "Lemon Laughs",
    "color": "Yellow",
    "flavorType": "Fruity"
  },
  {
    "flavor": "Pumpkin Spice and Everything Nice",
    "color": "Orange",
    "flavorType": "Spicy"
  }
]
```

</pre></code>
</details>

## Import the data

In `index.js`:

- Import `icecreams.js` and set it to a variable `icecreams`.
- Import `icecreams.json` and set it to a variable `icecreamsJSON`.
- Log each one to confirm you've successfully imported each data set.

## Work with the data

### See a list of salty ice creams

There are 7 `flavorType`s:

- spicy
- salty
- fruity
- sweet
- sweet and salty
- bittersweet
- umami

Create a variable called `spicy` that will be an array of all the spicy icecreams from the `icecreams` array.

We can approach this by realizing we want to `filter` out all the ice creams that are not spicy. Therefore we can use the `filter` method:

```js
const spicy = icecreamsJSON.filter();
```

Then, we want to confirm that the icecreams(jb) `flavorType` is equal to `spicy`. This value will be added to a new array if it is true. If it is false, it will not be added to the new array.

```js
const spicy = icecreamsJSON.filter((jb) => {
  return jb.flavorType === "spicy";
});

console.log(spicy);
```

- [Filter method documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

### Write a function that allows you to see ice creams listed alphabetically by color

Create a function called `organizeByColor` that will take the arguments of an ice cream array and return the array with the objects organized by color.

```js
const organizeByColor = (treats) => {
  return treats;
};
```

> **Question:** Why is it important to NOT name the parameter the same as the data variable?

#### Review the sort method

`a` represents the first array object, and `b` represents the second object.

`.sort()` will iterate over the array and compare `a` to `b`.

Strings are compared by the first character only. The character values are based on their [character code values](https://www.w3schools.com/charsets/ref_utf_basic_latin.asp). For example, lowercase `a` is valued at 97, `b` is valued at 98, and `z`'s value is 122. Notice that capital letters have different codes. For example, the letter `A` has a value of 65.

There are three possibilities when comparing values. To sort the items in alphabetically ascending order, we will follow the following:

- `a` is smaller than `b`. Therefore it must move to the left. To move it to the left, we will return a value of `-1`.
- `a` is larger than `b`. Therefore it must move to the right. To move it to the right, we will return a value of `1`.
- `a` and `b` are the same. Therefore the order should not d. We will return a value of 0.

#### Complete the function

```js
const organizeByColor = (treats) => {
  return treats.sort((a, b) => {
    if (a.color < b.color) {
      return -1;
    } else if (a.color > b.color) {
      return 1;
    } else {
      return 0;
    }
  });
};
```

```js
console.log(organizeByColor(icecreamsJSON));
```

- [Sort method documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

## Write a custom script

Open the `package.json` file. Write a custom script that prints the name of your favorite mythical creature in the terminal.

```js
{
 "name": "make-fake-data",
 "type": "module",
 "version": "1.0.0",
 "description": "",
 "main": "index.js",
 "scripts": {
 "mythical": "echo 'My favorite mythical creature is a pegasus'"
 },
 "author": "",
 "license": "ISC"
}


```

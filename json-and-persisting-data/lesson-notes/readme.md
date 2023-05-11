# JSON and Persisting Data

## Lesson Objectives

By the end of this lesson

- Define CRUD and how it relates to coding operations.
- Create some data using Faker.js.
- Use the built-in `fs` module to read and write JSON.
- Use the methods `JSON.parse()` and `JSON.stringify()` to translate data from a file to a datatype that JavaScript can more easily manipulate.
- Read and create some data from and to a file.

## Guiding Questions

- What does CRUD stand for?
- What are the five common things to do with data?

- Create a new Node.js project for playlists.
- Add the package `faker` (version 7) as a dev dependency
- Why add faker as a dev dependency instead of a regular dependency?
- Why select a version when installing faker (or another package)?
- What is the purpose of the faker package?

- Create a start script that runs an `index.js` file.

- A playlist is made of songs. What fields should a song have?
- What faker data can you use to simulate fake song data?

- Write a function to create a single fake song.
- Where should you write this function?
- What should you name this function
- Can you explain why you put your function where you did and the thought behind the name?

- When it comes to coding, what are design decisions? What does it mean to defend your design?

- Why is it essential to think about your code in terms of design?

- Create another function to create multiple fake songs. Use user input to determine the number of songs to create.

- Create scripts that allow a user to run `npm run create` to create a single song and `npm run create 3` to create 3 songs.

- Create a folder to store data files.
- Add the `fs` module to your project. (Where?)
- What does `fs` stand for?
- What does `fs` allow you to do?
- What is the separation of concerns in terms of code?
- Is it important for a small application you are building now?
- What are the pros of putting your code into different files? What are the cons?
- What are the pros of combining the function to create songs and immediately write them to a file? What are the cons?

- What datatype does `fs` accept as data?
- When a file is read and stored in a JavaScript variable, what kind of datatype is it?
- How can you change a JSON string into an object?
- How can you change an object into JSON?

- Update your application so that every time new songs are made, they are added to a playlist collection (array of objects).
- Update your application so that every time new songs are made, they are saved to a `playlist.json` file

# Feasibility Testing

## Introduction

As a developer, you'll do hackathons and coding interviews that involve building a small project, participating in open-source projects, and working in teams to make features on the job.

Before jumping into any project, it's crucial to think about the limitations like time, which technologies you can use, and what you may have to learn before being able to work on or complete a project.

This lesson will review some essential project considerations and help you make strategic choices that will help you succeed.

## Learning Objectives

By the end of this lesson, you should be able to:

- As a developer, ensure you have the technologies and data to build an application's key feature.
- Identify how users will use your application and whether or not it is feasible.
- Identify what features need not be fully implemented to develop an MVP for a prototype.
- Plan milestones and time box things to keep the project moving forward

---

## App ideas and technology

We're going to walk through an app idea: It will be an app that will show where there are available parking spaces in real-time. Let's say you have one week to build a prototype (a demonstration that gives a good sense of how this app would work but doesn't have to have all the features complete).

Let's list the technologies needed (feel free to add your notes and comments):

- An app:

  - Mobile would be ideal, but creating a browser version that people could open on their phones would be ok for a prototype.
  - Build with JavaScript, HTML, and CSS
  - Great! You know these technologies.
  - Need map technology/geolocation

  - Is there an API with the data type and updates that fit the app's needs?
  - You might need to learn this if you have not previously worked with this kind of API. How much time can you give yourself?
  - Would it be enough time to learn and implement?
  - Is there a free tier or affordable resource for this prototype?

    - Database?

      - Use an external API for map data.
      - Would need to store data about parked cars/empty spaces. So yes.
      - Which database would make sense?
      - One, you know.
      - A different one that suits the needs of your app better?
      - Given the time constraints, do you have time to learn a second technology, or would it be better to go with what you know for your prototype?

    - Log-in?
      - A prototype might not need this.
      - In the long term, having users log in and log out might make sense.
    - UX/UI
      - How can a user (a vehicle driver) safely view the app?
      - This might be a big problem.
      - How can a user mark a space they just left?
      - How can a user mark a space they just took?
      - How can you ensure users mark spaces correctly and in a timely way?

- Limitations

  - Is there another technology that could be incorporated to automate the marking of spaces?
  - Can this app work with a few people using it? Or do you need most people to have this app running to contribute the data?

Can you create a demo based on your time to complete this project?

- Just let anyone drop or remove pins on a map for now.

## Is it feasible to build?

Now that you've run through the app's main challenges let's say you want to move forward with the app.

You have one week. How can you make the most of your time? As someone just starting, estimating the time needed to build things can be tricky. It can also be easy to feel overwhelmed and procrastinate.

Start by assuming how many hours a day you will work on the app. Realistically, most people can spend an average of 4-8 productive hours a day coding. Even if you spend over 12 hours a day in front of your computer "coding", realistically, not all 12+ hours are typically productive. Once in a while, you will have an epic 16-hour day where you get a lot done, and it's all productive, but for most people, that is an exception. It's normal to get tired, to feel distracted, or to have "off days". It's better to carve out time for self-care to get yourself back to being productive than forcing yourself to sit unproductively in front of the computer the entire day. Quality coding is more important than quantity coding.

Next, you will have the optimal amount of time to make something, but you must add some buffer time for bugs and other unexpected challenges.

Next, you likely came up with a bunch of cool ideas. Perhaps you are thinking about adding sounds, animations, a text messaging alert system, and badges that people could earn. But none of these are needed for the core functionality of the app. Keep a separate list of ideas you'd like to implement if you end up ahead of schedule.

Next, you will have to plan time to learn something. How much time can you spare? Is it enough time? If it is not enough time, can you pivot? It is essential to [timebox](https://en.wikipedia.org/wiki/Timeboxing) tasks. For example, it's better to set aside 2 hours to do CSS early on to make your app easier to develop and move on to other crucial tasks rather than spending three days making the app very attractive and only leaving yourself a day to build the core functionality. If you have time at the end, you can dedicate more time to CSS. Timeboxing will help you keep moving on to the essential goals.

Milestones are completing crucial tasks, like deploying a basic app, adding full CRUD to a resource, and functional log-in/authentication. If you meet your milestone, you can move on to another task. If you did not, you should adjust your schedule accordingly. You may have to cut bonus features to be sure you meet the core functionality.

Let's put a rough schedule with milestones together:

Day 1:

- App planning:

  - Trello
  - Wireframes
  - Feasibility testing
  - Reviewing project requirements and making sure you fully understand the prompt.
  - Asking clarifying questions
  - Planning your schedule for the week
  - Setting milestones
  - Checking in with your team (if you are working with others)
  - Set up a GitHub repository

- Day 2:

  - Learn how to use map/geolocation API
  - Don't need to put it into your app right away. You should build a little test app or follow a tutorial that leads you to a working demo
  - If you do not progress sufficiently, pivot to another app idea.

- Day 3:

  - Build a basic app and deploy it
  - Build out a static version of the features (placeholders and stubs)

- Day 4:

  - Integrate map/geolocation
  - Start building user interaction with the app

- Day 5:

  - Plan to finish building user interaction with the app

- Day 6:

  - Recheck project requirements, and address anything outstanding.
  - Polish
  - Squash bugs
  - Add error handling and improve UX/UI
  - Code freeze

- Day 7:
  - Review your work one final time, check the project requirements
  - Submit your work

It may be surprising that the app's core functionality is scheduled to be finished on day 5 and there is a code freeze initially planned for Day 6. There are several reasons for this:

    - This conservative schedule gives you some buffer time in case you run into bugs or other major road blocks.
    - Polishing an app is important. First impressions matter and an app with decent UX/UI will make a better impression, especially to non-technical people, so it is important to set aside time for it.
    - When you are tired and rushed, you are more likely to make big mistakes that can take a long time to unravel.
    - At some point, adding an extra hour of frenzied work won't significantly improve your app before the deadline.

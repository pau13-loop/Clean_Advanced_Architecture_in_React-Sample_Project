# Clean Advanced Architecture in React - Sample Project

As mentioned in the description of the GitHub repository this repository is to help people, and to help me, to remember how to keep a clean and good structure in your React Front End projects to be able to scale easly and mantain the project with consistency.

I hope you enjoy it, best regards!

## Table of Contents

- [Clean Advanced Architecture in React - Sample Project](#clean-advanced-architecture-in-react---sample-project)
  - [Table of Contents](#table-of-contents)
  - [Assets](#assets)
  - [Components](#components)
  - [Context](#context)
  - [Data](#data)
  - [Features](#features)
  - [Hooks](#hooks)
  - [Layouts](#layouts)
  - [Lib](#lib)
  - [Pages](#pages)
  - [Services](#services)
  - [Utils](#utils)
  - [Q\&A](#qa)
    - [Why I should have an *index.js* in my directorys to export my components, pages, layouts...?](#why-i-should-have-an-indexjs-in-my-directorys-to-export-my-components-pages-layouts)
    - [What to do if one of my directories grows too much?](#what-to-do-if-one-of-my-directories-grows-too-much)
    - [What is a Pure Function?](#what-is-a-pure-function)
  - [References](#references)
  - [License](#license)

## Assets

---

**[⬆ back to top](#table-of-contents)**

## Components

This is the directory with you store the components that are used all around your application. **DON'T STORE HERE the components that you use in a specific page.**
Each component should have the following files:

- ***Component-File.tsx:*** the component logic and rendering
- ***styles.scss:*** styles files, I reader use scss because of the reusability of styles and improvements done over classic plain css, but you can add a css files instead
- ***__test__;*** test directory where you test the correct behaviour of your component
- ***index.js:*** answered in Q&A section

---

**[⬆ back to top](#table-of-contents)**

## Context

In this directory you can sotre any context used in your React App and their own test cases. Any contest you'll create in the future should be stored here too.

---

**[⬆ back to top](#table-of-contents)**

## Data

The *data* folder is great to contain any json data file, for example if you have an store or you might have a mock file with predefined values.

At the same time your constants should be stored here but if the constants file grows too much I'll advice to create a constants directory inside the data directory and break the constants into groups of logic, for example one file can be called dates if you want to store constants about date formats, month names, days of the week, years...

---

**[⬆ back to top](#table-of-contents)**

## Features

This features folder is all about taking all of the code for a feature and putting it in one single place. So for example if you look into **features/authentication** you have all the handling signup, login, user data, all that kind of stuff it's all in this feature folder.

You'll notice in this **feature folder** we have another ser of folders like components, contexts, data, hooks, services. __Those folders are a replica structure of our source folder__, minus the features folder of course, so feature it has to be like a mini version of your source folder for each one of your different features. Remember that is not necessary implement all of the folders specified if is no content in them.

All the code of each feature is going to be contained and encapsulated, here is where our ***index.js*** comes to play. The idea, as explained in ***Q&A*** section, behind the ***index.js*** file is that we export all of the things we want to use from this feature and then we only ever import from this index.js file in our application. That means if we want to have a bunch of components in our to-do's but we only want to be able to export a couple of those components to be used we export them into index.js and you just make sure you never import from any other files or folders inside this features folder.

As I said before this is a great way of encapsulating all the logic for those features in one single location instead of having it all spread out throughout your entire application. This makes easier to change features currently implemented or add new features to the project.

By making this ***features*** folder everything outside the features is going to be used globally all around our entire application.

---

**[⬆ back to top](#table-of-contents)**

## Hooks

Add the custom hooksyou'll create  in this directory along the process of coding your applciation.

---

**[⬆ back to top](#table-of-contents)**

## Layouts

This directory is specifically for components that deal or set the layout of your app. Those components are user across a lot of pages or other components. This **layout folder is optional** if you don't have that many layouts just put them into your components folder and it's fine, but if you have a page with a lots of complex layouts using the layoutsfolder is really helpful.

---

**[⬆ back to top](#table-of-contents)**

## Lib

This **lib folder is very important** because in a lot of projects you're giong to build especially larger projects and you're going to pull in a lot of third-party libraries wheter you're using fetch which is built into the browser or you're using axios or any other third-party libraries you're going to want to implement into your code and generally you're going to put that in many places in your code but what if you need to update the version of one of those libraries, then you'll need it to udate it all over your code base.
The idea of this lib folder is essentially an implementation of the **facade pattern**, you have to take a library for example axios and you wrap the entire library with your own code that exposes the library in its own way so you essentially have a *facade* that you put over the top of this axios library and then you use that *facade* everywhere in your application. So now if you need to update axios you only have to do it in one single file in your application and everywhere else is just going to work so this makes working with large scale applications way easier because instead of changing in a million places you change it in one single location.

---

**[⬆ back to top](#table-of-contents)**

## Pages

We are goint to store the pages of our application, like this:

- Home 
- About
- Contact
- etc

One interesting thing to look at is we no longer have folders in our pages directory, it will be a lot more basic, straightforward and easy, we'll just have individual files for each of our pages. 

*But how do we go from that folder structure of pages to the file structure?*

The way we did that is by implementing **features** folder. In application development generally what you're going to do is you're going to add new feature to a website. Pages is just going to be taking our different features and implement them  where they belong and is going to be straightforward because all the logic it will be contain inside the features folder where they beolng.

---

**[⬆ back to top](#table-of-contents)**

## Services

Services folder is about integrating with an api, in other projects you might find this folder called *gateways*. For most of the applications you're going to have to integrate with an api so this folder is where you should allocate your services for calling your api.

---

**[⬆ back to top](#table-of-contents)**

## Utils

Into the *utils* folder we are going to store very small and simple functions and generally **pure functions** 

---

**[⬆ back to top](#table-of-contents)**

## Q&A

### Why I should have an *index.js* in my directorys to export my components, pages, layouts...?

**IMPORTANT**
- ***index.js***
  - *Simplified imports:* simplify the import statements in other parts of your application. Instead of importing the component directly with the full path (import Card from './components/Card';), you can use a shorter, more convenient syntax (import Card from './components';).
  - *Abstraction of Implementation Details:* The index.js file acts as an abstraction layer that hides the internal file structure of the components directory. It provides a clear and consistent entry point for other parts of your codebase. If you decide to reorganize your component files or change file names, you can do so without affecting the import statements elsewhere.
  - *Encapsulation of Implementations:* It encapsulates the implementation details of the Card component within its own directory. This helps in keeping the component's internal structure private, exposing only what's necessary for external use. It's a good practice for maintaining a clean and organized project structure.
  - *Preventing File Explosion:* As your project grows, you might have multiple files within the Card component directory (e.g., tests, styles, additional functionality). Using an index.js file allows you to keep the directory well-organized while still providing a straightforward way to import the component.
  - *Consistency Across the Project:* Adopting this pattern consistently across your project makes it easier for developers to understand and navigate the codebase. They can expect to find the main export of a component in its index.js file, creating a consistent pattern for component imports.

### What to do if one of my directories grows too much?

For example if you have too many contexts in context directory you could store each one into his own directoy with their test cases inside context directory. For example:

__Before__
- Context
  - __test__
    - AnalyticsContext.test.js 
    - AuthContext.test.js
    - UserContext.test.js
  - AnalyticsContext.js
  - AuthContext.js
  - UserContext.js
  And more...

  __After__
  - Context
    - AnalyticsContext
      - __test__
        - AnalyticsContext.test.js 
      - AnalyticsContext.js
    - AuthContext
      - __test__
        - AuthContext.test.js
      - AuthContext.js
    - UserContext
      - __test__
        - UserContext.test.js
      - UserContext.js
  And os on...

### What is a Pure Function?

A function that no matter what input you give it always gives you the same output for the same input and it doesn't have any weird side effects. So to clarify, it's just a really small function and very simple to understand.

---

**[⬆ back to top](#table-of-contents)**

## References

- https://www.youtube.com/@WebDevSimplified 

--- 

**[⬆ back to top](#table-of-contents)**

## License

MIT License

Copyright (c) 2020 AntoniPizarro and Pau Llinàs

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

**[⬆ back to top](#table-of-contents)**
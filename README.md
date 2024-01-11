# Clean Advanced Architecture in React - Sample Project

| ***__Reminder!__*** the files are empty, this is just an architecture template of how a clean advanced design should be structured in a front-end project.

As mentioned in the description of the GitHub repository, this repository is meant to help people, and me, remember how to keep a clean and good structure in your React front end projects, to be able to scale easily and maintain the project with consistency.

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
    - [Where is going to be stored most of our code?](#where-is-going-to-be-stored-most-of-our-code)
  - [References](#references)
  - [License](#license)

## Assets

Folder to store global assets like png, logos, etc

---

**[⬆ back to top](#table-of-contents)**

## Components

This is the directory where you store the components that are used throughout your application. **DON'T STORE HERE the components that you use in a specific page.**
Each component should have the following files:

- ***Component-File.tsx:*** the component logic and rendering
- ***styles.scss:*** styles files, I would  rather use scss because of the reusability of styles and improvements done over classic plain css, but you can add a css files instead
- ***__test__;*** test directory where you can test the correct behaviour of your component
- ***index.js:*** answered in the Q&A section

---

**[⬆ back to top](#table-of-contents)**

## Context

In this directory you can store all the contexts used in your React app and your own test cases. Any contests you create in the future should also be stored here.

---

**[⬆ back to top](#table-of-contents)**

## Data

The *data* folder is ideal for storing any JSON data file, such as for a store or a mock file with predefined values.

Similarly, your constants should be stored here, but if the constants file becomes too large, I would advise creating a constants directory within the data directory and breaking the constants into logical groups. For example, you could have a "dates" file to store constants related to date formats, month names, days of the week, and years.

---

**[⬆ back to top](#table-of-contents)**

## Features

This features folder is all about taking all of the code for a feature and putting it in one single place. So, for example, if you look into **features/authentication**, you have all the handling for signing up, logging in, user data – all that kind of stuff – it's all in this feature folder.

You'll notice in this **feature folder** we have another set of folders like components, contexts, data, hooks, and services. Those folders are a replica structure of our source folder, minus the features folder of course, so each one has to be like a mini version of your source folder for each one of your different features. Remember that it is not necessary to implement all of the folders specified if there is no content in them.

All the code of each feature is going to be contained and encapsulated, here is where our ***index.js*** comes into play. The idea, as explained in the ***Q&A*** section, behind the ***index.js*** file is that we export all of the things we want to use from this feature and then we only ever import from this index.js file in our application. That means if we want to have a bunch of components in our to-do's but we only want to be able to export a couple of those components to be used, we export them into index.js and you just make sure you never import from any other files or folders inside this features folder.

As I said before, this is a great way of encapsulating all the logic for those features in one single location instead of having it all spread out throughout your entire application. This makes it easier to change features currently implemented or add new features to the project.

By making this ***features*** folder, everything outside the features is going to be used globally all around our entire application.

---

**[⬆ back to top](#table-of-contents)**

## Hooks

Add the custom hooks you'll create in this directory along the process of coding your application.

---

**[⬆ back to top](#table-of-contents)**

## Layouts

This directory is specifically for components that deal with or set the layout of your app. Those components are used across a lot of pages or other components. This **layout folder is optional**. If you don't have that many layouts, just put them into your components folder and it's fine. But, if you have a page with lots of complex layouts, using the **layout** folder is really helpful.

---

**[⬆ back to top](#table-of-contents)**

## Lib

This **lib folder is very important** because in a lot of projects you're going to build especially larger projects and you're going to pull in a lot of third-party libraries whether you're using fetch which is built into the browser or you're using axios or any other third-party libraries you're going to want to implement into your code and generally, you're going to put that in many places in your code but what if you need to update the version of one of those libraries, then you'll need to update it all over your code base.
The idea of this "lib" folder is essentially an implementation of the **facade pattern**. You have to take a library, for example "axios", and wrap the entire library with your own code that exposes the library in its own way. So you essentially have a "facade" that you put over the top of this "axios" library and then you use that **facade** everywhere in your application. So now, if you need to update Axios, you only have to do it in one file in your application and everywhere else, it's just going to work. This makes working with large-scale applications way easier because instead of changing in a million places, you change it in one location.

---

**[⬆ back to top](#table-of-contents)**

## Pages

We are going to store the pages of our application like this:

- Home
- About 
- Contact 
- etc.

One interesting thing to look at is that we no longer have folders in our pages directory. It will be a lot more basic, straightforward, and easy. We'll just have individual files for each of our pages. 

But how do we go from that folder structure of pages to the file structure?

The way we did that is by implementing a **features** folder. In application development, generally what you're going to do is add new features to a website. Pages will simply take our different features and implement them where they belong. This will be straightforward because all the logic will be contained inside the features folder where they belong.

---

**[⬆ back to top](#table-of-contents)**

## Services

Services folder is about integrating with an API, in other projects you might find this folder called **gateways**. For most of the applications, you are going to have to integrate with an API so this folder is where you should allocate your services for calling your API.

---

**[⬆ back to top](#table-of-contents)**

## Utils

Into the *utils* folder, we are going to store very small and simple functions and generally **pure functions**.

---

**[⬆ back to top](#table-of-contents)**

## Q&A

### Why I should have an *index.js* in my directorys to export my components, pages, layouts...?

**IMPORTANT**

- ***index.js***

- *Simplified imports:* Simplify the import statements in other parts of your application. Instead of importing the component directly with the full path (import Card from './components/Card';), you can use a shorter, more convenient syntax (import Card from './components';).

- *Abstraction of Implementation Details:* The index.js file acts as an abstraction layer that conceals the internal file structure of the components directory. It provides a clear and consistent entry point for other parts of your codebase. If you decide to reorganise your component files or change file names, you can do so without affecting the import statements elsewhere.

- *Encapsulation of Implementations:* It encapsulates the implementation details of the Card component within its own directory. This helps to keep the component's internal structure private, and expose only what's necessary for external use. It's a good practice for maintaining a clean and organised project structure.

- *Preventing File Explosion:* As your project grows, you might have multiple files within the Card component directory (e.g. tests, styles, additional functionality). Using an index.js file allows you to keep the directory well-organised while still providing a straightforward way to import the component.

- *Consistency Across the Project:* Adopting this pattern consistently throughout your project makes it easier for developers to understand and navigate the codebase. They can expect to find the main export of a component in its index.js file, creating a consistent pattern for component imports.

### What to do if one of my directories grows too much?

For example, if you have too many contexts in the context directory, you could store each one in its own directory with its test cases inside the context directory. For example:

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

A function that, no matter what input you give it, always gives you the same output for the same input and does not have any strange side effects. So to clarify, it is just a really small and simple function to understand.

### Where is going to be stored most of our code?

The 99% of our code will be implemented in our ***features*** folder. Most of the time, we have to worry about global code. That's the hard thing with creating a good folder structure - a lot of the time, the code seems to be global and is just imported and exported from all over the place. But with a structure like this, we have kind of self-encapsulated features and they only import and export certain code. They don't communicate with each other which makes it really easy to keep them separate from one another.

---

**[⬆ back to top](#table-of-contents)**

## References

- https://www.youtube.com/@WebDevSimplified 
- https://lince-plus.com/

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
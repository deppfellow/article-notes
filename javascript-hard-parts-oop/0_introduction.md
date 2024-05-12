# Introduction

---

So if you stumble upon this notes series, I'll tell you briefly that this series of notes is cover how JavaScript doing its object-oriented style under the hood. Some of you may already know that in JavaScript, the object-oriented paradigm is, standardly, written using `class` keyword with `extends` and `super` to create *inheritance*. What you'll find here:

1.  How to create an object in JavaScript (e.g., object literal or `Object.create()`) and how it works under the hood.
2.  Prototypical nature of object in JavaScript. (spoiler, what `prototype` and `__proto__` does)
3.  Standard way to create object using object-oriented paradigm in JavaScript (e.g., factory function, `new` and `class` keyword)
4.  How sub-classing work in JavaScript (from manually setting up ourself to automation using `extends` and `super` keyword)

So, as a table of contents, here what contains in each notes:

-   Notes #1 explain how to create an object in the most basic way
-   Notes #2 explain how prototypical nature in JavaScript and how to create object using `new` keyword (spoiler, `new` keyword heavily utilize the prototypical nature of JavaScript)
-   Notes #3 bring us to the most standard way of today for creating object in JavaScript using `class` keyword
-   Notes #4 briefly explain us the default value of prototypical in JavaScript
-   Notes #5 to #7 explain to us how sub-classing works with each method of creating object in JavaScript, that is factory function, `new` keyword, and `class` keyword, respectively for each notes.



---

This notes is created from [The Hard Parts Series of Object Oriented Javascript](https://frontendmasters.com/courses/object-oriented-js/) by Will Sentance from Frontend Master. He is a great teacher, I must say. If you have access to Frontend Master, check his other courses, its worth it.






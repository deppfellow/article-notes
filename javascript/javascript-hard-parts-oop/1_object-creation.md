# Object Creation

---

Object-Oriented Javascript. In a project, we want to write a code that is maintainable and performant. Object Oriented Programming (in short, OOP) is a popular paradigm that enables us to do so. Its a design pattern that structure our complex code so that:

- Easy to add features and functionality
- Easy for developer to reason about
- Performant (i.e., efficient in memory)

And so that out data can be easily maintainable, we must bundled up our data. And now the question, how we may bundled up our data? ==**By storing it in an object**==



---

## Creating an Object

So to bundled up our data, we must create and store all of our data inside those object. One of, and the most easy way, to create an object is by using **object literal**:

```javascript
const user = {
  name: "Depp",
  score: 9,
  increment: function() { user.score++ }
};

user.increment()  // user.score => 10
```

This will do the job. But its getting repetitive and we violating our most basic principles in coding, DRY (Don't Repeat Yourself). So what is a way to do repetitive task like those? **we use function to wrap our code**.

```javascript
function userCreation(name, score) {
    const newUser = {};
    
    newUser.name = name;
    newUser.score = score;
    newUser.increment = function() { newUser.score++ };

    return newUser;  
};

const user_1 = userCreation("Depp", 9);
const user_2 = userCreation("Markovich", 5);
user_1.increment()
```

Now we can create any number of user without having to write down manually each object, perfect. But you see, folk, this approach is untenable. Here's the question, what make this approach untenable? ==**we create every single copy of the function (i.e., increment function above) on each user**==. Now you might think what wrong with that, you see that every single copy of the function with millions of user is means millions copies of those functions. Coupled that with our function may not only one but hundreds? ITS BURDENING OUR MEMORY!!



---

Next read go to `prototype-and-new.md`




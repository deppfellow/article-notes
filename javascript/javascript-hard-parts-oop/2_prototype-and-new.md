# Prototype and New Keyword

---

So, following our previous article, we must have a better way to create our object, right? Sure, ==we can store all of our *shared* function in a different object== and make all our object links, or refer, to those function's object.

```javascript
const functionStore = {
    increment: function() { this.score++ },
    login: function() { console.log("You're logged in!") }
};
```

And now all our user can refer to those `functionStore` object to get all the functionality we define, without having to make copies of the function.

But sure, how do we make these link that connect our object with the function's object?



---

## Property `__proto__`

So there is another way to create an object in JavaScript, by using `Object.create()`. This may seems long-winded to type `Object.create()` every time we want to create an object, but this technique right here return us a little bonus other than the object itself.

```javascript
function userCreation(name, score) {
    const newUser = Object.create(functionStore)  // link to our function's obj
    
    newUser.name = name;
    newUser.score = score;

    return newUser;  
};

const functionStore = {
    increment: function() { this.score++ },
    login: function() { console.log("You're logged in!") }
}

const user_1 = userCreation("Depp", 9);
const user_2 = userCreation("Markovich", 5);
user_1.increment()
```

Now one thing to note, whatever we pass in the `Object.create()`, it'll always return an empty object. The passed argument just make us able to link our created object with passed object. 

Now if we call `user_1.increment()`, JavaScript will search the function in the `user_1` itself but not found it, not panicking, then follow to search it in the passed function's object, that is `functionStore`, found it, then execute it.



---

## Property `__proto__`: Under the Hood

Now, it still seems abstract how the `Object.create()` can create links between our created object with another function's object. Behind the scene, `Object.create()` not only returning us an empty object, but also giving those empty object a hidden property named `__proto__`. This `__proto__` property referring to the value of passed argument in `Object.create()` such that every new created object will give us:

```javascript
const newUser = {
    name: ...
  	score: ...
    // __proto__: functionStore  // This property is hidden but still there
}
```



---

## Interlude: Function as Func-Obj Combo in JavaScript

Before we continue, there is one thing that I want to talk about. Function, in JavaScript, is not only "*functioning*" as function, but also an object, such that if we declare a new function, we also get an object attached to that function that we can use. I call it **function-object combo**

```javascript
function multiplyBy2(num) {
		return num * 2;
}    // + object {...}

multiplyBy2.stored = 5
multiplyBy2(3)  // return 6

multiplyBy2.stored  // return 5
multiplyBy2.prototype  // {}  <- this is one of our property in the multiplyBy2 object
```

That mean, whenever we create a function, we also get an object associated with those function. Now if we want to take the property of those object, we call it using dot notation. Whereas if we want to execute the function's code, we call it using parentheses.



---

## New Keyword

So creating a function that automate our object creation using `Object.create()` is very verbose, as we also need to refers it to the function's object. Luckily, there is `new` keyword that automate all of those verbose stuff.

```javascript
function UserCreation(name, score) {
  	this.name = name;
	  this.score = score;
};

UserCreation.prototype.increment = function() { this.score++ };
UserCreation.prototype.login = function() { console.log("You're logged in!") };

const user_1 = new UserCreation("Depp", 9);
user_1.increment();
```

Now remember that when we create a function (e.g. UserCreation function), JavaScript also creates for us the object of those function. So when we creating our new object `user_1`, under the hood, here's what happen:

1.  JavaScript create a local execution context from calling `UserCreation` function. Its store its argument to its parameters, at the same time, its also create a new *implicit* object called `this` inside those execution context.

    ```javascript
    this = {
      	name: "Depp",
      	score: 9,
    }
    ```

2.  Its automatically set a hidden property `__proto__` inside those `this` object. These hidden property linked to `prototype` property of `UserCreation` func-object combo.

    ```javascript
    this = {
      	name: "Depp",
      	score: 9,
    		// __proto__: UserCreation.prototype	// Hidden property
    };
    ```

3.  After all of that, its automatically return `this` object to us, and the calling process of `UserCreation` function end.



---

## Wrapping Up

So that it. Simply put, function act both as function and object. In those object, there is hidden property `prototype` that will store all of the functionality. By using `new` keyword to create object, we automate 3 things. First, creating the said object under the name `this`. Second, giving it hidden property `__proto__` that linked to `prototype` property where all functionality stored. Third, returning out those object to us.

For final check, why we going through all of this so that:

1.  We want our data and its functionality bundled together
2.  We don't want to copies our functionality on each bundled object
3.  We want it as short as possible, by automate all our job with `new` keyword



In ES6, JavaScript add another method to help us using `class` keyword. Head up next to ...




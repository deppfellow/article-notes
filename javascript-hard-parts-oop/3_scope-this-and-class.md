# Scope, `this`, and `class`

---

We already see from before that `new` keyword automate several things for us, and one of them is the creation of  `this` object. So what if we calling the function that create object without `new` keyword? there will be no `this` object being created and, as a result, the `this` code inside the function will refer to `this` object in global scope. In fact, when we call a function, JavaScript will automatically create `this` object in every local execution context.

Now look at this example:

```javascript
function userCreation(name, score) {
  	this.name = name;
	  this.score = score;
};

UserCreation.prototype.increment = function() {
  	function add1() { this.score++ };
  	add1();
};

// ...
// Bunch of another code
const user_1 = new UserCreation("Depp", 9);
user_1.increment()
```

Here is the question, what `this` in `add1()` function declaration refer to? you may answer `user_1`, but, in reality, its refer to `Window` object where global `this` refer to. You may asked "why", its because the **scope** of `this` keyword. It only cover the scope of the function its declared on, which is `increment`. When we enter new `add1` function, the scope is off.

Any way to fix this problem? yeah, sub-title below is the answer.



---

## Arrow Function and Lexical Scoping

In new ES2015, JavaScript introduce **arrow function** as a way to defining a function. To fix previous problem, we want to write our code as below:

```javascript
function userCreation(name, score) {
  	this.name = name;
	  this.score = score;
};

UserCreation.prototype.increment = function() {
  	const add1 = () => { this.score++ };
  	add1();
};

// ...
// Bunch of another code
const user_1 = new UserCreation("Depp", 9);
user_1.increment()
```

By defining a function with arrow, we create what we call lexical scoping, that is the variables the function is use is where the function is declared. Which from example above, the `this` object  `add1` function refer to is within the `increment` function.



---

## Class Keyword

So ES6 JavaScript introduce `class` keyword as another way to bundled object in JavaScript. Here the example code:

```javascript
class UserCreation {
  	constructor(name, score) {
      	this.name = name;
      	this.score = score;
    };
  
  	increment() {
      	this.score++;
    };	// Previously we need to write UserCreation.prototype.increment
  
  	login() {
      	console.log("You're logged in!")
    };	// Previously we need to write UserCreation.prototype.login
};

const user_1 = new UserCreation("Depp", 9);
user_1.increment();
```

Now you see we place all our functionality inside the `class`'s umbrella, making our code cleaner. But under the hood, everything is the same as explained in `2_prototype-and-new.md`. It just that JavaScript automate more things again even further.


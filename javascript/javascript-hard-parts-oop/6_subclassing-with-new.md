# call(), apply(), and Sub-classing with `new` keyword

---

For interlude, we will start this notes with understanding the `call()` and `apply()` built-in functionality store in `Object` object's `prototype`. Take a look at below example:

```javascript
const obj = { 
  	num: 3, 
  	increment: function() { this.num++; },
  	// __proto__: Object.prototype  // Hidden property
};

const otherObj = {
  	num: 10,
  	// __proto__: Object.prototype  // Hidden property
};

obj.increment();  // obj.num now 4

obj.increment.call(otherObj);  // otherObj.num now 11
// obj.increment.apply(otherObj);
```

So, we create two objects named `obj` and `otherObj`. After that, we run `obj.increment()` on `obj` object. Of course we can because `obj` has `increment()` function.

Now, we want to run `increment()` function on `otherObj` too, but it doesn't have `increment()` function. Can we run it? Of course we can, we run it from `obj`, find the `increment()` function in its own, then grab the `call()` function from `Object` using its `__proto__` link and pass the argument. Under the hood, `call()` function does is overwrite the `this` object creation, from `new`, by refer to the passed argument of `call()` instead of using the left-side of dot notation.

`apply()`, on the other hand, is the same as `call()`. But instead of passing it arguments one-by-one, we pass it as an arrays. Slight different.



---

## Sub-classing with `new` keyword

Now we'll back to the object creation method in notes#2, by using the `new` keyword, except now we'll apply the `new` keyword on the sub-class. We'll start with example:

```javascript
function UserCreation(name, score) {
  	this.name = name;
	  this.score = score;
};

UserCreation.prototype.increment = function() { this.score++ };
UserCreation.prototype.sayName = function() { console.log("I'm " + this.name) };

const user_1 = new UserCreation("Depp" , 9);
user_1.sayName()  // I'm Depp

/* -----
	We start our sub-classing below 
*/ 

function PaidUserCreation(paidName, paidScore, paidAccountBalance) {
		UserCreation.call(this, paidName, paidScore);
  	// UserCreation.apply(this, [paidName, paidScore]);
  	
  	this.accountBalance = paidAccountBalance;
};

// Remember to set the __proto__ link of PaidUserCreation to UserCreation.prototype
Object.setPrototypeOf(PaidUserCreation, UserCreation);

PaidUserCreation.prototype.increaseBalance = function(amount) {
  	this.accountBalance += amount;
};

const paidUser_1 = new PaidUserCreation("Markovich", 8, 50);
paidUser_1.increaseBalance(100);
paidUser_1.sayName()  // I'm Markovich
```

So those are wall of code. On the upper half is just like usual, we create our initial *factory function*. While the lower half is where we create our inherited *factory function* using `new` keyword. Let's break it down:

1.  We define out *factory function* `PaidUserCreation` accepting 3 arguments.

    -   We want to create our object by using `UserCreation` instead of re-write our code. But remember, using `new` keyword automatically make JavaScript create `this` object inside the local execution context with `__proto__` linked to `PaidUserCreation` func-obj combo. So now, inside execution context of `PaidUserCreation`, we have `this` object:

        ```javascript
        this = {
          	// __proto__: PaidUserCreation.prototype  // Hidden property
        }
        ```

    -   Now, we want the creation of `UserCreation` to assign the argument to our `this` object in `PaidUserCreation` above instead of `UserCreation`, so we using `call()` function and pass our current `this` object in `PaidUserCreation` as an argument along with other 2 arguments.

    -   Call process of `UserCreation` assigning our `paidUser` and `PaidScore` in the `this` object of `PaidUserCreation`. So now our `this` object looks like below:

        ```javascript
        this = {
          	name: "Markovich",
          	score: 8
          	// __proto__: PaidUserCreation.prototype  // Hidden property
        }
        ```

2.  We add additional property of `paidAccountBalance` assigned to `this` object. Now our final `this` looked like below:

    ```javascript
    this = {
      	name: "Markovich",
      	score: 8,
      	accountBalance: 50,
      	// __proto__: PaidUserCreation.prototype  // Hidden property
    }
    ```

3.  The `new` keyword automatically return the `this` object from `PaidUserCreation` to global context. Here assigned to `paidUser_1`.

4.  Don't forget that we want to also assigned the `__proto__` of our `PaidUserCreation` to the `prototype` of `UserCreation` to access its all functionality. Hence we use `Object.setPrototypeOf()` function.

5.  The rest is we create our functionality exclusive for `PaidUserCreation` and creating a new object.

And that its, folks, the process of creating sub-class using `new` keyword under the hood.  Next we will cover how its works with `class` keyword.


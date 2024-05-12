# Sub-classing

---

The core aspect in OOP. One of them generally known as name *inheritance*. Take a look at diagram below:

```
															 [ user ]   ---   name, score, increaseScore()
                              /        \
                             /          \
								 	 /--------/            \--------\
									/																 \
			[ moderator ]																[ paidUser ]
				|-sharePublic()															|-accountBalance
				|-<all property from user>									|-increaseBalance()
																										|-<all property from user>
```

We have a function to create user object which have `name` and `score` property, as well `increaseScore()` functionality. From there, we want to have another function that **can create object with additional property and functionality** (e.g., moderator or paidUser function). But we want those new object **have access to all property and functionality on the *upper function*** without having to rewrite our code, while at the same time, the object created from *upper function* **cannot have access to the lower function's property or functionality**.

Think that a `user_1` object created from `user`. Then another `paidUser_1` is created from `paidUser`. We want `paidUser_1` to have additional property called `accountBalance` and `increaseBalance()` while also have `name`, `score`, and `increaseScore()`.

While our `user_1` cannot access the `accountBalance` and `increaseBalance()`.



---

## Sub-classing with Factory Function

The previous method where we create our object using `Object.create()` is called ***factory function***. Lets have an example of sub-classing with those method:

```javascript
function userCreation(name, score) {
  	const newUser = Object.create(userFunction);
  	newUser.name = name;
	  newUser.score = score
  
  	return newUser;
};

const userFunction = {
  	increment: function() { this.score++ },
  	sayName: function() { console.log("I'm " + this.name) }
};

const user_1 = userCreation("Depp", 9);
user_1.sayName()  // "I'm Depp"

/* ---
	We start our sub-classing below 
*/ 

function paidUserCreation(paidName, paidScore, accountBalance) {
  	const newPaidUser = userCreation(paidName, paidScore);
  	Object.setPrototypeOf(newPaidUser, paidUserFunction);
  	
  	newPaidUser.accountBalance = accountBalance;
  	
  	return newPaidUser;
};

const paidUserFunction = {
  	increaseBalance: function(amount) { this.accountBalance += amount };
};
Object.setPrototypeOf(paidUserFunction, userFunction);

const paidUser_1 = paidUserCreation("Markovich", 8, 50);
paidUser.increaseBalance(100);
paidUser.sayName()  // "I'm Markovich"
```

We have understand the upper half of the code from previous notes. Lets focus on the lower half:

1.  We create a new factory function `paidUserCreation` that take additional property called `acountBalance`
    -   Constructing new object `newPaidUser` by calling `userCreation` function with arguments `paidName` and `paidScore`
    -   After that, we set the `__proto__` property that link `newPaidUser` object to the `paidUserFunction` object that we have define using built-in functionality from `Object.setPrototypeOf()`
    -   We add additional property to `newPaidUser` called `acountBalance`
    -   Returning the created object
2.  We want to create exclusive functionality for paidUser, so we create an object `paidUserFunction` that bundled all our paid user functions.
3.  Set the `__proto__` property of `paidUserFunction` to `userFunction` , so that when the `paidUser` object doesn't have the functionality in its link to `paidUserFunction`, it will lookup the functionality to `userFunction`.
4.  The rest, we construct our new Object and check its functionality.

You see, the work we have done is creating another factory function, set the `__proto__` link of the new object to its own functions object, but also, set the `__proto__` link of those own functions object to link to another *upper-functions* object. **Its a chain-link!!**.



---

And so with that, we can create another functions that accept additional property and functionality, while still have access to its *parent*'s function, without having to re-write our code. Next notes, we'll cover the sub-classing with `new` and `class` keyword.


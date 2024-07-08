# Sub-classing with `class` Keyword and the Use of `extends` & `super`

---

As we are know from `3_scope-this-and-class.md`, ES6 JavaScript introduce `class` keyword that automate many stuff in creating an object, under the hood. And for sub-classing, it also introduce `extends` and `super` keyword to make subclass in JavaScript. Lets use an example, again:

```javascript
class UserCreation {
  	constructor(name, score) {
      	this.name = name;
      	this.score = score;
    };
  
  	increment() {
      	this.score++;
    };
  
  	sayName() {
      	console.log("I'm " + this.name);
    };
};

const user_1 = new UserCreation("Depp", 9);

/* -----
	We start our sub-classing below 
*/ 

class PaidUserCreation extends UserCreation {
  	constructor(paidName, paidScore, paidAccountBalance) {
      	super(paidName, paidScore);
      	this.accountBalance = paidAccountBalance;
    };
  
  	increaseBalance(amount) {
      	this.accountBalance += amount;
    };
};

const paidUser_1 = new PaidUserCreation("Markovich", 8, 50);
paidUser_1.increaseBalance(100);
paidUser_1.sayName();  // It's Markovich
```

So, same as before, the upper half is the creation of `UserCreation` class using `class` keyword in ES6. Now, the creation of subclass in the lower half, its use `extends` and `super` keyword.

First, the `extends` keyword does is automate 2 things for us:

1.  Set the `__proto__` in `PaidUserCreation.prototype` object to links into what it follow after, in this case is `UserCreation.prototype`. Whereas in before, we manually set it using `Object.setPrototypeOf()`.
2.  Set the `__proto__` in the func-obj combo of `PaidUserCreation` to links into `UserCreation`.

This may looks abstract, but here what it looks like:

```javascript
// PaidUserCreation's object portion of func-obj combo
{
		prototype: {
				// < all shared functionality for PaidUserCreation >
				// __proto__: UserCreation.prototype  // hidden property
		},
		// __proto__: UserCreation,
		// // hidden property. Previously links to Function.prototype
}
```



---

From above we can see that (1) the func-obj combo has its own `__proto__` links to `UserCreation`, and (2) its `prototype` object's `__proto__` to links into `UserCreation.prototype`. That what `extends` automate for us.

With that in mind, now let's follow through the lower half of the example:

1.  It use `extends` to tell we want to refer to `UserCreation`

    -   Create object for `PaidUserCreation` using constructor that take 3 arguments.

    -   Using `super` keyword, it tells JavaScript to create the object using `new` keyword with whatever the `__proto__` in func-obj combo links to, which in this case is link into `UserCreation`, and return the object to `this` in current `PaidUserCreation`

        -   ```javascript
            // Creation of this object automated by super(), under the hood
            /*
            		Reflect.construct() tell us to make the object using <first arg> 
            		..with its input provided in <second arg>, 
            		..but link its __proto__ to <third arg>
            */
            this = Reflect.construct(UserCreation, [paidName, paidScore], PaidUserCreation.prototype)
            ```

        -   `Reflect.construct()` got its `first arg` from what `__proto__` in func-obj combo point to (i.e., in this case, `UserCreation`), with `second arg` from `super()` arguments, and the `third arg` from `prototype` of where its being called (i.e., in this case, `PaidUserCreation`)

    -   After creation of the object, the `super` keyword return our object to `this` object of current subclass, where we can add another property to it.

2.  We add our functionality for `PaidUserCreation` where `class` keyword will automatically store it in the `prototype` object of current subclass.

3.  The rest is as usual, constructing our object with `new` keyword and call our functionality.

Wow, that brutal! Look what `class`, `extends`, and `super` automate for us, all those complexity. But by using that, now we have the standard approach of declaring and bundling our data using JavaScript in object-oriented-like manner.
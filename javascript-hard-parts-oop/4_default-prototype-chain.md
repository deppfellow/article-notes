# Default Prototype Chain

---

So now we know that every function in JavaScript is a function-object combo, and in those object has `prototype` property which store all the shared functionality. But now, look at this code:

```javascript
const obj = {
  	num: 3
};

obj.num		// 3
obj.hasOwnProperty("num")		// Where does this functionality come from?
Object.prototype		// { hasOwnProperty: FUNCTION }
```

You see that `hasOwnProperty` function? where is it come from? The answer is that, every object (and function, and arrays too) also have `__proto__`, by default. And those `__proto__` is linked to `Object` object.

Remember in the first notes we can create object using `Object.create()`? Those are the `__proto__` in this object refer too. And now you can guess it, on those `Object` object, which also have its own `prototype` property, there is the `hasOwnProperty` function.



---

## Additional Functionality

In above I say that functions, objects, and arrays all have `__proto__` that linked to `Object`'s `prototype`. You may have come upon some function such `toString`, `call`, `bind`, etc in JavaScript. And you can guess it, all those functionality is stored in the `Object`'s `prototype`. Hence why all of our entities in JavaScript as additional functionality. Is that each entities has its own default `__proto__` link:

-   Object has link to `Object.prototype`
-   Function has link to `Function.prototype`


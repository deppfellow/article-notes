# React Hooks Simplified

---

This notes is taken for video from [Fireship's 10 React Hooks Explained](https://www.youtube.com/watch?v=TNhaISOUy6Q). I'll summarized the higher-concept idea of each hooks, which I feel is the main idea of using React in the first place.



---

## 1. useState()

*Things* (e.g., data, variables, etc) that changes in React is called `state`, and for any `state` that changes, React have to re-render the entire component to show the changes to the client.

Example, a text `counter: 0` and a button. When a user press the button, the text's number increments. In this case, the text's number is a `state` and when user click the button, React has to re-render its entire page to display the incremented text.

Example code:

```react
const [count, setCount] = useState(0)
```

`useState` take optional argument which is the initial state displayed in the UI for the first time. Next, Inside array, we provide two value:

1.  First value is the *reactive data* aka the state that often change. 
2.  The second value is a function that will do the logic. It will change how the state will changed. Example, `setCount(count + 1)` to increment the count.

In summary, `useState` used to manage a *state* within a component, make us able to store and update data, then update the UI to the client.



---

## 2. useEffect()

When a *state* change within a component, React will re-render its component. And when the re-render occur, we may want to add a side effect to the component, such as fetching data or changing the DOM. `useEffect` will executed every time re-render occur in those component.

Example, previous counter & button plus a title that appear when the counter reach 10 (i.e., the side effect). When a user press the button ten times, then a `<h1>` title showing user have reach counter of 10 will appear. To do that, we use `useEffect` to control the behaviour of component, to add side-effect of `<h1>` title when *state met 10*.

Example code:

```react
const [count, setCount] = useState(0)

useEffect(() => {
  if (count === 10) {
    // Add <h1> to the component
  } 
}, [count])
```

In the above code, when tell `useEffect` to execute the function when *state*  `count` is change. Inside the function, if the `count` equal 10, then we add the `<h1>` to the component.

A note, you see that we provide the second argument inside `useEffect`. Its called *dependency array*. In short, it tell `useEffect` to execute the function when the *state* provided inside dependency array is changed. 

1.  If we doesn't provide *dependency array*, `useEffect` will executed every time the component re-rendered.
2.  If we provide empty array, `useEffect` will executed only once, that is when the component rendered for the first time.



Another things to take note is "*teardown*" code. It means that when a component is unmount (e.g., removed from the DOM), a specified returned function will be triggered.

```react
const [count, setCount] = useState(0)

useEffect(() => {
  if (count === 10) {
    // Add <h1> to the component
  }
  
  return () => alert("Teardown occurs")
}, [count])
```

In above example, teardown is the function being returned from `useEffect`, and it returned every time the state specified in dependency array is change or when the component unmount. If we didn't specify the state in dependency array, the teardown will only occur when the component unmount.



---

## 3. useContext()

`useContext` is used to share the *state*'s value to the entire component tree, which mean its children component, and so on. Imagine a "*logged in*" button that need to change the text to "*logged out*" when a user already logged in. We can create an `App` component where inside those component, there is direct children `Button` component.

```react
// App's component
function App() {
  // Creating state, default to logged in
  const [loggedIn, setLoggedIn] = useState(true)
  
  return (
    // Use the created context with Provider, pass the value
  	<LogContext.Provider value={[loggedIn, setLoggedIn]}>
      <h1>{loggedIn ? "Logged In" : "Logged Out"}</h1>
      <Btn />
    </LogContext.Provider>
  );
};

export const LogContext = React.createContext();	// Create the context

// --------------------
// Btn's component
import { LogContext } from './App';	// Import the state created in App.jsx

export default function Btn() {
  // Consume the context's state from App.jsx
	const [loggedIn, setLoggedIn] = useContext(logContext)
  
  return (
  	<button onClick={ () => setLoggedIn(!loggedIn) }>
    	{loggedIn ? "Log out" : "Log in"}
    </button>
  );
};
```

That quite a lot of code, lets go through it:

1.  In `App.jsx` component, we create a `loggedIn` state that determine whether a user is Logged in or Logged out.
    -   There is a `<h1>` tag that will show current `loggedIn` value
    -   Inside `App.jsx` component, we have `Btn.jsx` component that need to change the text to "Logged Out" when current user is logged in.
    -   So we create the `LogContext` context to tell the `Btn.jsx` component, what our `loggedIn` state value currently. Then wrap all children component inside `Provider` context's tag.
2.  In `Btn.jsx` component, we export the button with correct text depending on `loggedIn` state.
    -   To know what value `loggedIn` state is, we consume the imported `LogContext` using `useContext`
    -   In the `<button>`, we can then define our button behavior depending on the `loggedIn` state.

In short, `useContext` is used to pass down the *state*'s value to its children component, so that the children component can use that *state*'s value to determine its behavior.



---

## 4. useRef()

It create a immutable object that will persist between render. Same like `useState`, we can use those object, and unlike `useState`, it will not trigger a re-render. Frequent usage of `useRef` is to (1) Reference a DOM element, (2) Keep track of re-render count, and (3) viewing previous state object.

### Referencing a DOM Element

Say that we have a button, and when user click on those button, we want to move the screen to those element.

```react
function App() {
	const refElement = useRef()	// Reference to the said element
  const scrollBehavior = () => {
    refElement.current.scrollIntoView({
      behavior: "smooth", block: "end", "inline": nearest
    })
  };	// Function to scroll into referenced element
  
  return (
  	<div className="App">
    	<p>lorem ipsum</p>
      
      /* --- another HTML content --- */
      /* --- another HTML content --- */
			/* --- another HTML content --- */
      
      <footer ref={refElement}> ... </footer>
    </div>
  );
}
```

In above example, we create a reference object and link the HTML element with `ref` tag. So now the `useRef` object has its `current` property set to those element. With `current` property, we can control what our desired behavior.



### Tracking Render Count

When we use `useState`, it'll re-render the component and we can't know how many time it has occur. But with `useRef`, we can know how many re-render occur since its an immutable object that persist between re-render.

```react
function App() {
  const [count, setCount] = useState(0)
  const renderCount = useRef(0)
  
  useEffect(() => {
    renderCount.current = renderCount.current + 1;
  });
  
  return (
  	<div className="App">
    	<button onClick={() => setCount(count + 1)}>Increment</button>
      <h1>{count}</h1>
    </div>
  );
};
```

In above example, we set the immutable `renderCount` object using `useRef` and set the initial value to `0`. Using `useEffect`, we want to create side-effect that incrementing the `renderCount` every time re-render occur.

Inside the `return` value, we create a `<button>` that will change the `count` state to make `useEffect` take effect. And if it pressed, previous explanation will happen.



### Viewing Previous State between Re-render

`useRef` can also used to store the previous *state*'s value so that persist between re-render.

```react
function App() {
  const [count, setCount] = useState(0)
  const prevCount = useRef(0)
  
  useEffect(() => {
    prevCount.current = count
  }, [count]);
  
  return (
  	<div className="App">
			<button onClick={() => setCount(count + 1)}>Increment</button>
      <h1>{count}</h1>
      
      <p>{prevCount.current}</p>
    </div>
  );
}
```

With similar example, now we use `useEffect` to store the previous value of `count` state inside object `current` property.



---

## 5. useReducer()

>   Dispatch Action to Reducer

`useReducer` is pretty similar to `useState`, but unlike `useState`, `useReducer` is used to manage more complex changes of *state*, especially when the next *state*'s value is depend on the previous value. Basic example of `useReducer` is increment/decrement button

```react
import { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return state + 1;
    case 'decrement':
      return state - 1;
    default:
      throw new Error('Not an action');
  };
};

function App() {
  const [count, dispatch] = useReducer(reducer, 0)
  
  return (
  	<div>
    	Count: {count}
      <button onClick={() => dispatch({type: 'decrement'})}>Decrement</button>
			<button onClick={() => dispatch({type: 'increment'})}>Increment</button>
    </div>
  );
}
```

From example above, lets break it down:

1.  Starting from `function App()`, we define our `useReducer` that returning two values, first one is the reactive *state* `count`, while the second is, instead of a function that set *state* like in `useState`, its a function that dispatch an action.
    -   `useReducer` take two arguments, the `reducer` function that handle the dispatched action, explained later, and an initial value, in this case is `0`
    -   In the `return` value, it use the `dispatch` function from `useReducer`. The function take an object with `type` property defining its action. The action can be anything, as long we define it in `reducer` function later.
2.  Next to the `function reducer()`, we create it with two arguments. First is the `state` that will be handled. Second is the `action` dispatched through `dispatch` function.
    -   Inside the function, using `switch` statement, we handle the next `state`'s value depend on the `action.type` passed as its arguments.



---

## 6. useMemo()

`useMemo` is a hooks that memoizes the result of a function so that it only re-execute the function when the *state* provided in dependencies array is changed. Here an example:

```react
import { useMemo } from 'react';

function App() {
  const [firstNum, setFirstNum] = useState(1);
  const [secondNum, setSecondNum] = useState(1)
  const [double, setDouble] = useState(1);
  
  const getDouble = slowFunction(secondNum)
  
  function slowFunction(num) {
    for (let i = 0; i > 1000000000; i++) {}
    return num * 2;
  }
  
  return (
  	<div>
    	<h1>{count}</h1>
      <button onClick={() => setFirstNum(firstNum + 1)}>Increment</button>
      
      <h1>{count}</h1>
      <button onClick={() => setSecondNum(secondNum + 1)}>Increment</button>
      
      <h1>{double}</h1>
      <button onClick={() => setDouble(getDouble)}>Double</button>
    </div>
  );  
};
```

Above example is three buttons, first to increment first number, second to increment second number, and the third is to take the second number and double it. In those component, we added an expensive for loop acts as a heavy computation.

What happen is, whenever a user click on a button whether is first, second, or third button, the entire component need to re-render, and so the heavy computation for loop. It will cause delay in user's screen. To overcome that, we use `useMemo`.

```react
// ...
  const getDouble = useMemo(() => {
    slowFunction(secondNum)
  }, [secondNum])
// ...
```

By changing the above part of code, we only execute the `slowFunction` when the *state* in the  dependencies array is changed, in this case when the second number `secondNum` is changed from pressing the second button. If user press the first or third button, the *state*'s value in `secondNum` is not changed so the `slowFunction` not executed, resulting in pressing first or third button doesn't causing delay in user's screen.



---

## 7. useCallback()

Similar to `useMemo`, `useCallback` hooks used to memoize, but the difference is `useCallback` returning the entire function, not just the return value like `useMemo` do.

```react
// App.jsx component
import { useState, useCallback } from 'react';

const todos = [
	{ id: 1, content: 'On the first day, grant Truth' },
	{ id: 2, content: 'On the second day, grant the Calendar' },
	{ id: 3, content: 'On the third day, grant Language' },
	{ id: 4, content: 'On the fourth day, grant Value' },
	{ id: 5, content: 'On the fifth day, grant Rules' },
	{ id: 6, content: 'On the sixth day, grant Meaning' },
	{ id: 7, content: 'On the seventh day, grant Dignity...' },
];

function App() {
	const [count, setCount] = useState(1);
  const [number, setNumber] = useState(100);

	const getTodos = () => {
		return todos[count - 1];
	};

	return (
		<>
			<h1>{count}</h1>
			<div className="card">
				<button onClick={() => setCount((count) => count + 1)}>
					count is {count}
				</button>
			</div>
			<Todos getTodos={getTodos} />
		</>
	);
}

// --------------------
// Todos.jsx component
import { useState, useEffect } from 'react';

export default function Todos({ getTodos }) {
	const [todos, setTodos] = useState([]);

	useEffect(() => {
		setTodos([...todos, getTodos()]);
	}, [getTodos]);

	return (
		<div>
			{todos.map((todo) => (
				<p key={todo?.id}>{todo?.content}</p>
			))}
		</div>
	);
}   
```

in `App.jsx`, we pass the `getTodos()` function as a props in children component `<Todos>`. So, when we have another state changed, `number` in this example, whole `App.jsx` will re-render and it'll trigger the `useEffect` in `Todos.jsx` component.

So, same as `useMemo` before, we need to memoize this function being passed in the `<Todos>` child component so that only when the *state*, linked with the function, change it'll trigger the function.

```react
// In App.jsx
// ...
const getTodos = useCallback(() => {
		return todos[count - 1];
	}, [count]);
// ...
```










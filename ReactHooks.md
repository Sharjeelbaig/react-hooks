<div style="padding:20px; background-color:#2d333b; border-radius:5px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);">
<h1 style="text-align:center"> <u>React Hooks</u> </h1>
React hooks are a feature introduced in React 16.8 that allow you to use state and other React features in functional components. They provide a way to manage stateful logic without writing a class component. Hooks are functions that let you "hook into" React features and add functionality to your components.
<hr />
</div>

## useState

The useState hook allows you to add state to your functional components. It takes an initial value as an argument and returns an array with two elements: the current state value and a function to update that value. You can use array destructuring to assign names to these elements.

```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

## useEffect

The useEffect hook allows you to perform side effects in your components. It takes a function as its first argument, which will be executed after the component renders. You can also provide a second argument, an array of dependencies, to control when the effect should run.

```jsx
import React, { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Perform some asynchronous data fetching
    fetchData()
      .then((result) => setData(result))
      .catch((error) => console.error(error));
  }, []); // Empty dependency array means the effect runs only once

  return <div>{data ? <p>Data: {data}</p> : <p>Loading...</p>}</div>;
}
```

## useContext

The useContext hook allows you to access the value of a context in your component. It takes a context object created using React.createContext and returns the current context value.

```jsx
import React, { useContext } from "react";

const MyContext = React.createContext();

function MyComponent() {
  const value = useContext(MyContext);

  return <p>Context value: {value}</p>;
}
```

## useRef

The useRef hook returns a mutable ref object that persists across re-renders of a component. It allows you to keep a reference to a DOM element or any other value that doesn't trigger a re-render when it changes.

```jsx
import React, { useRef } from "react";

function FocusableInput() {
  const inputRef = useRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

## useMemo

The useMemo hook allows you to memoize a value and compute it only when its dependencies change. It takes a function and an array of dependencies, and it returns the memoized value. The function is only re-executed if any of the dependencies change.

```jsx
import React, { useMemo } from "react";

function ExpensiveCalculation({ a, b }) {
  const result = useMemo(() => {
    // Perform some expensive calculation using a and b
    return a + b;
  }, [a, b]); // Only recompute if a or b changes

  return <p>Result: {result}</p>;
}
```

## useCallback

The useCallback hook is similar to useMemo, but it memoizes a function instead of a value. It returns a memoized version of the callback function that only changes if any of the dependencies change.

```jsx
import React, { useCallback } from "react";

function Button({ onClick }) {
  const handleClick = useCallback(() => {
    // Handle click event
    onClick();
  }, [onClick]); // Only recreate the callback if onClick changes

  return <button onClick={handleClick}>Click me</button>;
}
```

## Custom Hooks

In addition to the built-in hooks, you can create your own custom hooks. Custom hooks are functions that use the existing hooks to provide reusable logic. They can abstract away complex logic and make it easier to share stateful code between components.

```jsx
import { useState, useEffect } from "react";

function useTimer(initialValue) {
  const [timer, setTimer] = useState(initialValue);

  useEffect(() => {
    const interval = setInterval(() => {
      setTimer((prevTimer) => prevTimer + 1);
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  return timer;
}

function Timer() {
  const timer = useTimer(0);

  return <p>Timer: {timer}</p>;
}
```

These are some of the most commonly used React hooks. Each hook serves a different purpose and allows you to write more concise and reusable code in your functional components.

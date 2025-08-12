# React

## Core principles of React
- Virtual DOM
- Component-based. React uses reusable, self contained pieces of UI that manage their own state and behavior.
- Declarative. Instead of manipulating the DOM directly, you say what you want to happen based on the current state. React handles all the DOM stuff to match what you said. For example instead of writing imperative code to show/hide elements, you simply declare:
```javascript
{isVisible && <Component />}
```

## JSX
Javascript XML, which is basically HTML in javascript files. JSX gets converted into javascript function calls by Babel. For instance, <div>Hello, world!</div> is transformed into 
```javascript
React.createElement('div', null, 'Hello, world!').
```

### How do browsers read JSX?
Browsers cant read JSX. We use a transpiler (Babel) to convert JSX to JS.

## State
Internal data within a component that can change over time
- State updates trigger rerenders
- State updates are asynchronous. If the state update relies on previous state value, use the functional update form.

## Hooks
Functions that let you hook into core React features from function components
- Only call them at the top level. React relies on the hooks being called in the smae order every render to maintain state correctly.
- **useContext:** Subscribes to React context without nesting
    - Enables sharing values between components without prop drilling
    - Great for global state like themes or user data (state rarely change)
- **useReducer:** Alternative to useState for complex state logic
- **useRef:** Creates a muable reference that persists across renders
- **useMemo:** Memozies expensive calculations between renders
- **useCallback:** Returns a momized callback function
    - Prevents unnecessary renders in child components that rely on callback functions
- **useLayoutEffect:** Similar to useEffect but fires synchronously after DOM mutations and before the first paint.

## Hydration
When we have server side rendering and send back the HTML from the server to the client we still need to add the interactivity (JS) back to it. Hydration is the step where we connect Javascript logic back to the HTML.

## Virtual DOM
A lightweight copy of the DOM which makes DOM manipulations easier and more efficient.
React uses it for updating and rendering UI changes.

Whenever a re-render occurs due to state or props change, react will make a new virtual copy of the DOM and compare it to the previous. Since actual DOM manipulations are expensive React will only update the diff in the real DOM to save on resources.

This is called `reconciliation`, when we actually compare the virtual DOM with the previous virtual DOM and figure out the minimum changes needed to update the actual DOM.

## Data flow
In react data flows in one direction - from parent to children.

## Side effects
Side effects are when a change occurs outside the scope of the calling function.
Meaning that we are making changes somewhere else in the app. 

Calling an API, or doing I/O, console logging etc. is a side effect.

React wants rendering to be pure. React components are meant to behave like pure functions, meaning that:
- Same props + same state --> Same output (JSX)
- No changing data, no fetching, no subscriptions **while rendering**.

If you do side effects directly in the render function:
- They could run multiple times unexpectedly
- They might block rendering and make the UI feel slow
- They could cause infinite loops if they update state during render

That's why we use the useEffect hook.

You use the useEffect hook to handle side effecs in React.

- Runs after React updates the DOM - so it wont block rendering and your side effect will see the updated DOM/state
- Lets you tell React exactly when to run the effect
- Handles cleanup (important for avoiding memory leaks). We need to cleanup if the component unmounts (removed from the DOM) to prevent timers, event listeners from still running.

In React, a side effect is any interaction with the outside world or changes outside the component’s rendering — things React can’t handle purely by just rendering JSX.

We use useEffect for side effects because it lets React run them after rendering, in a controlled, efficient, and clean way — keeping the render phase pure and predictable.

## Keys in React
Used to uniquely identify virtual DOM elements. They are used to optimize rendering. They help React to identify which items have changed, are added, or are removed, enabling it to reuse already existing DOM elements, thus providing a performance boost.

## Controlled vs uncontrolled input
Controlled components rely on the React state to manage the form data while uncontrolled components use the DOM itself to handle the form data often with useRef.

## What are refs?
`Refs` are variables that allow you to persist data between renders, updating refs does not cause the component to re-render unlike state. Refs can also be used to store references to DOM elements.

## Optimization techniques
- useMemo is used for caching CPU-expensive functions.
- Lazy loading is a technique used to reduce the initial load time of a React app. It loads the components as the user navigates through the app.
- **Debouncing:** Only call a function after X units of time being idle.
- **Throttling:** Limit the number of times a function can be called in a given time frame.
build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## State and Lifecycle

---

# Lesson Objectives

- Discuss the concept of component state
- Discuss component lifecycle
- Introduce hooks
- Use the `state` hook
- Use the `effect` hook
- Discuss the rules of hooks
- Build a custom hook

---

# Objective

## Discuss the concept of component state

^ In React, the application is divided into the smallest possible pieces known as Components. Components can be presentational or container. When we talk about presentational components, they have no logic. They are embedded inside the components; it only has the UI.

^ Container components are the ones that use presentational components and have business logic in the component. Such components often have to keep local state objects to achieve one of the many use cases they might be responsible for.

---

# What is _state_?

^ Understanding the concept of states in React will allow you to build interesting, robust applications. Without states, your React components are glorified static templates. A state is a description of the status of a system that is waiting to execute a transition. A transition is a set of actions to be executed when a condition is fulfilled or changed.

^ State is how to interact with your components. State is a special React object that determines how your component renders and behaves. State is what allows us to create components that are dynamic and interactive.

---

[.background-color: #f4f4f4]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1650035948/interactive_app_design/state-h20_k77xg6.svg)

^ You can change the value on a thermometer, which means you have the ability to put a piece of matter into a different state. Put water in a freezer (below 32F) and its state will change from liquid to solid. Put it on a hot stovetop (above 212F), its state will change from liquid to gas. All of this can be done by changing one value: temperature.

^ We can do the same thing with programs. We can define a set of properties that determine how our program behaves in any situation, similar to water's relationship with temperature.

---

[.background-color: #ffffff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1650036040/interactive_app_design/687474703a2f2f6469676d2e64726578656c2e6564752f6372732f49444d3336342f63646e2f696d616765732f4765747479496d616765732d3633383032393634382e6a7067_cmnyah.jpg)

^ The concept of state in React derives from that of a state machine. Think about a turnstile, used to control access to subways and amusement park rides. It's a gate with rotating arms at waist height, one of which blocks the entryway. Initially the arms are locked, blocking entry, preventing you from passing through. Deposit a coin or token in a slot and the arms are unlocked, allowing a single person to push through. After you pass through, the arms are locked again until another coin is inserted.

^ A turnstile has two possible states: locked and unlocked. There are two possible inputs that affect its state: putting a coin in the slot and pushing the arm. In the locked state, pushing the arm has no effect no matter how many times you push; it stays in the locked state. Putting a coin in shifts the state from locked to unlocked. In this state, putting in another coin has no effect, however you can now push the arm, which shifts the state back to locked.

---

# Objective

## Discuss component lifecycle

^ State in React is mutable, which means the values can change. State is also self contained logic within each component. When state changes, only the corresponding parts of the view changes. Everything else in the DOM remains intact.

^ Each component has a specific lifecycle it follows in our application.You can use lifecycle events to modify the behavior of components (for example, decide when to rerender the view). This enhances performance because unnecessary operations are eliminated.

---

[.background-color: #ffffff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1650038391/interactive_app_design/component_lifecycle_gaeu1z.png)

^ React defines several component events in three categories. Mounting and unmounting events are invoked once, but updating events can be invoked many times.

^ mounting events: happen when a React element is attached to a DOM node

^ updating events: happen when a React element is updated as a result of new values of its properties or state

^ unmounting events: happen when a React element is detached from the DOM

---

# Objective

## Introduce hooks

---

```jsx
import React, { Component } from 'react'

export default class App extends Component {
  constructor(props){
    super(props)
    this.state = { status: 'Constructor method' }
  }

  componentDidMount() {
    setTimeout(() => {
      this.setState({status: "Component mounted"})
    }, 5000)
  }

  componentDidUpdate(prevState){
    if(prevState.status !== this.state.status){
      document.getElementById('statechange').innerHTML = "State changed"
    }
  }

  render() {
    return (
      <p>Status: {this.state.status}</p>
    )
  }
}
```

^ Before we discuss hooks, it's important to take a look at how things were done before hooks were introduced into React. Prior to hooks, components in React were built using classes. React still supports the class syntax, and you will see many examples and documentation using this format.

---

```jsx
import {useState, useEffect} from 'react'

const Example = () => {
  const [status, setStatus] = useState('');

  useEffect(() => {
    setStatus('Component mounted')
  }, [])

  useEffect(() => {
    console.log('status', status)
  }, [status])

  return (
    <p>Status: {status}</p>
  )
}
```

^ Hooks were added to React in version 16.8. They let us use state and other React features without writing a class. Hooks let us split one component into smaller functions based on what pieces are related. Let's look at some common hooks that are built into React.

^ A Hook is a special function that lets you “hook into” React features. For example, useState is a Hook that lets you add React state to function components. We’ll learn other Hooks later.

---

## Hooks and function components

```jsx
const Example = () => {
  // You can use Hooks here!
  return <div />
}
```

^ If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a Hook inside the existing function component.

---

# Objective

## Use the `state` hook

---

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

^ Before hooks, if we wanted to create a state variable for a component, it would look something like this.

^ The state starts as `{ count: 0 }`, and we increment `state.count` when the user clicks a button by calling `this.setState()`.

---

```jsx
import { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </>
  );
}
```

^ **What does calling useState do?** It declares a "state variable". Our variable is called count but we could call it anything else, like banana. This is a way to “preserve” some values between the function calls.

---

[.code-highlight: 5]

```jsx
import { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </>
  );
}
```

---

[.code-highlight: 10]

```jsx
import { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </>
  );
}
```

^ If we want to update the current `count`, we can call `setCount`.

---

## Declaring state variables

```jsx
const [count, setCount] = useState(0);

const [fruit, setFruit] = useState('banana');

const [user, setUser] = useState({
  name: 'Jane',
  email: 'jane@example.com'
});
```

---

# Objective

## Use the `effect` hook

^ The _Effect Hook_ lets us perform side effects in function components. We can use the effect hook to execute code when our component mounts, and after aspects of our component, including state, are updated.

---

## `useEffect`

```jsx
import { useEffect } from 'react';

const Example = () => {
  useEffect(() => {
    // Do something
  }, []);
}
```

^ 1. Import `useEffect` from 'react'

^ 2. Call the `useEffect` function before the returned JSX. This will be called after the component renders.

^ 3. Pass two arguments, a function and an array. This is called the dependencies array. This array should include all of the values that are side effect relies on. If the array is empty, the function will only execute when the component mounts, not when an update occurs. If you don't provide this array, the effect will run every render (a common mistake).

---

## `useEffect`

```jsx
import { useState, useEffect } from 'react';

const Example = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(count)
  }, [count]);
}
```

^ 1. Import `useEffect` from 'react'

^ 2. Call the `useEffect` function before the returned JSX. This will be called after the component renders.

^ 3. Pass two arguments, a function and an array. This is called the dependencies array. This array should include all of the values that are side effect relies on. If the array is empty, the function will only execute when the component mounts, not when an update occurs.

---

```jsx
import { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </>
  );
}
```

---

[.code-highlight: 1, 6-8]

```jsx
import { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </>
  );
}
```

---

## The cleanup function

```jsx
import { useState, useEffect } from 'react';

const Timer = () => {
  const [time, setTime] = useState(0);

  useEffect(() => {
    // count up 1 every second
    setInterval(() => setTime(1), 1000);
  }, []);
}
```

^ Sometimes our side effects need to be shut off. In this example, we have a countdown timer using the `setInterval` function, that interval will not stop unless we use the clearInterval function.

^ If we are setting state using setInterval and that side effect is not cleaned up, when our component unmounts and we're no longer using it, the state is destroyed with the component – but the setInterval function will keep running.

---

## The cleanup function

```jsx
import { useState, useEffect } from 'react';

const Timer = () => {
  const [time, setTime] = useState(0);

  useEffect(() => {
    let interval = setInterval(() => setTime(1), 1000);

    return () => {
      // setInterval cleared when component unmounts
      clearInterval(interval);
    }
  }, []);
}
```

---

[.code-highlight: 7-12]

## The cleanup function

```jsx
import { useState, useEffect } from 'react';

const Timer = () => {
  const [time, setTime] = useState(0);

  useEffect(() => {
    let interval = setInterval(() => setTime(1), 1000);

    return () => {
      // setInterval cleared when component unmounts
      clearInterval(interval);
    }
  }, []);
}
```

^ The cleanup function will be called when the component is unmounted. When a component is unmounted, our cleanup function runs, our interval is cleared, and we no longer get an error of attempting to update a state variable that doesn't exist.

^ Cleanup is not required in every cases. Use it when you need to stop a repeated side effect when your component unmounts.

---

## [Hooks API Reference](https://reactjs.org/docs/hooks-reference.html)

---

[.text: alignment(center)]

# Objective

## [Discuss the rules of hooks](https://reactjs.org/docs/hooks-rules.html)

---

# Objective

## Build a custom hook

---

## Resources

- [useHooks.com](https://usehooks.com)

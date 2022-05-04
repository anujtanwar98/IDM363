build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## Global State Management

---

# Lesson Objectives

- Introduce global state management
- Discuss the React Context API
- Discuss global state management libraries

---

# Objective

## Introduce Global State Management

^ We have previously discussed handling states within our components and the various events in a component's lifecycle. Managing the state of a component becomes more difficult as the size and complexity of our application increase. It's common for various components throughout our app architecture to depend on the state of other components. Passing state values up and down our app structure can get very tricky.

---

[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651598429/interactive_app_design/global_state_management_overview_w23krr.svg)

^ Global state management is a way to enable communication and sharing of data across all of the components in our application. It creates a concrete data structure to represent your app's state that you can read and write. State management is one of the most important aspects of every app.

^ The simplest technique for sharing state among components is to provide that state information via props to a component that is a parent to all the components that need to access that state data. If you remember from our previous lessons, this is known as "lifting state up".

^ Alternatively, a state management tool will make it much easy to maintain all of your app states, and make those state available to all of the components throughout your application.

---

# Objective

## Discuss the React Context API

^ React’s Context API simplifies the process of making data available to a large number of components, without having to manually pass that data through props at each level of your app’s component tree.

---

## How to use the context

- creating the context
- providing the context
- consuming the context

^ Using the context in React requires 3 simple steps: creating the context, providing the context, and consuming the context.

---

## Create the context

```javascript
import { createContext } from 'react';

const Context = createContext('Default Value');
```

^ The built-in factory function createContext(default) creates a context instance:

---

## Providing the context

```javascript
function Main() {
  const value = 'My Context Value';

  return (
    <Context.Provider value={value}>
      <MyComponent />
    </Context.Provider>
  );
}
```

^ `Context.Provider` component available on the context instance is used to provide the context to its child components, no matter how deep they are.

^ To set the value of context use the value prop available on the `<Context.Provider value={value} />`:

^ Again, what's important here is that all the components that'd like later to consume the context have to be wrapped inside the provider component. If you want to change the context value, simply update the `value` prop.

---

## Consuming the context

```javascript
import { useContext } from 'react';

function MyComponent() {
  const value = useContext(Context);

  return <span>{value}</span>;
}
```

^ Consuming the context can be performed in 2 ways.

^ The first way, is to use the `useContext(Context)` React hook. The hook returns the value of the context: `value = useContext(Context)`. The hook also makes sure to re-render the component when the context value changes.

---

## Consuming the context

```javascript
function MyComponent() {
  return (
    <Context.Consumer>
      {value => <span>{value}</span>}
    </Context.Consumer>
  );
}
```

^ The second way is by using a render function supplied as a child to `Context.Consumer` special component available on the context instance. Again, in case if the context value changes, <Context.Consumer> will re-render its render function.

---

[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651603611/interactive_app_design/react_context_flowchart_vs87ke.png)

^ You can have as many consumers as you want for a single context. If the context value changes (by changing the value prop of the provider `<Context.Provider value={value} />`), then all consumers are immediately notified and re-rendered.

---

## React Context Example

---

## React Context Resources

- [How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)
- [Application State Management with React](https://kentcdodds.com/blog/application-state-management-with-react)

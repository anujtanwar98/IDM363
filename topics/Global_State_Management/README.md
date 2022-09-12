build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

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

---

# Objective

## Discuss global state management libraries

^ There are a number of global state management libraries available that are fairly straight forward to implement into a React application. I'll provide some links in this file, but the library we're going to focus on is Redux.

---

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651759561/interactive_app_design/redux-logo_fabmux.png)

^ Redux is a pattern and library for managing and updating application state, using events call "actions". We'll use Redux to create a centralized "store" for our state that we can use across our entire application. There will be rules associated with the store that will ensure the state is always updated in a predictable fashion.

---

## When to use Redux

- Large amounts of state
- Frequent updates to state
- Update logic is complex
- Medium/large codebase
- Multiple developers

^ Redux helps you deal with shared state management, but like any tool, it has tradeoffs. There are more concepts to learn, and more code to write. It also adds some indirection to your code, and asks you to follow certain restrictions. It's a trade-off between short term and long term productivity. Not all apps need Redux.

^ You have large amounts of application state that are needed in many places in the app

^ The app state is updated frequently over time

^ The logic to update that state may be complex

^ The app has a medium or large-sized codebase, and might be worked on by many people

---

[.text: alignment(center)]

## [React Redux](https://react-redux.js.org)

^ Redux can integrate with any UI framework, and is most frequently used with React. React-Redux is the official package that lets your React components interact with a Redux store by reading pieces of state and dispatching actions to update the store.

---

## Redux Devtools

- [Firefox Redux Devtools](https://addons.mozilla.org/en-US/firefox/addon/reduxdevtools/)
- [Chrome Redux Devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)

---

## An analogy

^ Before getting involved in the details of implementation, let's talk through a real life scenario that can serve as a guide to learning Redux.

^ <https://levelup.gitconnected.com/an-unforgettable-way-to-learn-redux-f36afd38c966>

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651760618/interactive_app_design/1_rRbT3p4vI6FQOvwppdMuzA_srbsep.png)

^ Let's pretend you're going to the back to withdraw cash. Everyone should be familiar with this concept.

---

$$
intention / action = WITHDRAW\_MONEY
$$

^ While going to the bank there’s just one intention / action you’ve got in mind i.e to WITHDRAW_MONEY.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651760860/interactive_app_design/1_wgMTYZNauE-xrHlcPEiOnA_a0bnxn.png)

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651760907/interactive_app_design/1_yy1NfkM5n7E-97hyH2qYsA_b7mbpn.png)

^ When you get into the bank, you go straight to the cashier to make your request known, right?

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651760931/interactive_app_design/1_Ca5dfoZcpdfmVCAaxlkliw_ulqdr7.png)

^ Why didn't you just go into the bank vault to get your money?

^Well, like you already know, things don’t work that way. Yes, the bank has money in the vault, but you have to talk to the Cashier to help you follow a due process for withdrawing your own money.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651761016/interactive_app_design/1_9wklChnNZx8Cpt4Sa7vb7Q_eu3zcv.png)

^ The Cashier, from their computer, then enters some commands and delivers your cash to you.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651761087/interactive_app_design/1_y60iqwOOfQmzPcQhzU8WFA_lcqisi.png)

^ The BANK VAULT is to the bank what the REDUX STORE is to Redux.

^ Within your application, you don’t spend money. Instead, the STATE of your application is like the money you spend. The entire user interface of your application is a function of your state.

^ Just like the bank vault keeps your money safe in the bank, the state of your application is kept safe by something called a redux STORE. So, the STORE keeps your "money" i.e state, intact.

^ The Redux Store can be likened to the Bank Vault. It holds the state of your application — and keeps it safe.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651761187/interactive_app_design/1_aG_sU6CyVDRW9iy4SfuKRg_cdrksm.png)

^ In simple terms, with Redux, it is is advisable to store your application state in a single object managed by the Redux STORE. It’s like having ONE VAULT as opposed to littering money everywhere along the bank hall.

---

> Go to the bank with an ACTION in mind

^ If you’re going to get any money from the bank, you’re going to have to go in with some intent or action to withdraw money.

^ If you just walk into the bank and roam about, no one’s going to just give you money. You may even end up been thrown out by the security. Sad stuff.
The same may be said for Redux.

^ Write as much code as you want, but if you want to update the state of your Redux application (like you do with setState in React,) you need to let Redux know about that with an ACTION.

^ In the same way you follow a due process to withdraw your own money from the bank, Redux also accounts for a due process to change/update the state of your application.

---

```javascript
{
  type: "WITHDRAW_MONEY",
  amount: "$10,000"
}
```

^ If we chose to represent that process in a simple Redux application, your action to the bank may be represented by an object.

^ In the context of a Redux application, this object is called an action! It always has a type field that describes the action you want to perform. In this case, WITHDRAW_MONEY

^ Whenever you need to change/update the state of your Redux application, you need to dispatch an action.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651761746/interactive_app_design/1_niOOiE8U1EzTmDSNdCUwaQ_daysgk.png)

---

```javascript
import { createStore } from "redux"; //an import from the redux lib
import reducer from "./reducers"

const store = createStore(reducer);
```

^ Programmatically, here’s how a store is created.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651762956/interactive_app_design/1_9U0ntjx6hpWKc7deAFYsdQ_ph1ok4.png)

^ Back to our analogy. You had to see the cashier with an action in mind. The cashier communicates with teh vault that holds all of the money.

^ In Redux, we convey the ACTION to a REDUCER. This process is called DISPATCHING an ACTION.

^ The REDUCER knows what to do. In this example, It will take your action to WITHDRAW_MONEY and ensure you get your MONEY.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651763291/interactive_app_design/1_Xa5F3FkCXNVquJVGh13JWg_c5i5xz.png)

---

```javascript
export default (state, action) => {
  return state;
};
```

^ In very simple terms, a reducer is just a function that takes in state and action , and returns a new state

---

```javascript
// DON'T DO THIS
export default (state=[], action) => {
  state.push('new value');
  return state
};
```

^ You should not mutate the state received in your Reducer. Instead, you should always return a new copy of the state.

---

```javascript
// DO THIS
export default (state=[], action) => {
  return [...state, 'new value']
};
```

^ We are returning a new array. This array has all the values of the previous state array, and also appends the ‘new value.’ The spread operator helps make this easy.

---

```javascript
import { createSlice } from '@reduxjs/toolkit'

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})
```

^ Redux requires that we write all state updates immutably, by making copies of data and updating the copies. However, Redux Toolkit's `createSlice` and `createReducer` APIs allow us to write "mutating" update logic that becomes correct immutable updates.

---

## Installing Redux

```sh
# create a new app with Redux
npx create-react-app my-app --template redux

# add Redux to an existing app
npm install react-redux
```

^ if you use the Redux template option, the application will come with boilerplate code for a simple counter.

^ <https://react-redux.js.org/tutorials/quick-start>

---

```javascript
import store from './app/store'
import { Provider } from 'react-redux'

const root = ReactDOM.createRoot(document.getElementById('root'))

root.render(
  <Provider store={store}>
    <App />
  </Provider>
)
```

^ We're going to use a `<Provider>` to make our store available to our app, just like we did with React Context.

^ There are also a number of hooks available that allow our components to interact with the Redux store.

---

## Redux Example

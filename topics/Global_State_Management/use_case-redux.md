# Use case: Redux

## Cleanup

Let's remove all of the Context related code from our previous example.

```javascript
// App.jsx
import "./App.css";

import Form from "./components/Form";
import Header from "./components/Header";

function App() {
  return (
    <>
      <Header />
      <main>
        <Form />
      </main>
    </>
  );
}

export default App;
```

```javascript
// components/UserInfo.jsx

const UserInfo = () => {
  return (
    <span>username | email</span>
  )
}

export default UserInfo
```

```diff
// Header.jsx

+ import UserInfo from './UserInfo'

const Header = () => {
  return (
    <header>
-     <span>username | email</span>
+     <UserInfo />
    </header>
  );
};

export default Header;
```

```javascript
// Form.jsx

const Form = () => {
  function handleInputChange(e) {}

  return (
    <form>
      <div className="control">
        <input
          name="username"
          onChange={handleInputChange}
          placeholder="user_name"
          type="text"
        />
      </div>
      <div className="control">
        <input
          name="email"
          onChange={handleInputChange}
          placeholder="email"
          type="email"
        />
      </div>
    </form>
  );
};

export default Form;

```

## Installation

```sh
npm install react-redux
npm install @reduxjs/toolkit
```

```javascript
// src/store.js

import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: {},
})
```

```diff
// index.js

import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
+ import store from './app/store'
+ import { Provider } from 'react-redux'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
+   <Provider store={store}>
      <App />
+   </Provider>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

```sh
mkdir src/features
touch features/user.js
```

## Create a Redux State Slice

Add a new file named `src/features/user.js`. In that file, import the `createSlice` API from Redux Toolkit.

Creating a slice requires a string name to identify the slice, an initial state value, and one or more reducer functions to define how the state can be updated. Once a slice is created, we can export the generated Redux action creators and the reducer function for the whole slice.

Redux requires that we write all state updates immutably, by making copies of data and updating the copies. However, Redux Toolkit's `createSlice` and `createReducer` APIs use Immer inside to allow us to write "mutating" update logic that becomes correct immutable updates.

```javascript
// features/user.js

import { createSlice } from "@reduxjs/toolkit";

const initialStateValue = {
  username: "jane_smith",
  email: "jane@example.com",
};

export const userSlice = createSlice({
  name: "user",
  initialState: {
    value: initialStateValue,
  },
  reducers: {
    update: (state, action) => {
      state.value = action.payload;
    },
  },
});

export const { update } = userSlice.actions;

export default userSlice.reducer;
```

## Add Slice Reducers to the Store​

Next, we need to import the reducer function from the counter slice and add it to our store. By defining a field inside the reducers parameter, we tell the store to use this slice reducer function to handle all updates to that state.

```diff
// store.js

import { configureStore } from "@reduxjs/toolkit";
+ import userReducer from "./features/user";

export default configureStore({
  reducer: {
+   user: userReducer,
  },
});
```

## Use Redux State and Actions in React Components​

Now we can use the React Redux hooks to let React components interact with the Redux store. We can read data from the store with useSelector, and dispatch actions using useDispatch. Create a `src/components/UserInfo.js` file with a `<UserInfo>` component inside, then import that component into `App.js` and render it inside of `<App>`.

```diff
// src/components/UserInfo.js

+ import { useSelector } from "react-redux";

const UserInfo = () => {
+ const user = useSelector((state) => state.user.value);

  return (
-   <span>username | email</span>
+   <span>{user.username} | {user.email}</span>
  );
};

export default UserInfo;
```

```diff
// Form.js

+ import { useSelector } from "react-redux";

const Form = () => {
+ const user = useSelector((state) => state.user.value);

  function handleInputChange(e) {
+   console.log(e.target.name, e.target.value);
  }

  return (
    <form>
      <div className="control">
        <input
          name="username"
          onChange={handleInputChange}
          placeholder="user_name"
          type="text"
+         value={user.username}
        />
      </div>
      <div className="control">
        <input
          name="email"
          onChange={handleInputChange}
          placeholder="email"
          type="email"
+         value={user.email}
        />
      </div>
    </form>
  );
};

export default Form;
```

## Update store values

```diff
// Form.js

- import { useSelector } from "react-redux";
+ import { useDispatch, useSelector } from "react-redux";
+ import { update } from "../features/user";

const Form = () => {
  const user = useSelector((state) => state.user.value);
+ const dispatch = useDispatch();

  function handleInputChange(e) {
-   console.log(e.target.name, e.target.value);
+   const state = {
+     ...user,
+     [e.target.name]: e.target.value,
+   };
+   dispatch(update(state));
  }

  return (
    <form>
      <div className="control">
        <input
          name="username"
          onChange={handleInputChange}
          placeholder="user_name"
          type="text"
          value={user.username}
        />
      </div>
      <div className="control">
        <input
          name="email"
          onChange={handleInputChange}
          placeholder="email"
          type="email"
          value={user.email}
        />
      </div>
    </form>
  );
};

export default Form;
```

## References

- <https://github.com/machadop1407/react-redux-toolkit-tutorial>
- <https://www.youtube.com/watch?v=k68j9xlbHHk>

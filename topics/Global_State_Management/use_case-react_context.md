# Use case: React Context

## Read store values

```sh
npx create-react-app context_example
cd context_example
cd src
mv App.js App.jsx
mkdir components
```

```json
"importSort": {
  ".js, .jsx, .ts, .tsx": {
    "style": "module-compact"
  }
}
```

```diff
// App.jsx

- import logo from './logo.svg';
import './App.css';

function App() {
  return (
-   <div className="App">
-     <header className="App-header">
-       <img src={logo} className="App-logo" alt="logo" />
-       <p>
-         Edit <code>src/App.js</code> and save to reload.
-       </p>
-       <a
-         className="App-link"
-         href="https://reactjs.org"
-         target="_blank"
-         rel="noopener noreferrer"
-       >
-         Learn React
-       </a>
-     </header>
-   </div>
+   <>

+   </>
  );
}

export default App;
```

```javascript
// Header.jsx

const Header = () => (
  <header>
    <span>username | email</span>
  </header>
);

export default Header;
```

```diff
// App.jsx

import './App.css';
+ import Header from './Header';

function App() {
  return (
    <>
+     <Header />
    </>
  );
}

export default App;
```

```sh
npm start
```

```css
/* App.css */

header {
  align-items: center;
  border-bottom: 2px solid darkgray;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  padding: 2rem;
}
```

```javascript
// store.js

import { createContext } from "react";

export const state = {
  user: {
    username: "jane_smith",
    email: "jane@example.com",
  },
};

const StateContext = createContext(state);

export default StateContext;
```

```diff
// App.jsx

import "./App.css";
+ import StateContext, { state } from "store";
import Header from "./components/Header";

function App() {
  return (
-   <>
+   <StateContext.Provider value={state}>
      <Header />
-   </>
+   </StateContext.Provider>
  );
}

export default App;
```

```diff
// Header.jsx

+ import { useContext } from "react";
+ import StateContext from "../store";

- const Header = () => (
+ const Header = () => {
+   const state = useContext(StateContext);

+   return (
      <header>
-       <span>username | email</span>
+       <span>{state.user.username} | {state.user.email}</span>
      </header>
    )
+ };

export default Header;
```

```javascript
// Form.jsx

import { useContext } from "react";
import StateContext from "../store";

const Form = () => {
  const state = useContext(StateContext);

  function handleInputChange(e) {
    console.log(e.target.name, e.target.value);
  }

  return (
    <form>
      <div className="control">
        <input
          name="username"
          onChange={handleInputChange}
          placeholder="user_name"
          type="text"
          value={state.user.username}
        />
      </div>
      <div className="control">
        <input
          name="email"
          onChange={handleInputChange}
          placeholder="email"
          type="email"
          value={state.user.email}
        />
      </div>
    </form>
  );
};

export default Form;
```

```diff
// App.jsx

import "./App.css";

+ import Form from "./components/Form";
import Header from "./components/Header";
import StateContext, { state } from "./store";

function App() {
  return (
    <StateContext.Provider value={state}>
      <Header />
+     <main>
+       <Form />
+     </main>
    </StateContext.Provider>
  );
}

export default App;
```

```diff
// App.css

+ * {
+   box-sizing: border-box;
+ }
+
+ html {
+   font-size: 130%;
+ }

header {
  align-items: center;
  border-bottom: 2px solid darkgray;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  padding: 2rem;
}

+ form {
+   border: 2px solid darkgray;
+   margin: 2rem auto;
+   padding: 2rem;
+   width: 25rem;
+ }

+ .control {
+   margin-top: 2rem;
+ }

+ form .control:first-child {
+   margin-top: 0;
+ }

+ input[type="text"],
+ input[type="email"] {
+   border: 1px solid darkblue;
+   padding: 0.5rem;
+   width: 100%;
+ }
```

## Update store values

We're going to use the `useState` hook in our store to add the ability to update the state values.

```diff
// store.js

- import { createContext } from "react";
+ import { createContext, useState } from "react";

- export const state = {
-   user: {
-     username: "jane_smith",
-     email: "jane@example.com",
-   },
- };

- const StateContext = createContext(state);
```

We're going to move the provider out of the `App.jsx` file and into our store.

```javascript
export const StateContext = createContext({
  username: "",
  email: "",
  setUser: () => {},
});

export const StateContextProvider = ({ children }) => {
  const setUser = () => {
    // this will be how we update the user state
  };

  const initialState = {
    username: "jane_smith",
    email: "jane@example.com",
    setUser: setUser,
    // setUser
  };

  const [state, setState] = useState(initialState);

  return (
    <StateContext.Provider value={state}>{children}</StateContext.Provider>
  );
};

export default StateContext;
```

```diff
// App.jsx

import "./App.css";

import Form from "./components/Form";
import Header from "./components/Header";
- import StateContext, { state } from "./store";
+ import { StateContextProvider } from "./store";

function App() {
  return (
-   <StateContext.Provider value={state}>
+   <StateContextProvider>
      <Header />
      <main>
        <Form />
      </main>
-   </StateContext.Provider>
+   </StateContextProvider>
  );
}

export default App;
```

```diff
// Header.jsx

import { useContext } from "react";
- import StateContext from "../store";
+ import { StateContext } from "../store";

const Header = () => {
  const state = useContext(StateContext);

  return (
    <header>
      <span>
-       {state.user.username} | {state.user.email}
+       {state.username} | {state.email}
      </span>
    </header>
  );
};

export default Header;
```

```diff
// Form.jsx

import { useContext } from "react";
- import StateContext from "../store";
+ import { StateContext } from "../store";

const Form = () => {
  const state = useContext(StateContext)

  function handleInputChange(e) {
    console.log(e.target.name, e.target.value);
  }

  return (
    <form>
      <div className="control">
        <input
          name="username"
          onChange={handleInputChange}
          placeholder="user_name"
          type="text"
-         value={state.user.username}
+         value={state.username}
        />
      </div>
      <div className="control">
        <input
          name="email"
          onChange={handleInputChange}
          placeholder="email"
          type="email"
-         value={state.user.email}
+         value={state.email}
        />
      </div>
    </form>
  );
};

export default Form;
```

```diff
// store.js

export const StateContextProvider = ({ children }) => {
- const setUser = () => {
- // this will be how we update the user state
+ const setUser = (data) => {
+   console.log("data", data);
};

const initialState = {
  username: "jane_smith",
  email: "jane@example.com",
  setUser: setUser,
  // setUser
};
```

We're going to call our `setUser` function from our store, and pass a copy of the current state values in.

```diff
// Form.jsx

function handleInputChange(e) {
+ state.setUser({
+   ...state
+ });
}
```

We also need to send in which values have changed based on user input.

```diff
function handleInputChange(e) {
  state.setUser({
    ...state,
+   [e.target.name]: e.target.value,
  });
}
```

Now we update the store function to call `setState` with our new data.

```diff
// store.js

const setUser = (data) => {
  // console.log("data", data);
+ setState({
+   ...state,
+   ...data,
+ });
};
```

## References

- <https://reactjs.org/docs/hooks-reference.html#usecontext>
- <https://stackoverflow.com/questions/41030361/how-to-update-react-context-from-inside-a-child-component>

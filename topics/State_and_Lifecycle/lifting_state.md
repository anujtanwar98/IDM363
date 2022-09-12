# Lifting State

```sh
npx create-react-app my-app
cd my-app/src
rm App.css App.test.js index.css logo.svg reportWebVitals.js setupTests.js
```

```diff
// index.js

import React from 'react';
import ReactDOM from 'react-dom/client';
- import './index.css';
import App from './App';
- import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

- // If you want to start measuring performance in your app, pass a function
- // to log results (for example: reportWebVitals(console.log))
- // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
- reportWebVitals();

// App.js

- import logo from './logo.svg';
- import './App.css';

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
  );
}

export default App;
```

## Setup App to use two components

```javascript
// App.js

import { useState } from 'react';
import ChangeLocation from './components/ChangeLocation';
import ShowLocation from './components/ShowLocation';

function App() {
  const [location, setLocation] = useState('');

  return (
    <>
      <ShowLocation location={location} />
      <ChangeLocation location={location} setLocation={setLocation} />
    </>
  );
}

export default App;
```

## `ShowLocation` component

Nothing crazy here. We pass down the location state variable value and display it in this component.

```javascript
import PropTypes from 'prop-types';

const ShowLocation = ({ location }) => <p>Your location is {location}</p>;

ShowLocation.propTypes = {
  location: PropTypes.string,
};

export default ShowLocation;
```

## `SetLocation` component

Obviously this could all be done in the `App.js` file, but for the purposes of this exercise, we're going to change the state variable in this child component.

```javascript
import PropTypes from 'prop-types';

const ChangeLocation = ({ location, setLocation }) => (
  <>
    <input value={location} onChange={(e) => setLocation(e.target.value)} />
  </>
);

ChangeLocation.propTypes = {
  location: PropTypes.string,
  setLocation: PropTypes.func,
};

export default ChangeLocation;
```

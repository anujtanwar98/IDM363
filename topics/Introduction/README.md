build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Introduction

---

[.build-lists: false]

![left](https://res.cloudinary.com/pjs-uxid/image/upload/v1648152629/web_authoring_one/avatar-pjs_gafnzu.jpg)

## About Me

- Name: Phil Sinatra
- Email: ps42@drexel.edu
- GitHub: [@philsinatra](https://github.com/philsinatra)

## About This Course

- [Drexel Learn](https://learn.dcollege.net/webapps/login/)
- [Course Repository](https://github.com/Drexel-University-UXID/IDM363)

^ All course information including syllabus, overview and assignments will be managed through Drexel's Blackboard (BBLearn) system. Let's log in and review the syllabus and course information now.

---

# Lesson Objectives

- Discuss React and its advantages
- Discuss tooling and editor setup
- Discuss modern Javascript syntax
- Create a React application
- Introduce JSX

---

# Objective

## Discuss React and its advantages

---

[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1649267035/interactive_app_design/react-brand_jbef09.svg)

^ You're all hear to learn React. Does anyone know what React is?

---

> A JavaScript library for building user interfaces.
-- reactjs.org

---

> A declarative, component-based, flexible library for building efficient and interactive web applications.

^ **Declarative**: We will develop "views" for each state in our application. React will update and render these components when our data changes. As users interact with our application, we can easily update parts of the application without having to re-render the entire page.

^ **Component-based**: React components are self-contained pieces of UI that can be composed to build more complex components. Each encapsulated component has its own state and behavior.

^ Everything in React is JavaScript!

---

[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1649267035/interactive_app_design/react-brand_jbef09.svg)

^ Okay so what does all this mean? React is a library, not a framework. A library is a collection of code that we can use in our project. Our project is not completely dependent on it.

^ A framework is a complete package of code with its own functionalities, libraries, and rules. (Show AngularJS)

---

[.background-color: #0e0f10]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1650638999/interactive_app_design/mozilla_webdocs_bpdmi0.svg)

^ React uses a virtual DOM. The DOM is the representation of the HTML code in a webpage and the model of DOM is a tree structure. <https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction>

^ Each time we make a change in the code, the DOM will be rewritten and updated, which takes time. In many cases when the changes are not significant, it's not necessary to update the whole DOM. (show browser inspector)

^ React creates an exact copy of the DOM called the virtual DOM. When there's a change in the code, React compares the virtual DOM with the real DOM and figures out which components need to be updated. React copies only the new parts of the virtual DOM to the real DOM instead of completely rewriting the real DOM. This approach is much faster.

---

## A component

```html
<header>
  <h1>Hello World</h1>
</header>
```

---

## A component

```php
<?php
  require_once "_header.php";
?>>
```

---

## A component

```jsx
const Header = () => (
  <header>
    <h1>Hello World</h1>
  </header>
);

export default Header;
```

---

## A component

```jsx
import Header from './components/Header';

const Layout = () => (
  <Header />
);

export default Layout;
```

---

## Benefits of React

- speed
- flexibility
- performance
- reusable components

^ Every new library or framework claims to be better than its predecessors in some respect. Anyone familiar with jQuery? jQuery made it easy to write cross-browser code in native JavaScript. Back then jQuery was considered a framework, but not anymore.

^ Similarly with things like Backbone and then Angular, each new JavaScript framework brings something new to the table and React isn't unique in this. What is new with React is that it challenges some of the core concepts used by most popular front-end frameworks: for example, the idea that you have to have templates.

---

## React vs Other Libraries

- simpler apps
- fast UIs
- less code

^ React is written in pure JavaScript, in a declarative style with powerful, developer-friendly DOM abstractions (and not just DOM, but also iOS, Android etc)

^ React provides outstanding performance thanks to a virtual DOM and a smart-reconciliation algorithm.

^ React's great community and vast ecosystem of components provide developers with a variety of libraries and components.

^ Many features make React simpler to work with than most other front-end frameworks.

---

## ReactJS vs React Native

---

## ReactJS

- ReactJS is a javascript library
- requires a code bundler
- responsible for the rendering of UI components

^ _(click)_ When you start a new project with ReactJS, you will choose a _(click)_ bundler like Webpack and try to figure out which bundling modules you need for your project. _(click)_ The React code is compiled into JavaScript which then runs in the browser as part of a web site or web based application.

---

### ReactJS Example

```jsx
const App = () => (
  <div>
    <p>Hello World</p>
  </div>
)

export default App;
```

---

## React Native

- requires Xcode or Android Studio
- doesn’t use HTML

^ React Native is used for building native applications. The application is coded in React Native, and then _(click)_ imported into Xcode or Android Studio and then compiled into a native app.

^ _(click)_ React-Native doesn’t use HTML to render the app, but provides alternative components that work in a similar way. Those React-Native components map the actual real native iOS or Android UI components that get rendered on the app.

[^1]: [website](https://medium.com/@alexmngn/from-reactjs-to-react-native-what-are-the-main-differences-between-both-d6e8e88ebf24)

---

### React Native Example

```jsx
import { Component } from 'react';
import { View, Text } from 'react-native';

export default class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.intro}>Hello world!</Text>
      </View>
    );
  }
}
```

---

# TLDR

## Let's go already

---

# Objective

## Discuss tooling and editor setup

---

## Tools For Getting Started

- [Node.js](https://nodejs.org/en/)
- [NPM](https://www.npmjs.com)
- [Yarn](https://yarnpkg.com)
- [ReactJS Devtools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
- [ReactJS Devtools for Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
- [ES7 React Snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
- [React PropTypes](https://marketplace.visualstudio.com/items?itemName=suming.react-proptypes-generate)

---

## Compilers & Packages

- [react-scripts](https://www.npmjs.com/package/react-scripts)
- [webpack](https://webpack.js.org)
- [parcel](https://parceljs.org)
- [babel](https://babeljs.io)

---

## More helpful resources

- [eslint](https://eslint.org)
- [prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

---

## Detour

^ Before we keep going, I need to know how comfortable you all are with using the command line and how experienced you are with things like Node.js and package managers like NPM and yarn.

---

# Objective

## Discuss modern Javascript syntax

---

## ES Modules

```javascript
// commonJS
module.exports = {
  add: function(a, b) {
    return a + b
  };
}
const utils = require('./utils.js');

//ES Modules
export function add(a, b) {
  return a + b;
}
import { add } from './utils.js';
```

^ As of ES6 (2015), Javascript supports a native modules format called ES Modules. This approach uses the `export` and `import` keywords, instead of the older CommonJS syntax of `module.exports` and `require()`.

---

## Import

```javascript
import PropTypes from 'prop-types';
import Header from './components/Header';
import { add } from './scripts/utils';
```

^ We can import local files as well as third-party packages we've installed with our package manager.

---

## Named Exports

```javascript
export let name = 'Jane';
export const age { age: 25 };

import {name, age} from './scripts/utils';
```

---

## Default Exports

```javascript
export default k = 12;

import k from './scripts/k.js';
```

---

# Objective

## Create a React App

---

## Create a React app

```sh
# Install the create-react-app package globally
npm i -g create-react-app

# Create a new React application
npx create-react-app my_app
```

^ You may need to use `sudo`

^ Let's explore what happens when we run `create-react-app`

---

# Objective

## Introduce JSX

^ One of the things we mentioned as a benefit to React is its simplicity and easiness to read. That last example doesn't look very easy to read, or maintain for that matter. Now it's time to look at JSX, one of the best things about React (in my opinion).

^ JSX is a JavaScript extension that provides syntactical sugar for function calls and object construction. It may look like a template engine or HTML, but it isn't. JSX produces React elements while allowing you to harness the full power of JavaScript. It is not required for React, but it is highly recommended by React's creators.

---

## Hello World & A Link

```javascript
React.createElement(
  'div',
  null,
  React.createElement(HelloWorld, null),
  React.createElement(
    'a',
    { href: 'http://example.com' },
    'Example Website'
  )
)
```

---

### Hello World & A Link - JSX

```jsx
<div>
  <HelloWorld />
  <a href="http://example.com">Example website</a>
</div>
```

^ To demonstrate the eloquence of JSX, here is the code to create `HelloWorld` and a link element:

^ JSX is a small language with an XML-like syntax, but it has changed the way people write UI components. Previously developers wrote HTML and JavaScript code for the controllers and views, jumping between various files. With JSX, the JS and HTML are tightly coupled to implement various pieces of functionality.

^ It looks like regular HTML and is easier to read and write.

---

## JSX ➡️ Browser

1. Write JSX code
1. Run JSX through transpiler
1. Save vanilla JavaScript file
1. Load `.js` in browser

---

## Creating Element With JSX

```javascript
React.createElement(
  name,
  { key: value, ... },
  child
)
```

Becomes:

```jsx
<name key=value>
  <child />
</name>
```

^ Instead of writing the top example, we can use JSX, where the attributes and their values come from the second argument of the `createElement()` method.

---

### HelloWorld Review

```javascript
ReactDOM.render(
  React.createElement('h1', null, 'Hello world!'),
  document.getElementById('content')
)
```

---

### HelloWorld JSX

```jsx
ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('content')
)
```

^ The JSX version is much more compact.

---

## Working With JSX In Components

```jsx
// HelloWorld.jsx
const HelloWorld = () => (
  <h1>Hello World</h1>
)

// App.jsx
import HelloWorld from './HelloWorld.jsx';

const App = () => (
    <HelloWorld />
);
```

^ The previous example used the `h1` JSX tag, which is also a standard HTML tag name. When working with components, you apply the same syntax. The only difference is that the component class name must start with a capital letter. Let's rewrite `HelloWorld` using JSX.

---

### Class based components

```jsx
class HelloWorld extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello world!</h1>
      </div>
    )
  }
}

ReactDOM.render(
  <HelloWorld />,
  document.getElementById('content')
);
```

---

## Outputting Variables In JSX

```jsx
const DateTimeNow = () => {
  let dateTimeNow = new Date().toLocaleString();
  return <span>Current date and time is {dateTimeNow}.</span>
}
```

^ You want your component to be smart enough to change the view based on some code. For example, a current date-time component should use the actual current date and time, not a hard coded value.

^ In JSX, you can use curly braces notation to output variables dynamically.

---

## Working With Properties In JSX

^ You can pass properties in JSX as you would in normal HTML. You also render standard HTML attributes by setting element properties.

---

### Hard Coded Properties

```jsx
const App = () => (
  <Header
    title="My Title"
    subtitle="My Subtitle"
   />>
)
```

^ Using hard coded values for attributes isn't flexible. If you want to reuse the component, the `href` must change to reflect a different address each time. So we need a component that can use dynamic values for attributes.

---

### Flexible Properties

```jsx
const Header = (props) => (
  <header title={props.title}>
    <h1>{props.title}</h1>
    <h2>{props.subtitle}</h2>
  </header>
)
```

---

#### Deconstruct Flexible Properties

```jsx
const Header = ({title, subtitle}) => (
  <header title={title}>
    <h1>{title}</h1>
    <h2>{subtitle}</h2>
  </header>
)
```

---

### Properties

```jsx
<ProfileLink
  url='http://profile.com'
  label='Profile for user'
  displayText='go to profile'
/>
```

^ The properties are defined when the component is created. These properties are passed to the component, and accessed via `props` followed by the property name you want to access.

---

## Creating Component Methods

```jsx
const Content = () => {
  const getURL = () => 'http://webapplog.com';

  return (
    <a href={getURL()}>
      {getURL()}
    </a>
  )
}
```

^ As a developer, you're free to write any component methods for your application. Here's a simple example. You can use the `getURL()` method within your other class methods.

---

## if/else in JSX

```jsx
render() {
  if (props.isLoggedIn)
    return <a href="/logout">Sign Out</a>
  else
    return <a href="/login">Sign In</a>
}
```

^ Since we're working with JavaScript, we can use logic to change our views based on the results of conditional statements.

---

## Conditional (ternary) operator

```jsx
const MyComponent = ({isLoggedIn}) => {
  !isLoggedIn ? (
    <a href="/login">Sign In</a>
  ) : (
    <a href="/logout">Sign Out</a>
  )
}
```

---

## JSX Comments

```jsx
let content = (
  <div>
    {/* this is a comment */}
  </div>
)
```

^ Comments in JSX are similar to comments in regular JavaScript, but you have to wrap standard JavaScript comments in curly braces.

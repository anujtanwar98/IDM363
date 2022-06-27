build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## Layouts & Layout Components

---

# Lesson Objectives

- Discuss layouts and layout components

---

## A `header`

```html
<header>
  <img src="" alt="our logo" />
  <nav>
    <ul>
      <li><a href="">Home</a></li>
      <li><a href="">About</a></li>
      <li><a href="">Contact</a></li>
    </ul>
  </nav>
</header>
```

^ If you think back to our first web development class, we learned HTML structure. You coded a portfolio project using HTML and CSS. When you created a component, like a `header`, you had to include the code for the `header` on every HTML page you wanted the header to appear on.

---

## A `header`

```php
<?php require_once "includes/_header.php"; ?>
```

^ When we discussed server side scripting, we learned how to include partial files, which made managing our components easier. We're talking about a similar concept here. We want to create reusable components like our `header`, but we also want to create top level layout components that we can use for multiple views in our apps.

---

## Layouts

```
src
|  assets
|  components
|  +-- Header.jsx
|  +-- Footer.jsx
|  +-- layouts
|      +-- Layout.jsx
|  App.jsx
|  index.css
|  index.js
```

^ Layout components accept `children` as `props` and render them to the DOM. It's usually a good practice to separate layout components from other components.

---

## Layout Component

```jsx
import Header from './Header';
import Footer from './Footer';

const Layout = ({ children }) => (
  <Header />
  <main>
    {children}
  </main>
  <Footer />
);
```

^ Here's an example of a layout component using the `children` prop to render content passed to the layout from the parent component.

---

## Children prop

```jsx
import Layout from './layouts/Layout';

function App() {
  return (
    <Layout>
      <h1>Hello World</h1>
    </Layout>
  )
};
```

---

## Passing `props`

```jsx
import Layout from './layouts/Layout';
import { getPrimaryMenu } from '../lib/api';

function App() {
  return (
    <Layout menu={getPrimaryMenu}>
      <h1>Hello World</h1>
    </Layout>
  )
}
```

---

## Passing `props`

```jsx
// Layout.jsx
import Header from './components/Header.jsx';

const Layout = ({children, menu}) => (
  <Header menuItems={menu} />
  <main>{children}</main>
)

export default Layout;
```

---

## Passing `props`

```jsx
// Header.jsx
const Header = ({menuItems}) => (
  <ul>
    {menuItems.map(item => (
      <li key={item.node}>
        {item.label}
      </li>
    ))}
  </ul>
)

export default Layout;
```

---

## Fragments

```jsx
const Box = () => (
  <div>one</div>
  <div>two</div>
)

// Error
```

^ Because JavaScript functions can only return one element, a problem exists if we build a component that is made up of multiple elements.

---

## Fragments

```jsx
const Box = () => (
  <div>
    <div>one</div>
    <div>two</div>
  </div>
)

// No error, extra div
```

^ If we add a parent element, we can eliminate the error since we're only returning a single element. This technique can impact our CSS though.

---

## Fragments

```jsx
const Box = () => (
  <React.Fragment>
    <div>one</div>
    <div>two</div>
  </React.Fragment>
)

// No error, no extra div
```

^ Fragments let you group multiple child elements without adding any extra nodes to the DOM.

---

## Fragment Short Syntax

```jsx
const Box = () => (
  <>
    <div>one</div>
    <div>two</div>
  </>
)

// No error, no extra div, type less
```

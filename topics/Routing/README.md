build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## Routing

---

# Lesson Objectives

- Discuss browser URL routing
- Introduce React Router

https://reactrouter.com/docs/en/v6/getting-started/tutorial

---

# Objective

## Discuss browser URL routing

^ So far everything we've been building has been within a single view. As applications get more complex, the view will need to change dramatically, loading different components with various states in and out. In the past, in many applications the URL rarely changed as users progress through the app. Only the content area changed.

---

## Consequences of a single URL

- refresh browser = restart application
- browsing history not recorded properly
- can't share
- SEO 😢

^ This approach had some negatives.

^ Refreshing the browser took the user back to the original view of the application.

^ Clicking the back button on the browser may take you to a completely different site.

^ Sharing a precise page within the app wasn't possible.

^ Search engines couldn't index the site because there were no legit URLs.

---

### `https://mywebsite.com/books/jsreact`

^ Fortunately, today we have browser URL routing. URL routing lets you configure an application to accept request URLs that don’t map to physical files. Instead, you can define URLs that are semantically meaningful to users, that can help with search-engine optimization (SEO), and that can reflect your application’s state.

^ This URL is for a page that displays information about a book. Behind the scenes, we are using a single page app and the URL maps to a view that displays information about a product with the id _jsreact_. You can browse other products, the URL can change and both the browser and search engines would work as you'd expect, but the site would still be run through a React application.

---

## Routing by hand

```jsx
const App = () => {
  const [hash, setHash] = useState('');

  useEffect(() => {
    window.addEventListener(
      'hashChange',
      () => setHash('new-hash')
    )
  }, [])
}
```

^ To implement a routing system, we can take advantage of the React lifecycle methods to listen for changes to the window location. We would also keep track of the changes in a one form or another so we could manage the browsing history. While all of this is possible, this is one case where we can take advantage of some of the available tools to make our lives easier.

---

[.background-color: #252525]
[.slidenumbers: false]
[.hide-footer]

![50%](https://res.cloudinary.com/pjs-uxid/image/upload/v1649959178/interactive_app_design/8r0ymglytx7xi3uzme48_gmdwhp.png)

^ React Router isn't part of the official React core library. It actually came from the working community, but it is popular enough that it is recommended by the official React documentation.

---

## Installation

```sh
npm install react-router-dom@6
```

^ The following examples are based on the instructions for an application created using the `create-react-app` command. If you're using a different bundler like Parcel or Webpack, the instructions will vary slightly. Consult the official documentation for specific instructions.

---

## Import the library

```javascript
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```

^ Once React Router is installed as a dependency, import the library into your main index file `src/index.js` and wrap your app in a `<BrowserRouter>`.

---

## Using the router

```jsx
import { Routes, Route, Link } from "react-router-dom";
import "./App.css";

function App() {
  return (
    <div className="App">
      <h1>Welcome to React Router!</h1>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="about" element={<About />} />
      </Routes>
    </div>
  );
}
```

^ Now you can use React Router anywhere in your app! For a simple example, open `src/App.js` and replace the default markup with some routes.

---

## Navigation

```jsx
import { Link } from "react-router-dom";

function Home() {
  return (
    <div>
      <h1>Home</h1>
      <nav>
        <Link to="/">Home</Link> |{" "}
        <Link to="about">About</Link>
      </nav>
    </div>
  );
}
```

^ Use Link to let the user change the URL.

---

## Navigation

```jsx
import { useNavigate } from "react-router-dom";

function Invoices() {
  let navigate = useNavigate();
  return (
    <div>
      <NewInvoiceForm
        onSubmit={async (event) => {
          let newInvoice = await createInvoice(
            event.target
          );
          navigate(`/invoices/${newInvoice.id}`);
        }}
      />
    </div>
  );
}
```

^ Or useNavigate to do it yourself (like after form submissions).

---

## Nested routes

```jsx
function App() {
  return (
    <Routes>
      <Route path="invoices" element={<Invoices />}>
        <Route path=":invoiceId" element={<Invoice />} />
        <Route path="sent" element={<SentInvoices />} />
      </Route>
    </Routes>
  );
}
```

^ This is one of the most powerful features of React Router making it so you don't have to mess around with complicated layout code. The vast majority of your layouts are coupled to segments of the URL and React Router embraces this fully.

^ Routes can be nested inside one another, and their paths will nest too (child inheriting the parent).

---

## Route configurations

- `/invoices`
- `/invoices/sent`
- `/invoices/:invoiceId`

^ This route config defined three route paths.

---

### `/invoices/sent`

```jsx
<App>
  <Invoices>
    <SentInvoices />
  </Invoices>
</App>
```

---

### `/invoices/123`

```jsx
<App>
  <Invoices>
    <Invoice />
  </Invoices>
</App>
```

---

## Not found routes

```jsx
function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="dashboard" element={<Dashboard />} />
      <Route path="*" element={<NotFound />} />
    </Routes>
  );
}
```

^ When no other route matches the URL, you can render a "not found" route using `path="*"`. This route will match any URL, but will have the weakest precedence so the router will only pick it if no other routes match.

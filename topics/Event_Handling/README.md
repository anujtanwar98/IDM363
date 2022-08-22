build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Handling Events

---

# Lesson Objectives

- Discuss how to handle events in React

^ Handling events with React is very similar to handling events on DOM elements. There are a couple syntax differences.

---

## DOM events

```javascript
function clickHandler() {
  console.log('clicked')
}

const element = document.getElementById('myElement');

element.addEventListener('click', clickHandler);
```

^ Recall how we can setup event listeners in JavaScript that will call a function or method when triggered. Also remember that in React, we're trying to not directly effect the DOM. Instead we'll use React to implement and execute events based on user interaction with our applications.

---

## React events

```jsx
const App = () => {
  function handleClick() {
    console.log('clicked');
  }

  return (
    <button onClick={handleClick}>
  )
}
```

^ When using React, we generally don't need to call `addEventListener` to add listeners to a DOM element after it's created. Instead, we provide a listener when the element is rendered.

---

## Default events

```jsx
const Form = () => {
  function handleSubmit(event) {
    event.preventDefault();
    console.log('You submitted the form');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  )
}
```

^ You can prevent default behavior by calling the `preventDefault` function.

---

## Event naming

```javascript
// javascript
<button onclick="doAwesome()">
  Do Something Awesome
</button>
```

```jsx
// React JSX
<button onClick={doAwesome}>
  Do Something Awesome
</button>
```

^ React events are named using camelCase, rather than lowercase.

---

## Passing arguments to event handlers

Can't do this:

```jsx
<button onClick={doAwesome(index)}>
  Do Something Awesome
</button>
```

^ What if we need to pass a parameter to our function when our button is clicked?

^ We can't do this because our `doAwesome` function is going to be executed when our component mounts.

---

## Use arrow functions

Do this:

```jsx
<button onClick={() => doAwesome(index)}>
  Do Something Awesome
</button>
```

---

## Inline functions

```jsx
<button onClick={() => {
  // do something awesome inline
}}>
  Do Something Awesome
</button>
```

^ Inline arrow functions can be used in cases where it's not necessary to bind to an externally defined function. There are some performance issues with this method.

^ We'll look at more examples of these types of cases when we discuss state and loops in React.

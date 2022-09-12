build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Lists & Keys

---

# Lesson Objectives

- Discuss transforming lists
- Discuss rendering multiple components
- Discuss React keys

---

# Objective

## Discuss transforming lists

---

## Loops & iterations

- for
- do...while
- while
- for...in
- for...of

---

## Array Methods

- foreach
- filter
- map
- reduce

---

## `Array.map()`

```javascript
const myArray = [1, 4, 9, 16]

const myMap = myArray.map(x => x * 2)

console.log(myMap)
// Array [2, 8, 18, 32]
```

^ The `map()` method **creates a new array** populated with the results of calling a provided function on every element in the calling array.

---

## `.map()` Syntax

```javascript
map((element, index, array) => {})
```

^ **element** is the current element being processed in the array.

^ **index** is the current element being processed.

^ **array** is the array map was called upon.

---

# Objective

## Discuss rendering multiple components

---

```jsx
const numbers = [1, 2, 3, 4, 5]

const listItems = numbers.map(number => (
  <li>{number}</li>
))

const MyList() => (
  <ul>{listItems}</ul>
)
```

^ We can build collections of elements and include them in JSX using curly braces. In this example, we loop through the numbers array using the JavaScript `map()` function. At each iteration, we return a `<li>` element for each item. The array of list items are assigned to the `listItems` variable. We can include the entire `listItems` array inside a `<ul>` element.

---

## A `key` warning

```jsx
const numbers = [1, 2, 3, 4, 5]

const listItems = numbers.map(number => (
  <li key={number.toString()}>{number}</li>
))

const MyList() => (
  <ul>{listItems}</ul>
)
```

^ When you run this code, you'll be given a warning that a key should be provided for the list items. A `key` is a special string attribute you need to include when creating lists of elements. We can assign a `key` to our list items inside our `map` function.

---

# Objective

## Discuss React keys

^ Keys help React identify which items have changed, are added, or removed. Keys should be given to elements inside the array to give the elements a stable identity.

---

```javascript
const todos = [
  {
    id: 1,
    text: 'Item 1'
  },
  {
    id: 2,
    text: 'Item 2'
  },
  {
    id: 3,
    text: 'Item 3'
  }
]
```

```jsx
const todoItems = todos.map((todo) => (
  <li key={todo.id}>
    {todo.text}
  </li>
))
```

^ The best way to pick keys is to use a string that uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys. Keys must be unique among siblings.

---

## `uuid`

```javascript
import { v4 as uuidv4 } from 'uuid';

uuidv4(); // ⇨ '9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d'
```

^ One of my favorite packages for dealing with keys is the `uuid` package. UUID stands for universally unique identifier. The `uuid` package we're talking about here can be installed into our project and imported anywhere we want to create a unique identifier. If you're working with data that doesn't have an ID or unique value to use for your keys, this package can help.

---

### `uuid` Quick Start

```sh
npm install uuid
```

```jsx
import { v4 as uuidv4 } from 'uuid';

const todoItems = todos.map((todo) => (
  <li key={uuidv4()}>
    {todo.text}
  </li>
))
```

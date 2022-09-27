build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Modern Front-End Frameworks

---

[.background-color: #222222]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1656356093/interactive_app_design/comparison_logos_ielisi.png)

^ You all know we're working in a fast-changing industry. Front-end development is full of frameworks, many of which didn't exist a few years ago. Who remembers jQuery? jQuery is more of a library that makes manipulating HTML documents easier. jQuery was the top dog for a while. Angular, which was released in 2010, was (and still is) big. Today I think the top dogs are React, Svelte, and Vue.

^ We've spent the last weeks covering the basics of React. It's important you know these other options exist. Depending on your project, you may find Vue or Svelte can help you get the job done more efficiently.

---

# Objectives

- Introduce Vue
- Introduce Svelte

---

# Objective

## Introduce Vue

^ To be honest, I've never used Vue.

---

```javascript
import { createApp } from 'vue'

createApp({
  data() {
    return {
      count: 0
    }
  }
}).mount('#app')
```

```html
<div id="app">
  <button @click="count++">
    Count is: {{ count }}
  </button>
</div>
```

^ I know Vue has an extensive library and developers love the documentation. It's supposed to be highly adaptable and scalable, and apparently if you have any experience with React or Angular, you should be able to pick it up quickly.

---

# Objective

## Introduce [Svelte](https://insights.stackoverflow.com/survey/2021#section-most-loved-dreaded-and-wanted-web-frameworks)

[~1]: [StackOverflow](https://insights.stackoverflow.com/survey/2021#section-most-loved-dreaded-and-wanted-web-frameworks)

^ Svelte is awesome (at least to me). Svelte doesn't do it's heavy lifting in the browser like React or Vue. Svelte has a compile step that happens when you build your app. React compares a virual DOM to the actual DOM, figures out the differences, and updates the app. Svelte surgically updates the DOM when your app changes.

^ Svelte was recently voted the most loved web framework with the most satisfied developers in a pair of industry surveys.

---

```javascript
import {useState} from 'react'

function MyComponent() {
  const [name, setName] = useState('world')

  return (
    <h1>Hello {name}</h1>
  )
}
```

---

```html
<script>
  let name = 'world'
</script>

<h1>Hello {name}</h1>
```

---

```html
<script>
  let name = 'world'
</script>

<h1>Hello {name}</h1>

<style>
  h1 {
    color: purple;
  }
</style>
```

^ CSS is scoped automatically

---

## Getting started with Svelte

- [Svelte](https://svelte.dev)
- [SvelteKit](https://kit.svelte.dev)

^ SvelteKit is the official applicaiton framework from the Svelte team (think Next.js). Let's run through one of the examples from the documentation.

^ npm prepare

---

## Svelte example project

^ `playground/svelte_mysql`

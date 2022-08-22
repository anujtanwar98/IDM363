build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Forms

---

# Lesson Objectives

- Discuss controlled components
- Discuss text input example
- Discuss select element example

---

# Objective

## Discuss controlled components

^ In HTML, form elements such as `input`, `textarea`, and `select` typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with `setState()`.

^ We need a single source of truth. Controlled components will use React's state as the source for the value of these inputs. We'll use React's state to also maintain the element values, so everything stays in sync.

---

```html
<form method="" action="">
  <label>
    Name:
    <input type="text" value="" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

---

```jsx
return (
  <form onSubmit={handleSubmit}>
    <label>
      Name:
      <input type="text" value={stateValue} onChange={handleChange} />
    </label>
    <input type="submit" value="Submit" />
  </form>
)
```

^ The input value is controlled by React state. The change handler updates the state, which is reflected in the input value.

---

# Objective

## Complete text input example

---

```jsx
const [inputValue, setInputValue] = useState('')
const handleChange = event => {
  setInputValue(event.target.value)
}

return (
  <form>
    <label>
      Name:
      <input type="text" value={inputValue} onChange={handleChange} />
    </label>
    <input type="submit" value="Submit" />
  </form>
)
```

---

# Objective

## Complete select element example

---

```html
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

^ Note that the Coconut option is initially selected, because of the selected attribute.

---

```jsx
const [flavor, setFlavor] = useState('coconut')
const handleChange = event => {
  setFlavor(event.target.value)
}

return (
  <label>
    Pick your favorite flavor:
    <select value={flavor} onChange={handleChange}>
      <option value="grapefruit">Grapefruit</option>
      <option value="lime">Lime</option>
      <option value="coconut">Coconut</option>
      <option value="mango">Mango</option>
    </select>
  </label>
)
```

^ React, instead of using this selected attribute, uses a value attribute on the root select tag. This is more convenient in a controlled component because you only need to update it in one place. For example:

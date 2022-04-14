build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## PropTypes

---

# Lesson Objectives

- Discuss PropTypes

^ As your app grows, you can catch a lot of bugs with typechecking. For some applications, you can use JavaScript extensions like Flow or TypeScript to type check your whole application. But even if you don’t use those, React has some built-in typechecking abilities. To run typechecking on the props for a component, you can assign the special propTypes property.

---

## PropType Example

```javascript
import PropTypes from 'prop-types';

const Greeting = ({name}) => (
  <h1>Hello, {name}</h1>
);

Greeting.propTypes = {
  name: PropTypes.string
};
```

^ `PropTypes` exports a range of validators that can be used to make sure the data you receive is valid. In this example, we’re using `PropTypes.string`. When an invalid value is provided for a prop, a warning will be shown in the JavaScript console. For performance reasons, propTypes is only checked in development mode.

---

## Validators

- `PropTypes.array`
- `PropTypes.bool`
- `PropTypes.func`
- `PropTypes.number`
- `PropTypes.object`
- `PropTypes.string`
- `PropTypes.symbol`

^ Here are examples of the different validators that are provided.

---

## Required Props

```javascript
Accordion.propTypes = {
  id: PropTypes.string.isRequired,
  modifier: PropTypes.string.isRequired,
  source: PropTypes.object.isRequired,
  type: PropTypes.string.isRequired
};
```

^ You can not only specify the prop types you want to validate, but you can also denote that they are required, which will throw an error if the prop type is incorrect, or if the prop is not provided at all.

---

## Reference

- [prop-types](https://www.npmjs.com/package/prop-types)
- [Reactjs.org](https://reactjs.org/docs/typechecking-with-proptypes.html)

^ The full reference of all the options available can be found on the React official website.

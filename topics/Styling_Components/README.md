build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## Styling Components

---

# Lesson Objectives

- Discuss CSS & SASS stylesheets
- Discuss CSS modules
- Discuss `styled-components`

---

# Objective

## Discuss CSS & SASS stylesheets

---

```scss
// Box.scss
.Box {
  margin: 40px;
  border: 5px black;

  .Box_content {
    font-size: 16px;
    text-align: center;
  }
}
```

^ CSS or SCSS Stylesheets is a styling strategy that involves the use of external CSS or SASS stylesheets that can be imported into your React components depending on where you need the styling to be applied.

^ For example, we have a SASS file of styles called Box.scss we need to use in a component called Box.js, below is the code for our SASS file.

---

```jsx
import './Box.css';

const Box = () => (
  <div className="Box">
    <p className="Box_content"> Styling React Components </p>
  </div>
);

export default Box;
```

^ In order to make use of this styling inside our Box component all we need to do is import the SASS file directly into our Box.js component like so.

^ After creating the styles and importing it into Box.js file, we can then set the className attribute to the match what we have in the stylesheet.

^ While using this strategy, you could also leverage on existing frameworks like; Bootstrap, etc. These frameworks provide you with existing classes and components you could plug into your React application without styling every aspect of your application.

---

## Benefits of CSS & SASS Stylesheets

- popularity
- caching & performance
- un-opinionated
- quick iteration
- CSS frameworks

^ It is much more popular than the rest of the styling strategies, so there is a ton of helpful resources when you run into a bug.

^ Standard CSS files are easy for the browser to optimize for, caching the files locally for repeat visits, and ultimately giving performance wins.

^ CSS and SASS is universal and has no opinion on how you render your UI making it a great choice for teams that have legacy CSS and are migrating over to a new framework or rebuilding their website or product.

^ You can very easily rip out the entire stylesheet and create a new one to refresh the look and feel of your app without digging through potentially hundreds of components.

^ CSS frameworks come in handy if you are a new developer, or you want to quickly work on a prototype without diving deep into writing your own full-blown stylesheets. CSS frameworks will provide you with building blocks to get your idea off the ground. Some of these frameworks include, Bootstrap, Semantic UI, Materialize.

---

## Shortcomings of CSS & SASS Stylesheets

- readability
- legacy CSS

^ If not properly structured, a CSS or SASS stylesheet can become long and difficult to navigate through as the application becomes complex.

^ Most times these really large stylesheets can become so complex and long that cleaning up old, outdated or even unused styles can be a pain.

---

# Objective

## Discuss CSS Module

^ A CSS Module is a CSS file in which all class names and animation names are scoped locally by default. When using CSS Modules, each React component is provided with its own CSS file, that is scoped to that file and component alone.

^ The beauty of CSS modules happens at build time when the local class names which can be super simple without conflict are mapped directly to the automatically-generated ones and are exported as a JS object literal to use within React.

^ We can make use of CSS Modules in our React applications by importing the file directly into the component file.

---

```css
/* Box.css */
.container {
  margin: 40px;
  border: 5px dashed pink;
}

.content {
  font-size: 15px;
  text-align: center;
}
```

---

```jsx
import styles from './Box.css';

const Box = () => (
  <div className={styles.container}>
    <p className={styles.content}> Styling React Components </p>
  </div>
);

export default Box;
```

^ In other to make use of this CSS Module inside our Box component we need to import the module file directly into our `Box.js` component and use the `className` instead of `style` prop to access the style like so:

^ `styles` here is an object that contains the styles we created in `Box.css`. This object will contain the classes; `container` and `content` that maps to their respective styles. To make use of them, we assign the element’s `className` to the appropriate class we have in `Box.css`.

---

## Benefits of using CSS modules

- modular, reusable CSS
- no styling conflicts (local scope)
- no code duplication
- variable sharing & JavaScript exposure

---

## Shortcomings of using CSS modules

- mixing CSS modules & global CSS is extra work
- `styles` object when constructing a `className`
- recommends `camelCase` for class names
  - dashes are possible
  - `className={styles['some-class-name']}`

---

# Objective

## Discuss `styled-components`

^ `styled-components` is a library for React and React Native that allows you to use component-level styles in your application that are written with a mixture of JavaScript and CSS.

^ It was created with the same method of operation of CSS Modules, a way to write CSS that’s scoped to a single component, and not accessible to any other element in the page or even component.

^ `styled-components` allows React developers to write plain CSS in React components without having to worry about clashing of class names.

---

## Using `styled-components`

1. install `styled-components`
    `npm install --save styled-components`
1. import the library
    `import styled from 'styled-components';`

---

```jsx
import styled from 'styled-components';

const Box = styled.div`
  margin: 40px;
  border: 5px black;
`;

const Content = styled.p`
  font-size: 16px;
  text-align: center;
`;

const Box = () => (
  <Box>
    <Content> Styling React Components </Content>
  </Box>
);

export default Box;
```

^ Now we can create a variable by selecting a particular HTML element where we store our style keys.

^ Then we use the name of our variable we created as a wrapper around our JSX elements.

---

```jsx
// StyledBox.js
import styled from 'styled-components';


const StyledBox = styled.div`
  margin: 40px;
  border: 5px black;

  .content {
    p {
      font-size: 16px;
      text-align: center;
    }
  }
`

export default StyledBox;
```

---

```jsx
// Box.jsx
import StyledBox from './StyledBox';

const Box = () => (
  <StyledBox>
    <div className="content">
      <p>Styling React Components</p>
    </div>
  </StyledBox>
)

export default Box;
```

---

## Benefits of using styled components

- SASS syntax
- Dynamic styling
- Theming

^ You can get SASS trademark syntax out of the box without having to install or setup SASS or any extra build tool.

^ You can make use of props to dynamically change the styles in any way that feels natural to anyone comfortable with React.

^ Using React’s Context API, styled-components offers a `ThemeContext` that can you can pass a theme object directly to, making it very accessible in any of your components, and by default can be interpolated into your styled definitions.

---

## Shortcomings of using styled components

- learning curve
- integration with legacy CSS can be difficult
- performance

^ Frontend developers that are already comfortable with writing traditional CSS will have to learn a different way of styling that is different from how traditional CSS is written.

^ If you’re making use of a UI library like Material UI or even traditional CSS, integrating styled-components together with them can be confusing to locate and debug styles.

^ styled-components converts all of the style definitions in your React component into plain CSS at build time and the inject everything into the `<style>` tags in the head of your `index.html` file. This affects performance in the sense that it is not only increasing the size of our HTML file which can have an impact on the load time, but there is also no way to chunk the output CSS either.

---

## References

- Akintayo, S. (2020, May 14). Styling Components In React. Smashing Magazine. <https://www.smashingmagazine.com/2020/05/styling-components-react/>

build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Conditional Rendering

---

# Lesson Objectives

- Discuss/Review JavaScript conditional scripting
- Discuss React conditional rendering & inline operators

---

# Objective

## Discuss/Review JavaScript conditional scripting

---

## If Else

```javascript
function testNum(a) {
  let result

  if (a > 0)
    result = 'positive'
  else
    result = 'negative'

  return result
}
```

^ Everyone is familiar with the `if...else` statement. We use logic like this is many programming languages.

---

## Ternary operator

```javascript
function testNum(a) {
  return a > 0 ? 'positive' : 'negative'
}
```

^ You may not be familiar with the ternary operator.

---

## Ternary operator syntax

```javascript
return a > 0 ?
```

^ The ternary operator takes three operands: a condition followed by a question mark...

---

## Ternary operator syntax

```javascript
return a > 0 ? 'positive'
```

^ ...then an expression to execute if the condition is true,

---

## Ternary operator syntax

```javascript
return a > 0 ? 'positive' : 'negative'
```

^ followed by a colon, and finally the expression to execute if the condition is false.

---

## Ternary operator syntax

```javascript
return a > 0     ? 'positive' : 'negative'

       condition ? exprIfTrue : exprIfFalse
```

---

### A simple example

```javascript
let age = 26
let beverage = (age >= 21) ? 'beer' : 'juice'

console.log(beverage) // beer
```

---

# Objective

## Discuss React conditional rendering

^ In React, you can change which components are rendered depending on the state of your application.

^ Conditional rendering in React works the same way conditions work in JavaScript. You can use operators like `if` or the `conditional operator` to create elements based on the current state.

---

```jsx
function UserGreeting() {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting() {
  return <h1>Please sign up.</h1>;
}

function Greeting({isLoggedIn}) {
  if (isLoggedIn) {
    return <UserGreeting />;
  }

  return <GuestGreeting />;
}
```

^ Here are two components. We'll display one of these depending on whether a user is logged in.

---

```jsx
function UserGreeting() {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting() {
  return <h1>Please sign up.</h1>;
}

function Greeting({isLoggedIn}) {
  return isLoggedIn ? <UserGreeting /> : <GuestGreeting />
}
```

^ Refactor to simplify the return statement.

---

```jsx
function Greeting({isLoggedIn}) {
  return isLoggedIn
    ? <h1>Welcome back!</h1>
    : <h1>Please sign up.</h1>
}
```

^ Refactor again to eliminate the greeting functions. Can we do better?

---

```jsx
function Greeting({isLoggedIn}) {
  return (
    <h1>
      {isLoggedIn ? 'Welcome back!' : 'Please sign up.'}
    </h1>
  )
}
```

^ Since we can embed expressions in JSX by wrapping them in curly braces, we can cut down on repeating the heading element, checked for the status, and send back the content we need.

---

```jsx
function Greeting({isLoggedIn}) {
  return (
    <h1>
      {isLoggedIn
        ? <LogoutButton onClick={handleLogout} />
        : <LoginButton onClick={handleLogin} />
      }
    </h1>
  )
}
```

---

## Inline `if` with Logical `&&` Operator

```javascript
true && expression
```

^ We can also use other operators in these types of expressions, like the logical `&&` operator. This comes in handy for conditionally including an element.

---

```jsx
function Mailbox({messages}) {
  return (
    <>
      <h1>Hello</h1>
      {messages.length > 0 &&
        <p>You have {messages.length} unread messages</p>
      }
    </>
  )
}
```

^ This works because in JavaScript, `true && expression` always evaluates to `expression`, and `false && expression` always evaluates to `false`.

^ Using this syntax, if the condition is `true`, the element right after the `&&` will appear in the output. If the condition is `false`, React will ignore and not render the content.

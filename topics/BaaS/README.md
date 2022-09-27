build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM363

## Backend as a Services (Baas)

---

# Lesson Objectives

- Discuss persisting state
- Discuss Backend as a Service (BaaS)
- Implement a persisting state management system

---

# Objective

## Discuss persisting state

^ We've seen in recent weeks how we can use different techniques to share the various states of our application between components. Each component has it's own local state. Global state of the app can be managed with React Context or another library like Redux. One problem we have yet to deal with is what happens to our state values between sessions. With everything we've build so far, we're good within a single user session. But if we refresh the browser, change pages and try to come back to our application, any changes we've made to state are reset to the defaults.

---

[.background-color: #1F2023]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1653416294/interactive_app_design/persisting_state-dark_mode-settings_pqc2pl.svg)

---

[.background-color: #1F2023]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1653416294/interactive_app_design/persisting_state-dark_mode-state_iygjee.svg)

---

[.background-color: #1F2023]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1653416294/interactive_app_design/persisting_state-dark_mode-localstorage_spfdkm.svg)

^ A localstorage solution for maintaining persisting state is a common solution for handling this problem. But let's take it a step further.

---

[.background-color: #1F2023]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1653418643/interactive_app_design/persisting_state_multiapp_pwfcyw.jpg)

^ Quite frequently users will begin a process on one device and finish it on another. How many of you have added something to your cart or a list on Amazon with your phone, but finished the purchase on your computer? You can do that because the state of your account is available outside of the browser session, and is being synced to every instance of the application where you are signed in.

---

# Objective

## Discuss Backend as a Service (BaaS)

^ Backend-as-a-Service (BaaS) is a cloud service model where developers outsource all of the behind the scenes aspects of a web or mobile application so they only have to write and maintain the frontend.

^ Think of developing an application without using a BaaS provider as directing a movie. A film director is responsible for overseeing or managing camera crews, lighting, set construction, wardrobe, actor casting, and the production schedule, in addition to actually filming and directing the scenes that will appear in the movie. Now imagine if there was a service that took care of all the behind-the-scenes activities so that all the director had to do was direct and shoot the scene. That's the idea of BaaS: The vendor takes care of the 'lights' and the 'camera' (or, the server-side* functionalities) so that the director (the developer) can just focus on the 'action' – what the end user sees and experiences.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1653420814/interactive_app_design/what-is-backend-as-a-service_vwbepv.svg)

^ BaaS vendors provide pre-written software for activities that take place on servers, like authentication, database management, remote updating, push notifications, and cloud storage and hosting.

^ Image courtesy of <https://www.cloudflare.com/learning/serverless/glossary/backend-as-a-service-baas/>

---

## BaaS Providers

- [AWS](https://go.aws/3A3bQ5b)
- [Firebase](https://firebase.google.com)
- [Azure](https://azure.microsoft.com/en-us/)

---

# Objective

## Implement a persisting state<br>management system

^ `playground/react-persist_state`

build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## Hosting

---

# Lesson Objectives

- Review hosting concepts
- Build a React project
- Deploy a React project
- Eject a React project

---

# Objective

## Review hosting concepts

---

[.background-color: #f4f4f4]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1648153205/web_authoring_one/ssr-html_e8vryd.svg)

^ If you remember our discussions earlier in the term, we examined how a user uses a browser to request a file from a server. Apache software on the server finds the correct file and sends it to the browser. The browser renders the code and the user sees the result.

---

[.background-color: #f4f4f4]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1648492111/web_authoring_one/git-30_qckhex.png)

^ Also recall our local work workflow. We used Git to track our changes and commit them to a repository. We push a copy of our repository to GitHub. So we have a copy of all of the files needed for our website on our computer, and a copy of the files on GitHub.

---

[.background-color: #f4f4f4]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1649262131/web_authoring_one/hosting-files_mhaced.svg)

^ The task now is to get our files to the server so they are accessible to our users. There are a number of ways for us to accomplish this. We'll look at a few today.

---

## Integrated hosting

- Netlify
- Vercel
- GitHub Pages
- Heroku
- Azure
- Firebase
- Now
- S3

^ There is a link in the _resources_ document that jumps out to the Create React App deployment documentation, which outlines configuration for all of these different deployment options.

^ Today we'll try Netlify and Vercel

---

# Objective

## Build a React project

---

```shell
npx create-react-app my_app
cd my_app
npm run build
```

---

# Objective

## Deploy a React project

^ Log into Vercel and Netlify and host the project via GitHub

---

# Objective

## Eject a React project

---

## Eject

```shell
npm run eject
```

^ If you aren't satisfied with the build tool and configuration, you can `eject` the app at any time. This will copy all of the configuration files into your project so you have control over them.

^ You don't have to use `eject`, but it's an option if you need to customize your project configuration. This is a one way operation. Once you `eject`, you can't go back.

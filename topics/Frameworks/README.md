build-lists: true
footer: Interactive App Design
slidenumbers: true
slide-transition: true
autoscale: true
theme: SuperHuman, 1

# IDM364

## React Frameworks

---

# Lesson Objectives

- Introduce Next.js
- Introduce Gatsby.js

^ In this topic, we're going to look at two popular frontend frameworks for React. These tools are designed to give developers a solid experience for building static and hybrid websites and applications that support many of today's tools and require minimal configuration. Both of these have pros and cons. We'll introduce each framework and talk about some of the benefits of each and when you might want to reach for one of these for your project.

---

# Objective

## Introduce Next.js

---

[.background-color: #1f2023]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1650384863/interactive_app_design/nextjs_wsov9s.svg)

^ Next.js gives you the best developer experience with all the features you need for production: hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. No config needed.

^ Next.js uses automatic code-splitting, code reloading, and single file components to help developers build attractive React websites.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651591024/interactive_app_design/next.js-workflow_w6zxwo.png)

^ Next.js works by providing an out-of-the-box solution for the server-side rendering of react components. Developers can render javascript code at the server’s end while sending indexable HTML to the user.

^ Image source: <https://medium.com/swlh/the-hitchhikers-guide-to-next-js-fd7aa14ae8d0>

---

## Next.js tools

- image optimization
- internationalization
- analytics
- static site exports
- server side rendering
- TypeScript support
- file system routing
- built in CSS support

---

## Next.js Docs

<https://nextjs.org>

---

# Objective

## Introduce Gatsby.js

^ GatsbyJS is a React-based, GraphQL powered frontend framework that generates static HTML in advance. Gatsby is known for fast page loads through the use of features like static-site generation, asset optimization, data pre-fetching, and code splitting.

^ Gatsby fetches data and content through external APIs and structures the data in a predefined page template for pages to be rendered ahead of time to improve performance and core web vitals.

^ When you code and develop your website, Gatsby uses its power to transform it into a static HTML file. This file is then hosted at your chosen provider, providing unbelievable speed and efficiency.

---

[.background-color: #130820]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1650384864/interactive_app_design/gatsbyjs_gwg50g.svg)

^ The other main frontend framework in the world of React is Gatsby.js. Gatsby boasts many of the same benefits of Next.js, including faster, scalable, secure exports and a favorable development experience.

^ GatsbyJS is a React-based, GraphQL powered frontend framework that generates static HTML in advance. Gatsby is known for fast page loads through the use of features like static-site generation, asset optimization, data pre-fetching, and code splitting.

---

[.background-color: #fff]
[.slidenumbers: false]
[.hide-footer]

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651591024/interactive_app_design/gatsby-how-does-it-work_buklep.png)

^ Gatsby fetches data and content through external APIs and structures the data in a predefined page template for pages to be rendered ahead of time to improve performance and core web vitals. When you code and develop your website, Gatsby uses its power to transform it into a static HTML file. This file is then hosted at your chosen provider, providing unbelievable speed and efficiency.

^ Image source: <https://www.webstacks.com/blog/gatsby-nextjs-breakdown-for-2022>

---

## Gatsby.js Docs

<https://www.gatsbyjs.com>

^ If we look at our routing example, Gatsby handles file based routing in the same way that Next.js does.

---

## Next.js index routes

- `pages/index.js` -> `/`
- `pages/blog/index.js` -> `/blog/`

^ Something I like about these frameworks is how easy they make it to build your site and handle routing. Instead of setting up and managing the routing system manually, we can leverage built in routing functions that are based on our file-system.

^ Next.js has a file-system based router built on the concept of pages. When a file is added to the pages directory, it's automatically available as a route. The files inside the pages directory can be used to define most common patterns.

---

## Next.js nested routes

pages/blog/first-post.js ➡️ /blog/first-post

pages/dash/settings/username.js ➡️ /dash/settings/username

^ The router supports nested files. If you create a nested folder structure, files will automatically be routed in the same way still.

---

## Next.js dynamic routes

pages/blog/[slug].js ➡️ /blog/:slug (/blog/hello-world)

pages/[username]/settings.js ➡️ /:username/settings (/foo/settings)

pages/post/[...all].js ➡️ /post/* (/post/2020/id/title)

^ To match a dynamic segment, you can use the bracket syntax. This allows you to match named parameters.

---

## Linking between pages

```jsx
import Link from 'next/link'

function Home() {
  return (
    <ul>
      <li>
        <Link href="/">
          <a>Home</a>
        </Link>
      </li>
      <li>
        <Link href="/about">
          <a>About Us</a>
        </Link>
      </li>
      <li>
        <Link href="/blog/hello-world">
          <a>Blog Post</a>
        </Link>
      </li>
    </ul>
  )
}
```

^ The Next.js router allows you to do client-side route transitions between pages, similar to a single-page application.

^ Gatsby.js offers a similar setup out of the box.

---

## Which should I choose?

^ Both Gatsby and Next.js are extremely useful for developing impressive websites. Before choosing a framework, stakeholders and developers must know the project requirements to suggest the best framework for the greatest return on investment. We hope this article helps you weigh the options when building a new static website. Let's compare some of the key differences.

---

## Data Fetching

```javascript
const Navbar = props => {
  return (
    <StaticQuery
      query={graphql`
        query {
          site {
            siteMetadata {
              title
            }
          }
        }
      `}
      render={data => <Brand data={data} {...props} />}
    />
  );
};
```

^ Data fetching is one of the larger differences that you would encounter when working with either framework. Next.js is agnostic about the data fetching method you wish to use. You can define it, implement it, and consume it however you wish, whether that’s via a REST API, a GraphQL API, or something else. Next.js doesn’t mind.

^ But, with Gatsby, it’s a different story. While Gatsby does support sourcing data without using its GraphQL data layer. Gatsby advises against this and pushes people to use their GraphQL data layer. This means if you want to query data in Gatsby on your pages or during the build phase, you’ll almost certainly be using GraphQL.

^ Gatsby boasts about the benefits that come from using GraphQL, like automatically optimizing images and allowing you to load data in the same place it’s consumed.

^ If you don’t like GraphQL, then Next.js will likely be a better fit because you can query data without it. But, if you prefer using GraphQL or want a great opportunity to become more familiar with it, then Gatsby would be a great choice for your next project.

---

## Plugins & Ecosystem

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651594466/interactive_app_design/ecosystem_zr5zcd.svg)

^ [Gatsby Plugin Library](https://www.gatsbyjs.com/plugins)

^ Both frameworks have very vibrant and active communities that contribute to the development and advancement of each framework overall. But, there is a key difference in the structure of these frameworks and how the community influences them. Gatsby has a heavy reliance on its community-authored plugins, which anyone can use in their applications for things like sourcing and transforming data or styling a site.

^ In essence, Gatsby makes it very easy to template out and create a new website. If you wanted to create a blog, for example, using Markdown, you could use the gatsby-source-filesystem plugin to source all your blog posts to GraphQL and then query them on your page. This is true for other things as well, like adding Google Analytics to a website; just use their gatsby-plugin-google-analytics plugin, give it your tracking ID, and it does the rest for you.

^ With Next.js, where there isn’t a plugin community like Gatsby’s, the developer has to do all of this work themselves. If you want a blog using Markdown then you need to source and transform the data yourself. So, if you don’t mind doing this type of work or want full control of the data sourcing process, as well as the nitty-gritty details of the code, then Next.js is best.

---

## Troubleshooting

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651594466/interactive_app_design/troubleshooting_wsijyf.svg)

^ Following the last section, you may be thinking that Gatsby sounds amazing and that having a lot of setup done for you is amazing. That is until it’s not.

^ Because the approach that Gatsby is often known for can be so reliant on plugins and other people’s work, troubleshooting a problem in the code can be a big pain for the developers. To get around this issue, you ideally need to fall into one of two categories: You don't mind waiting for other people to resolve a problem and push an update, or you don't mind being active in the open-source community and resolving problems yourself.

^ If you don't fit into one of those categories, you may want to consider Next.js instead.

---

## Render Methods

![fit](https://res.cloudinary.com/pjs-uxid/image/upload/v1651594466/interactive_app_design/rendering-methods_bukhxq.svg)

^ Both of these frameworks support Static-Site Generation (SSG), Server-Side Rendering (SSR), and Client-Side Rendering (CSR). They also both support deferred static rendering but with one subtle but important difference in how they implement it. It’s this difference that might help you choose between Gatsby and Next. We won't dig into this level of detail today, but there is plenty of information available online when you're ready to research.

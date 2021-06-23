# Vue 3 Studies - App Development / Nuxt / Vue CLI

- 🚌&nbsp;&nbsp; Course on [Frontend Masters](https://frontendmasters.com/courses/vue-3/)
- 👩‍🏫&nbsp;&nbsp; Taught by [Sarah Drasner](https://twitter.com/sarah_edo)
- 📓&nbsp;&nbsp; Notes by [Mel Jones](https://twitter.com/_moodybones)
- 📎&nbsp;&nbsp; Link to [GitHub Starter Docs & Slides](https://github.com/sdras/intro-to-vue)

# Codepen links to ALL my Vue 3 Collections

- [Directives](https://codepen.io/collection/nGrgGW)
- [Exercises/Challenges](https://codepen.io/collection/DrRLoJ)
- [Methods](https://codepen.io/collection/nmomeM)

# Single File Components / Vue CLI & Nuxt

- [slides](https://slides.com/sdrasner/intro-to-vue-3-4?token=0IQFDZvK)

### Why?

- Build processes that allow us to use great features like ES6, or SCSS, easy to use other libraries
- We're going to build and concatenate single file templates
- Not load all our files at startup (lazy load, async)
- Server-side rendering, code-splitting, performance metrics...
  - can monitor if we added too many libaries or how much we're creating on every builds
- Build/prod versions
- Production version
  - it will alert you on errors
  - if you are using a separate production & development version, then you can see the errors, you can get console logs, you can get dev tools
- Build version
  - then for production it will make sure it's minified and concatenated and the smallest amount possible
  - the errors and dev tools and logs don't show

## Single File Templates

```js
<template>
  <div>
     <!-- Write your HTML with Vue in here -->
  </div>
</template>

<script>
  // import librarys here
  export default {
     // Write your Vue component logic here
  }
</script>

<style scoped>
  /* Write your styles for the component in here */
</style>
```

**VUE FILES MEAN NOCONTEXT-SHIFTING!**

- you don't have to move from file to file
- good for people that get lost when they open
- [check out Sarah's VSCode Vue Pack](https://marketplace.visualstudio.com/items?itemName=sdras.vue-vscode-extensionpack)
- Bookmarks
  - `cmd + opt + K` to create
  - `cmd + opt + J` to jump between

`$`

```
// Sarah' Vue CLI preferences
Manually select
---
Babel
VueX
SCSS preprocessors
---
Vue 3
---
node sass
---
package.json
---

```

### Vue CLI

- gives a some starters and folders and boilerplates
- start with `App.vue` it has the default CSS styling
- Mounting of the app happens in `main.js`
- When we build all the files, in the public folder you will find `index.html`
  - add fonts or other links here

### Nuxt vs Vue CLI

- In Nuxt rendering is totally different
  - It's a meta framework, its a framework on top of Vue

### Vue style guide

- main CS/SCSS styles should be added to a top level component like `App.vue` or in an individual `main.css/index.scss` file
- any component below should have scoped CSS/SCSS

### hub

- for creating new gitHub repos

`$`

```js
// p is from private, you can add a name or if no name added it will use the name of the folder
hub create -p

git add -A

git commit -m "initial commit"

git push -u origin master

```

### Deploying with Netlify & GitHub

- build tool is in readme

```
### Compiles and minifies for production
npm run build
```

- public directory is dist

### Huge thanks to Sarah Drasner & the Frontend Masters Team.
